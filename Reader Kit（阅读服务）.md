# Reader Kit简介

更新时间: 2025-12-16 16:35

Reader Kit（阅读服务）为开发者提供多种格式电子书的解析、排版、阅读交互能力，开发者可以借助Reader Kit的能力和组件快速构建书籍阅读能力。

## 能力范围

Reader Kit提供的能力如下：

- 多种格式书籍的解析能力：提供对txt、epub、mobi、azw、azw3格式书籍进行解析的能力，可获取书籍中的书名、作者、书封、目录以及目录对应的正文内容。
- txt、富文本内容排版能力：支持对标准的txt、富文本内容（html+css）按仿真和横滑方式进行分页排版，并提供排版快照和排版信息。
- 阅读页组件（ReadPageComponent）：支持对书籍排版内容的显示、多种翻页交互和翻页动效，以及翻页阅读过程中阅读器所需要的进度、行为感知能力。

## 亮点/特征

- 支持多种电子书籍格式解析，提供标准规范的书籍信息和内容数据。
- 对富文本内容（html+css）的排版符合W3C标准规范，且对排版过程做了高效的算法优化，提高了排版速度和效率。
- 对内容进行展示时，除了支持系统字体之外，还支持扩展自定义字体，满足用户的个性化需求。
- 阅读页组件（ReadPageComponent）提供常用的阅读交互能力，支持多种翻页方式，采用OpenGL（C/C++）绘制翻页动效，阅读过程更丝滑，更流畅。

## 基本概念

- ReadPageComponent
    
    Reader Kit封装的阅读页UI组件[ReadPageComponent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/reader-api-readpagecomponent)（ets），支持对书籍排版内容的显示、多种翻页交互和翻页动效，以及翻页阅读过程中阅读器所需要的进度、行为感知能力。
    
- BookParser
    
    电子书解析引擎[bookParser](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/reader-book-parser)，支持txt、epub、mobi、azw、azw3格式书籍文件的解析。
    
- spine(书脊)
    
    书的背脊；平装书或精装书封面和封底的联结处。一般印有书名、作者名、出版单位名等。在Reader Kit中，spine(书脊)定义了书籍内容的阅读顺序，每一个[SpineItem](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/reader-book-parser#section1029864651619)表示一个可阅读的内容节点，标识着可阅读的一个内容资源。
    

## 约束和限制

- 在书籍处理过程中，Reader Kit只支持有本地文件的书籍，不支持在线的文件流，且不同的书籍文件需要存放在应用沙箱下的不同目录。
- 在书籍处理过程中，Reader Kit不提供对书籍的DRM保护能力。
- 解析能力只支持对txt、epub、mobi、azw、azw3标准格式的书籍文件进行解析，对于非标准格式的书籍在解析时可能会抛出异常，开发者需要捕获和处理。
- 排版引擎及交互能力需要配套Reader Kit的阅读页组件（ReadPageComponent）使用。

### 设备限制

Reader Kit仅适用于HarmonyOS NEXT 5.0.4及以上版本的Phone、PC/2in1、Tablet设备，暂**不支持模拟器**使用。

### 支持的国家/地区

Reader Kit当前仅在中国境内（香港特别行政区、澳门特别行政区、中国台湾除外）提供服务。

## 示例代码

Reader Kit开发指南涉及到的示例代码均为片段，全量示例代码请参考：[CodeLabs](https://developer.huawei.com/consumer/cn/codelabsPortal/carddetails/tutorials_NEXT-ReaderKit)或[SampleCode](https://gitcode.com/HarmonyOS_Samples/readerkit_samplecode_arkts)。CodeLabs和SampleCode包括了导入本地书籍、构建阅读器、构建目录列表、修改阅读设置等场景的完整实践示例，可帮助开发者更好的使用Reader Kit API。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/reader-kit-guide "Reader Kit（阅读服务）")
# 获取书籍信息

更新时间: 2025-12-16 16:36

当应用需要导入本地书籍到书架时，开发者可通过[DocumentViewPicker](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-file-picker#documentviewpicker)先将书籍文件导入到[应用沙箱目录](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-sandbox-directory)。然后利用解析能力获取书籍信息，用于书架中书封，书名，作者等信息的展示。

## 业务流程

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163638.61971934676935137476853699328280:50001231000000:2800:4FA0A9839FFB624DB6FA543FFA4C320CD9E9556413E14ED07A945777F902A80D.png "点击放大")

## 接口说明

获取书籍信息共涉及3个接口，具体API说明请参考下表。

|接口名|描述|
|:--|:--|
|[getDefaultHandler](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/reader-book-parser#section896820167243)(path: string): Promise<BookParserHandler>|获取书籍默认解析器。|
|[getBookInfo](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/reader-book-parser#section599065683812)(): BookInfo|获取书籍信息。|
|[getResourceContent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/reader-book-parser#section17546184255211)(spineIndex: number, filePath: string): ArrayBuffer|获取书籍内容资源。|

## 开发步骤

1. 导入相关模块。
    
    1. import { common } from '@kit.AbilityKit';
    2. import { bookParser } from '@kit.ReaderKit';
    3. import { hilog } from '@kit.PerformanceAnalysisKit';
    4. import { image } from '@kit.ImageKit';
    
2. 通过提前导入到[应用沙箱目录](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-sandbox-directory)中的书籍文件，初始化书籍解析器。
    
    1. private defaultHandler: bookParser.BookParserHandler | null = null;
    
    2. aboutToAppear(): void {
    3.   this.init().then(() => {
    4.   });
    5. }
    
    6. private async init() {
    7.   let context = this.getUIContext().getHostContext() as common.UIAbilityContext;
    8.   let path: string = `${context.filesDir}/abc.epub`;
    9.   try {
    10.     this.defaultHandler = await bookParser.getDefaultHandler(path);
    11.   } catch (error) {
    12.     hilog.error(0x0000, "testTAG", `getDefaultHandler failed, Code: ${error.code}, message: ${error.message}`);
    13.   }
    14. }
    
3. 获取书名、作者、书封信息并进行展示。
    
    1. @State bookCover: PixelMap | null = null;
    2. @State bookTitle: string = '';
    3. @State author: string = '';
    
    4. aboutToAppear(): void {
    5.   this.init().then(() => {
    6.     this.getBookInfo();
    7.   });
    8. }
    
    9. private async getBookInfo() {
    10.   try {
    11.     let bookInfo: bookParser.BookInfo | undefined = this.defaultHandler?.getBookInfo();
    12.     if (bookInfo) {
    13.       this.bookTitle = bookInfo.bookTitle || '';
    14.       this.author = bookInfo?.bookCreator || '';
    15.       // SpineIndex is not required for obtaining the book cover.
    16.       let buffer = this.defaultHandler?.getResourceContent(-1, bookInfo.bookCoverImage);
    17.       let imageSource: image.ImageSource = image.createImageSource(buffer);
    18.       this.bookCover = await imageSource.createPixelMap();
    19.       imageSource.release();
    20.     }
    21.     hilog.info(0x0000, 'testTAG', 'getBookInfo bookInfo is: ' + JSON.stringify(bookInfo));
    22.   } catch (error) {
    23.     hilog.error(0x0000, 'testTAG', `getBookInfo failed, Code: ${error.code}, message: ${error.message}`);
    24.   }
    25. }
    
    26. build() {
    27.   Column() {
    28.     Text('书名：' + this.bookTitle)
    29.       .fontSize(20)
    30.       .fontColor("#E6000000")
    31.       .margin({ top: 50 })
    32.     Text('作者：' + this.author)
    33.       .fontSize(20)
    34.       .fontColor("#E6000000")
    35.       .margin({ top: 10 })
    36.     Image(this.bookCover)
    37.       .width(200)
    38.       .aspectRatio(3 / 4)
    39.       .borderRadius(5)
    40.       .margin({ top: 10 })
    41.   }
    42.   .alignItems(HorizontalAlign.Start)
    43.   .margin({ left: 10, right: 10 })
    44. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/reader-parser "书籍内容解析")
# 获取目录列表

更新时间: 2025-12-16 16:36

当应用需要展示书籍目录列表时，开发者可通过解析能力获取目录节点列表，实现目录列表中章节名称按顺序、层级的展示。当用户点击目录节点时，开发者也需要获取目录位置及资源信息，用于跳转到指定位置。

## 业务流程

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163654.57637435474691043382759737958133:50001231000000:2800:C5B903FEFCD95F77F6D2AFB12C66BEAA44D151ADF1066FD55AE507B0F5E8890A.png "点击放大")

## 接口说明

获取目录列表及获取指定目录位置及资源信息共涉及4个接口，具体API说明请参考下表。

|接口名|描述|
|:--|:--|
|[getDefaultHandler](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/reader-book-parser#section896820167243)(path: string): Promise<BookParserHandler>|获取书籍默认解析器。|
|[getCatalogList](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/reader-book-parser#section14841714114211)(): CatalogItem[]|获取书籍目录列表。|
|[getDomPosByCatalogHref](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/reader-book-parser#section124930457617)(href: string): string|获取阅读起始位置domPos。|
|[getSpineList](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/reader-book-parser#section61575276477)(): SpineItem[]|获取书脊内容列表。|

## 开发步骤

1. 导入相关模块。
    
    1. import { common } from '@kit.AbilityKit';
    2. import { bookParser } from '@kit.ReaderKit';
    3. import { hilog } from '@kit.PerformanceAnalysisKit';
    
2. 通过提前导入到[应用沙箱目录](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-sandbox-directory)中的书籍文件，初始化书籍解析器。
    
    1. private defaultHandler: bookParser.BookParserHandler | null = null;
    
    2. aboutToAppear(): void {
    3.   this.init().then(() => {
    4.   });
    5. }
    
    6. private async init() {
    7.   let context = this.getUIContext().getHostContext() as common.UIAbilityContext;
    8.   let path: string = `${context.filesDir}/abc.epub`;
    9.   try {
    10.     this.defaultHandler = await bookParser.getDefaultHandler(path);
    11.   } catch (error) {
    12.     hilog.error(0x0000, "testTAG", `getDefaultHandler failed, Code: ${error.code}, message: ${error.message}`);
    13.   }
    14. }
    
3. 获取目录列表并进行展示。
    
    1. @State catalogItemList: bookParser.CatalogItem[] = [];
    
    2. aboutToAppear(): void {
    3.   this.init().then(() => {
    4.     this.getCatalogList();
    5.   });
    6. }
    
    7. private getCatalogList() {
    8.   try {
    9.     this.catalogItemList = this.defaultHandler?.getCatalogList() || [];
    10.   } catch (error) {
    11.     hilog.error(0x0000, "testTAG", `getCatalogList failed, Code: ${error.code}, message: ${error.message}`);
    12.   }
    13. }
    
    14. build() {
    15.   Column() {
    16.     List() {
    17.       ForEach(this.catalogItemList, (item: bookParser.CatalogItem) => {
    18.         ListItem() {
    19.           Column() {
    20.             Row() {
    21.               Row() {
    22.                 Text(' · ')
    23.                   .fontSize(14)
    24.                 Text(item.catalogName)
    25.                   .fontSize(14)
    26.                   .textOverflow({ overflow: TextOverflow.Ellipsis })
    27.                   .padding({ top: 8, bottom: 8 })
    28.                   .maxLines(2)
    29.                   .layoutWeight(1)
    30.               }
    
    31.             }
    32.             .width('100%')
    33.             .height(48)
    34.             .justifyContent(FlexAlign.Center)
    35.             .alignItems(VerticalAlign.Center)
    
    36.             Divider()
    37.           }
    38.           .padding({
    39.             left: item.catalogLevel ? item.catalogLevel * 26 : 10,
    40.             right: item.catalogLevel ? item.catalogLevel * 26 : 10,
    41.             top: 6,
    42.             bottom: 6
    43.           })
    44.           .onClick(async () => {
    45.             // 在此实现点击目录跳转到指定章节功能
    46.             this.jumpToCatalogItem(item);
    47.           })
    48.         }
    49.       })
    50.     }
    51.     .scrollBar(BarState.Off)
    52.     .width('100%')
    53.     .height('100%')
    54.   }
    55.   .width('100%')
    56.   .height('100%')
    57. }
    
4. 获取跳转用的目录位置及资源信息。
    
    1. private jumpToCatalogItem(catalogItem: bookParser.CatalogItem) {
    2.   let domPos = this.getDomPos(catalogItem);
    3.   let resourceIndex = this.getResourceItemByCatalog(catalogItem).index;
    4.   // 通过domPos及resourceIndex信息，即可通过startPlay接口跳转到指定位置
    5.   hilog.info(0x0000, "testTAG", `jumpToCatalogItem domPos:${domPos}, resourceIndex:${resourceIndex}`);
    6. }
    
    7. private getDomPos(catalogItem: bookParser.CatalogItem): string {
    8.   try {
    9.     let domPos: string = this.defaultHandler?.getDomPosByCatalogHref(catalogItem.href || '') || '';
    10.     return domPos;
    11.   } catch (error) {
    12.     hilog.error(0x0000, "testTAG", `getDomPos failed, Code: ${error.code}, message: ${error.message}`);
    13.   }
    14.   return '';
    15. }
    
    16. /**
    17.  * 获取书籍目录对应的资源条目
    18.  *
    19.  * @param catalogItem 目录条目
    20.  */
    21. private getResourceItemByCatalog(catalogItem: bookParser.CatalogItem): bookParser.SpineItem {
    22.   let resourceFile = catalogItem.resourceFile || '';
    23.   try {
    24.     let spineList: bookParser.SpineItem[] = this.defaultHandler?.getSpineList() || []
    25.     // 查找目录对应的资源条目
    26.     let resourceItemArr = spineList.filter(item => item.href === resourceFile);
    27.     if (resourceItemArr.length > 0) {
    28.       hilog.info(0x0000, 'testTag', 'getResourceItemByCatalog get resource ', resourceItemArr[0]);
    29.       let resourceItem = resourceItemArr[0];
    30.       return resourceItem;
    31.     } else if (spineList.length > 0) {
    32.       // 如果查找不到，则默认返回第1个资源条目
    33.       hilog.info(0x0000, 'testTag', 'getResourceItemByCatalog get resource in resourceList', spineList[0]);
    34.       return spineList[0];
    35.     }
    36.   } catch (error) {
    37.     hilog.error(0x0000, "testTAG", `getDomPos failed, Code: ${error.code}, message: ${error.message}`);
    38.   }
    39.   // 如果没有资源条目，则返回默认值
    40.   hilog.info(0x0000, 'testTag', 'getResourceItemByCatalog get resource in escape');
    41.   return {
    42.     idRef: '',
    43.     index: 0,
    44.     href: '',
    45.     properties: ''
    46.   };
    47. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/reader-book-info "获取书籍信息")
# 构建阅读器

更新时间: 2025-12-16 16:36

Reader Kit提供的阅读页组件ReadPageComponent，支持对标准的txt和富文本内容（html+css）按仿真和横滑方式进行分页排版的能力、支持翻页阅读过程中所需要的进度和行为感知能力。利用ReadPageComponent，开发者可快速实现书籍阅读的能力。

## 业务流程

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163638.84548092882073057102216712435228:50001231000000:2800:0DF4D8E37C1C69B1FC335CB674BDA72F706D6B1213154ED7ED078767E963BC1B.png "点击放大")

## 接口说明

构建书籍阅读能力共涉及5个接口，具体介绍如下表所示。

|接口名|描述|
|:--|:--|
|[getDefaultHandler](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/reader-book-parser#section896820167243)(path: string): Promise<BookParserHandler>|获取书籍默认解析器。|
|[init](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/reader-read-core#section8938164817438)(context: common.UIAbilityContext): Promise<void>|初始化ReadPageComponent控制器。<br><br>初始化接口需要优先于ReaderComponentController的其他接口之前执行。|
|[setPageConfig](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/reader-read-core#section6297758718)(pageConfig: ReaderSetting): void|设置或者修改页面排版属性。|
|[registerBookParser](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/reader-read-core#section181215815104)(bookParserHandler: bookParser.BookParserHandler): void|注册书籍解析器。<br><br>需要在startPlay接口调用之前执行。|
|[startPlay](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/reader-read-core#section3667128165411)(spineIndex: number, domPos: string): Promise<void>|以指定阅读进度打开书籍，使用Promise异步回调。<br><br>需要在registerBookParser接口调用之后执行。|

## 开发步骤

1. 导入相关模块。
    
    1. // 导入解析能力、页面组件和阅读器控制类
    2. import { bookParser, ReadPageComponent, readerCore } from '@kit.ReaderKit';
    3. import { BusinessError } from '@kit.BasicServicesKit';
    4. import { display } from '@kit.ArkUI';
    5. import { hilog } from '@kit.PerformanceAnalysisKit';
    6. import { common } from '@kit.AbilityKit';
    
2. 初始化组件控制器、默认设置项，以及定义书籍解析器。
    
    1. // 组件控制器，用于调用排版相关能力。
    2. private readerComponentController: readerCore.ReaderComponentController = new readerCore.ReaderComponentController();
    3. // 默认设置项，用于初始化阅读器页面的默认属性。
    4. private readerSetting: readerCore.ReaderSetting = {
    5.   fontName: '系统字体',
    6.   fontPath: '',
    7.   fontSize: 18,
    8.   fontColor: '#000000',
    9.   fontWeight: 400,
    10.   lineHeight: 1.9,
    11.   nightMode: false,
    12.   themeColor: 'rgba(248, 249, 250, 1)',
    13.   themeBgImg: '',
    14.   flipMode: '0',
    15.   scaledDensity: display.getDefaultDisplaySync().scaledDensity > 0 ? display.getDefaultDisplaySync().scaledDensity :
    16.     1,
    17.   viewPortWidth: 1260, // 视口宽度，需要根据设备实际情况获取，否则会导致阅读界面异常
    18.   viewPortHeight: 2720, // 视口高度，需要根据设备实际情况获取，否则会导致阅读界面异常
    19. };
    20. // 书籍解析器，用于注册给组件控制器，供排版引擎调用。
    21. private bookParserHandler: bookParser.BookParserHandler | null = null;
    22. // 是否正在加载页面（需要等待页面渲染完成再隐藏，避免进入页面会先显示黑屏的问题）
    23. @State isLoading: boolean = true;
    
3. 构建ReadPageComponent组件，用于显示阅读内容。
    
    1. build() {
    2.   Stack() {
    3.     ReadPageComponent({
    4.       controller: this.readerComponentController,
    5.       readerCallback: (err: BusinessError, data: readerCore.ReaderComponentController) => {
    6.         this.readerComponentController = data;
    7.       }
    8.     })
    
    9.     Row() {
    10.       Text('加载中...')
    11.     }
    12.     .width('100%')
    13.     .height('100%')
    14.     .justifyContent(FlexAlign.Center)
    15.     .backgroundColor(Color.White)
    16.     .visibility(this.isLoading ? Visibility.Visible : Visibility.None)
    17.   }.width('100%').height('100%')
    18. }
    
4. 通过提前导入到[应用沙箱目录](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-sandbox-directory)中的书籍文件，初始化书籍解析器。调用[startPlay](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/reader-read-core#section3667128165411)接口，以指定进度渲染阅读器页面。
    
    1. aboutToAppear(): void {
    2.   // 初始化阅读器
    3.   let context = this.getUIContext().getHostContext() as common.UIAbilityContext;
    4.   let filePath: string = `${context.filesDir}/abc.epub`;
    5.   let spineIndex: number = 0;
    6.   let domPos: string = '';
    7.   this.registerListener();
    8.   this.startPlay(filePath, spineIndex, domPos);
    9. }
    
    10. private registerListener(): void {
    11.   this.readerComponentController.on('pageShow', (data: readerCore.PageDataInfo): void => {
    12.     hilog.info(0x0000, 'testTag', 'pageshow: data is: ' + JSON.stringify(data));
    13.     if (data.state === readerCore.PageState.PAGE_ON_SHOW) {
    14.       this.isLoading = false;
    15.     }
    16.   });
    17. }
    
    18. private async startPlay(filePath: string, spineIndex: number, domPos: string) {
    19.   try {
    20.     let context = this.getUIContext().getHostContext() as common.UIAbilityContext;
    21.     // 组件控制器初始化，用于控制ReadPageComponent调用排版引擎
    22.     let initPromise = this.readerComponentController.init(context);
    23.     // 初始化书籍解析器
    24.     let bookParserHandler = bookParser.getDefaultHandler(filePath);
    25.     let result: [bookParser.BookParserHandler, void] = await Promise.all([bookParserHandler, initPromise]);
    26.     this.bookParserHandler = result[0];
    27.     // 设置默认页面属性，用于排版的默认样式
    28.     this.readerComponentController.setPageConfig(this.readerSetting);
    29.     // 注册解析能力到控制器中，用于排版引擎的调用。
    30.     this.readerComponentController.registerBookParser(this.bookParserHandler);
    31.     // 调用打开书籍接口，跳章至对应进度
    32.     this.readerComponentController.startPlay(spineIndex|| 0, domPos);
    33.   } catch (err) {
    34.     hilog.error(0x0000, 'testTag', 'startPlay: err: ' + JSON.stringify(err));
    35.   }
    36. }
    
    37. aboutToDisappear(): void {
    38.   this.readerComponentController.off('pageShow');
    39.   // 退出需要释放阅读器实例
    40.   this.readerComponentController.releaseBook();
    41. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/reader-content "书籍内容排版")
# 自定义字体

更新时间: 2025-12-16 16:37

当应用需要支持自定义字体时，开发者可通过[ReaderSetting](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/reader-read-core#section13615732174218)的fontPath属性，实现对阅读内容字体的实时修改。

自定义字体文件支持两种存放路径：

- 工程目录resources/rawfile文件夹。
- [应用沙箱目录](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-sandbox-directory)。

## 业务流程

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163754.55770690681271554308659702913155:50001231000000:2800:458AFE07C83D7A497EF4688B9D863D6CBE61A02FEFB8E0879AEB1B02CB3974AE.png "点击放大")

## 接口说明

自定义字体主要涉及3个接口，具体介绍如下表所示。

|接口名|描述|
|:--|:--|
|[setPageConfig](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/reader-read-core#section6297758718)(pageConfig: ReaderSetting): void|设置或者修改页面排版属性。|
|[on('resourceRequest')](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/reader-read-core#section169541417131914)|注册资源请求回调，如果设置了自定义背景，字体时，排版引擎会通过此接口获取对应的资源ArrayBuffer。|
|[off('resourceRequest')](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/reader-read-core#section3912114022216)|注销资源请求回调接口，可在页面销毁时调用。|

## 开发准备

- 进行自定义字体之前，请先确保已经“[构建阅读器](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/reader-read-page)”。
- 已经准备好字体资源，并放在对应的目录当中。

## 开发步骤

1. 导入相关模块。
    
    1. import { fileIo as fs } from '@kit.CoreFileKit';
    2. import { common } from '@kit.AbilityKit';
    3. import { hilog } from '@kit.PerformanceAnalysisKit';
    
2. 定义字体文件存放路径：
    - 若资源放在项目resources/rawfile/fonts文件夹下。
        
        1. let filePath: string = 'fonts/SourceHanSerifCN-VF.ttf';
        
    - 若资源放在[应用沙箱目录](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-sandbox-directory)下。
        
        1. let filePath: string = this.getUIContext().getHostContext()!.filesDir + '/fonts/SourceHanSerifCN-VF.ttf'  
        
3. 通过ReaderSetting的fontName和fontPath属性设置自定义字体的名称及所在的路径，并调用ReaderComponentController组件控制器的setPageConfig接口，重新渲染界面。
    
    1. this.readerSetting.fontName = '思源宋体';
    2. // 路径为上述两种之一
    3. this.readerSetting.fontPath = filePath;
    4. this.readerComponentController.setPageConfig(this.readerSetting);
    
4. 注册排版引擎资源请求接口，并返回相应资源。
    
    当排版引擎检测到是自定义字体场景时，会通过接口请求字体资源。开发者需要根据返回的文件路径，判断是否为请求字体资源。如果是，则根据字体资源所在的路径，返回对应的ArrayBuffer。
    
    1. aboutToAppear(): void {
    2.   // 注册资源请求回调
    3.   this.readerComponentController.on('resourceRequest', this.resourceRequest);
    4. }
    
    5. aboutToDisappear(): void {
    6.   // 注销资源请求回调
    7.   this.readerComponentController.off('resourceRequest');
    8. }
    
    9. private isFont(filePath: string): boolean {
    10.   let options = [".ttf", ".woff2", ".otf"];
    11.   let path = filePath.toLowerCase();
    12.   let result = path.indexOf(options[0]) != -1 || path.indexOf(options[1]) != -1 || path.indexOf(options[2]) != -1;
    13.   hilog.info(0x0000, 'testTag',  'isFont = ' + result);
    14.   return result;
    15. }
    
    16. /**
    17.  * 资源请求回调
    18.  */
    19. private resourceRequest: bookParser.CallbackRes<string, ArrayBuffer> = (filePath: string): ArrayBuffer => {
    20.   hilog.info(0x0000, 'testTag', 'resourceRequest : filePath = ' + filePath);
    21.   if (filePath.length === 0) {
    22.     return new ArrayBuffer(0);
    23.   }
    24.   if (!this.isFont(filePath)) {
    25.     return new ArrayBuffer(0);
    26.   }
    27.   try {
    28.     let context = this.getUIContext().getHostContext() as common.UIAbilityContext;
    29.     // 获取资源路径resources/rawfile/fonts下的字体文件Uint8Array数据
    30.     let value: Uint8Array = context.resourceManager.getRawFileContentSync(this.readerSetting.fontPath);
    31.     hilog.info(0x0000, 'testTag', 'resourceRequest : get other resource succeeded ');
    32.     return value.buffer as ArrayBuffer;
    33.   } catch (error) {
    34.     let code = (error as BusinessError).code;
    35.     let message = (error as BusinessError).message;
    36.     hilog.error(0x0000, 'testTag',
    37.       `resourceRequest : get other resource failed, error code: ${code}, message: ${message}.`);
    38.   }
    39.   // 如果在资源路径源路径resources/rawfile/fonts下获取字体文件数据失败，则去沙箱目录下获取字体文件数据
    40.   return this.loadFileFromPath(this.readerSetting.fontPath);
    41. }
    
    42. private loadFileFromPath(filePath: string): ArrayBuffer {
    43.   try {
    44.     let stats = fs.statSync(filePath);
    45.     let file = fs.openSync(filePath, fs.OpenMode.READ_ONLY);
    46.     let buffer = new ArrayBuffer(stats.size);
    47.     fs.readSync(file.fd, buffer);
    48.     fs.closeSync(file);
    49.     return buffer;
    50.   } catch (err) {
    51.     hilog.error(0x0000, 'testTag', "mkdir failed with error message: ", err.message, ", error code: ", err.code);
    52.     return new ArrayBuffer(0);
    53.   }
    54. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/reader-setting "修改阅读设置")
# 自定义页面背景

更新时间: 2025-12-16 16:38

当应用需要支持自定义背景时，开发者可通过[ReaderSetting](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/reader-read-core#section13615732174218)的themeColor及themeBgImg属性，实现对阅读内容自定义背景色及背景图片的实时修改。

更改页面背景色，可能会涉及到字体颜色和深色模式的适配。比如：设置了白色背景，但是当前是深色模式，字体颜色也是白色，这样会导致内容看不清楚。

自定义页面背景图片支持两种存放路径：

- 工程目录resources/rawfile文件夹。
- [应用沙箱目录](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-sandbox-directory)。

## 业务流程

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163801.89899334672305998576094623309277:50001231000000:2800:00FF8A4842C8E7831C22076BE9D9FB5DC2ACD507BF21D45B116D2AC1D5750204.png "点击放大")

## 接口说明

自定义页面背景主要涉及1个接口，具体介绍如下表所示。

|接口名|描述|
|:--|:--|
|[setPageConfig](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/reader-read-core#section6297758718)(pageConfig: ReaderSetting): void|设置或者修改页面排版属性。|

## 开发准备

- 进行自定义背景之前，请先确保已经“[构建阅读器](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/reader-read-page)”。
- 已经准备好自定义背景图片资源，并放在对应的目录当中。

## 开发步骤

1. 导入相关模块。
    
    1. import { fileIo as fs } from '@kit.CoreFileKit';
    2. import { common } from '@kit.AbilityKit';
    3. import { hilog } from '@kit.PerformanceAnalysisKit';
    
2. 单独设置背景色。如果有设置背景图片的情况下，背景色通常用于仿真翻页时背面主题色的绘制。否则，背景色还会用于渲染阅读页的背景色。
    
    1. this.readerSetting.themeColor = '#000000';
    2. this.readerSetting.themeBgImg = '';
    3. // 当设置背景色为浅色时，需要将深色模式关掉
    4. this.readerSetting.nightMode = false;
    5. // 当设置背景色为浅色时，字体颜色也需要适配
    6. this.readerSetting.fontColor = '#FFFFFF';
    
3. 设置背景图片。需要同时设置与背景图片相近的主题颜色，用于仿真翻页时背面主题色的绘制。
    
    1. this.readerSetting.themeBgImg = 'dark_sky_first.jpg';
    2. this.readerSetting.themeColor = '#000000';
    3. // 当设置背景图为浅色时，需要将深色模式关掉
    4. this.readerSetting.nightMode = false;
    5. // 当设置背景图为浅色时，字体颜色也需要适配
    6. this.readerSetting.fontColor = '#FFFFFF';
    
4. 调用ReaderComponentController组件控制器的setPageConfig接口，重新渲染界面。
    
    1. this.readerComponentController.setPageConfig(this.readerSetting);
    
5. 注册排版引擎资源请求接口，并返回相应的背景图资源。
    
    在排版引擎检测到是自定义背景图片场景时，会通过接口请求背景图片资源。开发者需要根据返回的文件路径，判断是否为请求背景图片资源。如果是，则根据背景图片资源所在的路径，返回对应的ArrayBuffer。
    
    1. aboutToAppear(): void {
    2.   // 注册资源请求回调
    3.   this.readerComponentController.on('resourceRequest', this.resourceRequest);
    4. }
    
    5. aboutToDisappear(): void {
    6.   // 注销资源请求回调
    7.   this.readerComponentController.off('resourceRequest');
    8. }
    
    9. /**
    10.  * 资源请求回调
    11.  */
    12. private resourceRequest: bookParser.CallbackRes<string, ArrayBuffer> = (filePath: string): ArrayBuffer => {
    13.   hilog.info(0x0000, 'testTag', 'resourceRequest : filePath = ' + filePath);
    14.   if(filePath.length === 0){
    15.     return new ArrayBuffer(0);
    16.   }
    17.   try {
    18.     let context = this.getUIContext().getHostContext() as common.UIAbilityContext;
    19.     // 获取资源路径resources/rawfile下的背景图片文件Uint8Array数据
    20.     let value: Uint8Array = context.resourceManager.getRawFileContentSync(filePath);
    21.     hilog.info(0x0000, 'testTag', 'resourceRequest : get other resource succeeded ');
    22.     return value.buffer as ArrayBuffer;
    23.   } catch (error) {
    24.     let code = (error as BusinessError).code;
    25.     let message = (error as BusinessError).message;
    26.     hilog.error(0x0000, 'testTag',
    27.       `resourceRequest : get other resource failed, error code: ${code}, message: ${message}.`);
    28.   }
    29.   // 如果在资源路径源路径resources/rawfile下获取背景图片文件数据失败，则去沙箱目录下获取背景图片数据
    30.   return this.loadFileFromPath(filePath);
    31. }
    
    32. private loadFileFromPath(filePath: string): ArrayBuffer {
    33.   try {
    34.     let stats = fs.statSync(filePath);
    35.     let file = fs.openSync(filePath, fs.OpenMode.READ_ONLY);
    36.     let buffer = new ArrayBuffer(stats.size);
    37.     fs.readSync(file.fd, buffer);
    38.     fs.closeSync(file);
    39.     return buffer;
    40.   } catch (err) {
    41.     hilog.error(0x0000, 'testTag', "mkdir failed with error message: ", err.message, ", error code: ", err.code);
    42.     return new ArrayBuffer(0);
    43.   }
    44. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/reader-setting-font "自定义字体")
# 修改翻页方式、字体大小及行间距

更新时间: 2025-12-16 16:38

当应用需要支持修改默认的翻页方式、字体大小、行间距时，开发者可通过[ReaderSetting](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/reader-read-core#section13615732174218)的flipMode、fontSize、lineHeight属性，实现对翻页方式、字体大小、行间距的实时修改。

## 接口说明

修改翻页方式、字体大小及行间距主要涉及1个接口，具体介绍如下表所示。

|接口名|描述|
|:--|:--|
|[setPageConfig](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/reader-read-core#section6297758718)(pageConfig: ReaderSetting): void|设置或者修改页面排版属性。|

## 开发准备

在修改翻页方式、字体大小及行间距之前，请先确保已经“[构建阅读器](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/reader-read-page)”。

## 开发步骤

1. 修改翻页方式。
    
    1. this.readerSetting.flipMode = '1'; // 0代表仿真翻页，1代表横滑翻页
    
2. 修改字体大小。
    
    1. this.readerSetting.fontSize = 20;
    
3. 修改行间距。
    
    1. this.readerSetting.lineHeight = 2;
    
4. 调用ReaderComponentController组件控制器的setPageConfig接口，重新渲染界面。
    
    1. this.readerComponentController.setPageConfig(this.readerSetting);
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/reader-setting-background "自定义页面背景")
# 适配深、浅色模式

更新时间: 2025-12-16 16:38

当应用需要根据设备的深、浅色模式变化动态切换主题时，开发者可通过UIAbility的onConfigurationUpdate回调判断模式的变化，然后设置模式对应的字体颜色及背景色。

## 接口说明

适配深、浅色主题主要涉及1个接口，具体介绍如下表所示。

|接口名|描述|
|:--|:--|
|[setPageConfig](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/reader-read-core#section6297758718)(pageConfig: ReaderSetting): void|设置或者修改页面排版属性。|

## 开发准备

在适配深、浅色主题之前，请先确保已经“[构建阅读器](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/reader-read-page)”。

## 开发步骤

1. 监听UIAbility的onConfigurationUpdate回调，并通过应用级变量的状态管理[AppStorage](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-appstorage)保存当前colorMode值。
    
    1. import { Configuration, UIAbility } from '@kit.AbilityKit';
    
    2. export default class EntryAbility extends UIAbility {
    
    3.   onConfigurationUpdate(newConfig: Configuration): void {
    4.     AppStorage.setOrCreate('colorMode', newConfig.colorMode);
    5.   }
    6. }
    
2. 阅读页通过[@StorageLink](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-appstorage#storagelink)装饰器监听colorMode字段的变化。如果颜色变化，则触发对应主题色的变更。
    
    1. import { ConfigurationConstant } from '@kit.AbilityKit';
    
    2. @StorageLink('colorMode') @Watch('colorModeChange') colorMode: ConfigurationConstant.ColorMode =
    3.   ConfigurationConstant.ColorMode.COLOR_MODE_NOT_SET;
    
    4. /**
    5.  * 系统深色模式变化，可以重新设置主题
    6.  */
    7. colorModeChange() {
    8.   if (this.colorMode === ConfigurationConstant.ColorMode.COLOR_MODE_DARK) {
    9.     this.readerSetting.nightMode = true;
    10.     this.readerSetting.fontColor = '#ffffff';
    11.     this.readerSetting.themeColor = '#202224';
    12.   } else {
    13.     this.readerSetting.nightMode = false;
    14.     this.readerSetting.fontColor = '#000000';
    15.     this.readerSetting.themeColor = '#FFFFFF';
    16.   }
    17.   this.readerComponentController.setPageConfig(this.readerSetting);
    18. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/reader-setting-other "修改翻页方式、字体大小及行间距")
# 监听文本缩放因子变化

更新时间: 2025-12-16 16:38

在[智慧多窗](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/multi-window-intro)等场景时，文本缩放因子[Display.scaledDensity](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-display#display)属性会发生变化。如果文本缩放因子的值与当前值不符，开发者需要更新[ReaderSetting](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/reader-read-core#section13615732174218)的scaledDensity属性，触发ReaderComponentController组件控制器的setPageConfig接口重新进行页面排版。

## 接口说明

监听文本缩放因子变化主要涉及1个接口，具体介绍如下表所示。

|接口名|描述|
|:--|:--|
|[setPageConfig](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/reader-read-core#section6297758718)(pageConfig: ReaderSetting): void|设置或者修改页面排版属性。|

## 开发准备

在监听文本缩放因子变化之前，请先确保已经'[构建阅读器](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/reader-read-page)'。

## 开发步骤

1. 导入相关模块。
    
    1. import { display } from '@kit.ArkUI';
    2. import { hilog } from '@kit.PerformanceAnalysisKit';
    
2. 通过[display.on](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-display#displayonaddremovechange)接口监听文本缩放因子的变化。
    
    在监听接口中比对系统值与当前值是否一致，如果不一致则通过应用级变量的状态管理[AppStorage](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-appstorage)将isDensityChange值设为true，并退出阅读页。
    
    1. @Entry
    2. @Component
    3. struct Reader {
    4.   private screenDensityCallBack: Callback<number> | null = null;
    
    5.   aboutToAppear(): void {
    6.     this.registerScreenDensityChange();
    7.     hilog.info(0x0000, 'testTag',
    8.       'aboutToAppear : current scaledDensity = ' + this.readerSetting.scaledDensity + ', change scaledDensity = ' +
    9.       display.getDefaultDisplaySync().scaledDensity);
    10.   }
    
    11.   /**
    12.    * 注册缩放文本缩放因子变化监听
    13.    */
    14.   registerScreenDensityChange() {
    15.     this.screenDensityCallBack = (data: number) => {
    16.       let displaySync = display.getDefaultDisplaySync();
    17.       let scaledDensity = displaySync.scaledDensity;
    18.       if (scaledDensity !== this.readerSetting.scaledDensity) {
    19.         AppStorage.setOrCreate('isDensityChange', true);
    20.         this.getUIContext().getRouter().back();
    21.       }
    22.     }
    23.     display.on('change', this.screenDensityCallBack);
    24.   }
    
    25.   aboutToDisappear(): void {
    26.     display.off('change', this.screenDensityCallBack);
    27.   }
    
    28.   build() {
    29.     // 需要开发者根据构建阅读器章节自行实现
    30.   }
    31. }
    
3. 在阅读页的上级页面通过[@StorageLink](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-appstorage#storagelink)装饰器监听isDensityChange字段的变化。
    
    当退出阅读页时，会触发上级Index页面的onPageShow生命周期回调。若检测到isDensityChange字段值变更，将执行重新进入阅读页的方法。
    
    开发者可参考[阅读进度通知](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/reader-progress)章节保存阅读进度，在进阅读页时将保存的进度信息传入到阅读页，在阅读页通过[startPlay](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/reader-read-core#section3667128165411)接口继续阅读。
    
    1. import { hilog } from '@kit.PerformanceAnalysisKit';
    
    2. @Entry
    3. @Component
    4. struct Index {
    5.   /**
    6.    * 系统字体缩放因子是否发生变化，如果变化需要重启阅读器
    7.    */
    8.   @StorageLink('isDensityChange') isDensityChange: boolean = false;
    
    9.   onPageShow(): void {
    10.     // 文本缩放因子变化需要重新打开书籍
    11.     if (this.isDensityChange) {
    12.       this.jumper();
    13.       AppStorage.setOrCreate('isDensityChange', false);
    14.     }
    15.   }
    
    16.   private jumper() {
    17.     this.getUIContext().getRouter().pushUrl({ url: "pages/Reader" }).catch(() => {
    18.       hilog.error(0x0000, 'testTag', 'pushUrl failed');
    19.     });
    20.   }
    
    21.   build() {
    22.     // 需要开发者根据业务需要自行实现
    23.   }
    24. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/reader-setting-color-mode "适配深、浅色模式")
# 手动触发翻页

更新时间: 2025-12-16 16:36

Reader Kit的交互能力已经集成了手指点击和触摸滑动翻页，如果开发者需要增加其它翻页场景时（如：耳机播控翻页），可使用手动翻页接口实现自定义翻页场景。

## 业务流程

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163638.06628601874301531596448263731169:50001231000000:2800:A89D81BC41C4F222FB607D8754EFAB8434335F901140CB64D60B5B6A97BC1EE7.png "点击放大")

## 接口说明

手动触发场景只涉及1个翻页接口，具体介绍如下表所示。

|接口名|描述|
|:--|:--|
|[flipPage](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/reader-read-core#section444911141952)(isNext: boolean): void|触发ReadPageComponent组件进行翻页。|

## 开发准备

在进行手动触发翻页之前，请先确保已经“[构建阅读器](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/reader-read-page)”。

## 开发步骤

1. 在调用翻页接口之前，需要应用先构建需要手动触发翻页的场景，如耳机播控场景等。
2. 当自定义翻页场景调用触发翻页时，调用flipPage接口即可实现翻页能力。
    
    1. let isNext: boolean = true; // true为下一页, false为上一页
    2. this.readerComponentController.flipPage(isNext);
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/reader-interaction "书籍内容交互")
# 阅读进度通知

更新时间: 2025-12-16 16:36

当页面展示时，会通过页面展示回调接口返回页面渲染信息。页面渲染信息提供用于阅读进度跳转的domPos及resourceIndex属性，开发者可将属性缓存到数据库当中，用于阅读进度的恢复。

## 接口说明

阅读进度通知涉及2个接口，具体介绍如下表所示。

|接口名|描述|
|:--|:--|
|[on('pageShow')](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/reader-read-core#section1657755491213)|注册章节内容分页展示结果回调。|
|[off('pageShow')](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/reader-read-core#section18368173691416)|注销章节内容分页展示结果回调，可在页面销毁时调用。|

## 开发准备

在进行阅读进度通知监听之前，请先确保已经“[构建阅读器](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/reader-read-page)”。

## 开发步骤

1. 通过ReaderComponentController组件控制器监听页面展示回调。
    
    当排版引擎渲染完页面后会回调on('pageShow')接口，将页面渲染信息进行返回。通过页面渲染信息的domPos及resourceIndex属性，可标识当前阅读进度。
    
    开发者可在on('pageShow')接口回调中将阅读进度实时保存到数据库当中，防止用户异常退出阅读器时的进度丢失。当用户下次继续阅读时，可将保存domPos及resourceIndex属性传入到[startPlay](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/reader-read-core#section3667128165411)接口中，用于阅读进度的恢复。
    
    1. aboutToAppear(): void {
    2.   this.setOnPageShowListener();
    3. }
    
    4. private async setOnPageShowListener(){
    5.   try {
    6.       this.readerComponentController.on('pageShow', (data: readerCore.PageDataInfo): void => {
    7.       // 开发者可在此保存内容分页排版数据，利用data.resourceIndex及data.startDomPos数据调用startPlay接口继续阅读
    8.       hilog.info(0x0000, 'testTag', 'pageshow: data is: ' + JSON.stringify(data));
    9.     });
    10.   } catch (err) {
    11.     hilog.error(0x0000, 'testTag', `failed to init, Code is ${err.code}, message is ${err.message}`);
    12.   }
    13. }
    
2. 页面销毁时，需要调用注销页面展示接口。
    
    1. aboutToDisappear(): void {
    2.   this.readerComponentController.off('pageShow');
    3. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/reader-flip-page "手动触发翻页")
