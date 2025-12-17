# ArkWeb简介

更新时间: 2025-12-16 16:38

## 使用场景

ArkWeb（方舟Web）提供了Web组件，用于在应用程序中显示Web页面内容。常见使用场景包括：

- 应用集成Web页面：应用可以在页面中使用Web组件，嵌入Web页面内容，以降低开发成本，提升开发、运营效率。
    
- 浏览器网页浏览场景：浏览器类应用可以使用Web组件，打开三方网页，使用无痕模式浏览Web页面，设置广告拦截等。
    
- 小程序：小程序类宿主应用可以使用Web组件，渲染小程序的页面，实现同层渲染，视频托管等小程序的功能。
    

## 能力范围

Web组件为开发者提供了丰富的控制Web页面能力。包括：

- Web页面加载：声明式加载Web页面和离屏加载Web页面等。
    
- 生命周期管理：组件生命周期状态变化，通知Web页面的加载状态变化等。
    
- 常用属性与事件：User-Agent管理、Cookie与存储管理、字体与深色模式管理、权限管理等。
    
- 与应用界面交互：自定义文本选择菜单、上下文菜单、文件上传界面等与应用界面交互能力。
    
- App通过JavaScriptProxy，与Web页面进行JavaScript交互。
    
- 安全与隐私：无痕浏览模式、广告拦截、坚盾守护模式等。
    
- 维测能力：[DevTools工具](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-debugging-with-devtools)调试能力，使用crashpad收集Web组件崩溃信息、定位与解决Web白屏问题、使用Hypium实现ArkWeb自动化测试。
    
- 其他高阶能力：与系统组件同层渲染、Web组件的网络托管、Web组件的媒体播放托管、Web组件输入框拉起自定义输入法、[网页接入密码保险箱](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkweb-access-password-safe)等。
    

## 需要权限

使用Web组件访问在线网页时需添加网络权限：ohos.permission.INTERNET，具体申请方式请参考[声明权限](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/declare-permissions)。

1. "requestPermissions":[
2.     {
3.       "name" : "ohos.permission.INTERNET"
4.     }
5.   ]

## 约束与限制

- 可依据ArkWeb内核版本在相关网站查询W3C标准的支持情况。例如：[https://developer.mozilla.org/en-US/](https://developer.mozilla.org/en-US/) 和 [https://webassembly.org/features/](https://webassembly.org/features/) 。
    
- Web内核版本：ArkWeb基于谷歌Chromium内核开发，系统版本与Chromium版本的对应关系如表格所示。
    
    |系统版本|Chromium版本|
    |:--|:--|
    |HarmonyOS 4.0及之前|M99|
    |HarmonyOS 4.1-5.1|M114|
    |HarmonyOS 6.0|M132（默认，推荐使用）<br><br>M114（可选，若应用需切换为此内核，请参考[M114内核在HarmonyOS6.0系统上的适配指导](https://gitcode.com/openharmony-tpc/chromium_src/blob/132_trunk/web/ReleaseNote/CompatibleWithLegacyWebEngine.md)）|
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkweb "ArkWeb（方舟Web）")
# ArkWeb进程

更新时间: 2025-12-16 16:38

ArkWeb是多进程模型，分为应用进程、Web渲染进程、Web GPU进程、Web孵化进程和Foundation进程。

说明

Web内核对内存大小的申请没有限制约束。

**图1** ArkWeb进程模型图

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163818.23241541612114263891869323904289:50001231000000:2800:BEE420C6CF192DB43CD0E7BBA41A24D50FB68EE967341ED454557A3E6A148425.png)

- 应用进程中Web相关线程（应用唯一）
    
    - 应用进程为主进程。包含网络线程、Video线程、Audio线程和IO线程等。
        
    - 负责Web组件的对外接口与回调处理，网络请求、媒体服务等需要与其他系统服务交互的功能。
        
- Foundation进程（系统唯一）
    
    负责接收应用进程进行孵化进程的请求，管理应用进程和Web渲染进程的绑定关系。
    
- Web孵化进程（系统唯一）
    
    - 负责接收Foundation进程的请求，执行孵化Web渲染进程与Web GPU进程。
        
    - 执行孵化后处理安全沙箱降权、预加载动态库，以提升性能。
        
- Web渲染进程（应用可指定多Web实例间共享或独立进程）
    
    - 负责运行Web渲染进程引擎（HTML解析、排版、绘制、渲染）。
        
    - 负责运行ArkWeb执行引擎（JavaScript、Web Assembly）。
        
    - 提供接口供应用选择多Web实例间是否共享渲染进程，满足不同场景对安全性、稳定性、内存占用的诉求。
        
    - 默认策略：移动设备上共享渲染进程以节省内存，2in1设备上独立渲染进程提升安全与稳定性。
        
- Web GPU进程（应用唯一）
    
    负责光栅化、合成送显等与GPU、RenderService交互功能。提升应用进程稳定性、安全性。
    

1. 可通过[setRenderProcessMode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#setrenderprocessmode12)设置渲染子进程的模式，从而控制渲染过程的单进程或多进程状态。
    
    移动设备默认为单进程渲染，而2in1设备则默认采用多进程渲染。通过调用[getRenderProcessMode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#getrenderprocessmode12)可查询当前的渲染子进程模式，其中枚举值0表示单进程模式，枚举值1对应多进程模式。若获取的值不在[RenderProcessMode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-e#renderprocessmode12)枚举值范围内，则系统将自动采用多进程渲染模式作为默认设置。
    
    1. // xxx.ets
    2. import { webview } from '@kit.ArkWeb';
    3. import { BusinessError } from '@kit.BasicServicesKit';
    
    4. @Entry
    5. @Component
    6. struct WebComponent {
    7.   controller: webview.WebviewController = new webview.WebviewController();
    
    8.   build() {
    9.     Column() {
    10.       Button('getRenderProcessMode')
    11.         .onClick(() => {
    12.           let mode = webview.WebviewController.getRenderProcessMode();
    13.           console.info("getRenderProcessMode: " + mode);
    14.         })
    15.       Button('setRenderProcessMode')
    16.         .onClick(() => {
    17.           try {
    18.             webview.WebviewController.setRenderProcessMode(webview.RenderProcessMode.MULTIPLE);
    19.           } catch (error) {
    20.             console.error(`ErrorCode: ${(error as BusinessError).code},  Message: ${(error as     BusinessError).message}`);
    21.           }
    22.         })
    23.       Web({ src: 'www.example.com', controller: this.controller })
    24.     }
    25.   }
    26. }
    
2. 可通过[terminateRenderProcess](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#terminaterenderprocess12)来主动关闭渲染进程。若渲染进程尚未启动或已销毁，此操作将不会产生任何影响。此外，销毁渲染进程将同时影响所有与之关联的其他实例。
    
    1. // xxx.ets
    2. import { webview } from '@kit.ArkWeb';
    
    3. @Entry
    4. @Component
    5. struct WebComponent {
    6.   controller: webview.WebviewController = new webview.WebviewController();
    
    7.   build() {
    8.     Column() {
    9.       Button('terminateRenderProcess')
    10.       .onClick(() => {
    11.         let result = this.controller.terminateRenderProcess();
    12.         console.info("terminateRenderProcess result: " + result);
    13.       })
    14.       Web({ src: 'www.example.com', controller: this.controller })
    15.     }
    16.   }
    17. }
    
3. 可通过[onRenderExited](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onrenderexited9)来监听渲染进程的退出事件，从而获知退出的具体原因（如内存OOM、crash或正常退出等）。由于多个Web组件可能共用同一个渲染进程，因此，每当渲染进程退出时，每个受此影响的Web组件均会触发相应的回调。
    
    1. // xxx.ets
    2. import { webview } from '@kit.ArkWeb';
    
    3. @Entry
    4. @Component
    5. struct WebComponent {
    6.   controller: webview.WebviewController = new webview.WebviewController();
    
    7.   build() {
    8.     Column() {
    9.       Web({ src: 'chrome://crash/', controller: this.controller })
    10.         .onRenderExited((event) => {
    11.           if (event) {
    12.             console.info('reason:' + event.renderExitReason);
    13.           }
    14.         })
    15.     }
    16.   }
    17. }
    
4. 可通过[onRenderProcessNotResponding](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onrenderprocessnotresponding12)、[onRenderProcessResponding](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onrenderprocessresponding12)来监听渲染进程的无响应状态。
    
    当Web组件无法处理输入事件，或未能在预期时间内导航至新URL时，系统会判定网页进程为无响应状态，并触发onRenderProcessNotResponding回调。在网页进程持续无响应期间，该回调可能反复触发，直至进程恢复至正常运行状态，此时将触发onRenderProcessResponding回调。
    
    1. // xxx.ets
    2. import { webview } from '@kit.ArkWeb';
    
    3. @Entry
    4. @Component
    5. struct WebComponent {
    6.   controller: webview.WebviewController = new webview.WebviewController();
    
    7.   build() {
    8.     Column() {
    9.       Web({ src: 'www.example.com', controller: this.controller })
    10.         .onRenderProcessNotResponding((data) => {
    11.           console.info("onRenderProcessNotResponding: [jsStack]= " + data.jsStack +
    12.             ", [process]=" + data.pid + ", [reason]=" + data.reason);
    13.         })
    14.     }
    15.   }
    16. }
    
    17. // xxx.ets
    18. import { webview } from '@kit.ArkWeb';
    
    19. @Entry
    20. @Component
    21. struct WebComponent {
    22.   controller: webview.WebviewController = new webview.WebviewController();
    
    23.   build() {
    24.     Column() {
    25.       Web({ src: 'www.example.com', controller: this.controller })
    26.         .onRenderProcessResponding(() => {
    27.           console.info("onRenderProcessResponding again");
    28.         })
    29.     }
    30.   }
    31. }
    
5. [Web组件](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web)创建参数涵盖了多进程模型的运用。其中，sharedRenderProcessToken标识了当前Web组件所指定的共享渲染进程的token。在多渲染进程模式下，拥有相同token的Web组件将优先尝试重用与该token绑定的渲染进程。token与渲染进程的绑定关系，在渲染进程的初始化阶段形成。一旦渲染进程不再关联任何Web组件，它与token的绑定关系将被解除。
    
    1. // xxx.ets
    2. import { webview } from '@kit.ArkWeb';
    
    3. @Entry
    4. @Component
    5. struct WebComponent {
    6.   controller1: webview.WebviewController = new webview.WebviewController();
    7.   controller2: webview.WebviewController = new webview.WebviewController();
    
    8.   build() {
    9.     Column() {
    10.       Web({ src: 'www.example.com', controller: this.controller1, sharedRenderProcessToken: "111" })
    11.       Web({ src: 'www.w3.org', controller: this.controller2, sharedRenderProcessToken: "111" })
    12.     }
    13.   }
    14. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-component-overview "ArkWeb简介")
# Web组件的生命周期

更新时间: 2025-12-16 16:38

## 概述

开发者可以使用Web组件加载本地或者在线网页。

Web组件提供生命周期回调接口，用于感知状态变化和处理业务。

Web组件的状态主要包括：Controller绑定到Web组件、网页加载开始、网页加载进度、网页加载结束、页面即将可见。

Web页面保活可以参考[使用离线Web组件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-offline-mode)。

自定义组件析构销毁时执行[aboutToDisappear](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-custom-component-lifecycle#abouttodisappear)函数，Web组件会被销毁，Web组件与WebviewController解绑，js运行环境也会一并销毁。

**图1** Web组件网页正常加载过程中的回调事件

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163819.00710641874244603976216248422918:50001231000000:2800:37AA940EEFD9AB96DEF1EF7229C8F56DE4BA81BB4EE24BC98D4DD9693F0E5F70.png)

## Web组件网页正常加载过程所涉及的状态说明

- [aboutToAppear](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-custom-component-lifecycle#abouttoappear)函数：在创建自定义组件的新实例后，在执行其build函数前执行。建议在此设置WebDebug调试模式、自定义协议URL的权限、Cookie等。
    
- [onControllerAttached](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#oncontrollerattached10)事件：当Controller成功绑定到Web组件时触发该回调，且禁止在该事件回调前调用Web组件相关的接口，否则会抛出js-error异常。建议在此事件中注入JS对象、设置自定义用户代理，使用操作网页不相关的接口。但因该回调调用时网页还未加载，因此无法在回调中使用有关操作网页的接口，例如[zoomIn](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#zoomin)、[zoomOut](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#zoomout)等。
    
- [onLoadIntercept](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onloadintercept10)事件：当Web组件加载url之前触发该回调，用于判断是否阻止此次访问。默认允许加载。
    
- [onInterceptRequest](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#oninterceptrequest9)事件：当Web组件加载url之前触发该回调，用于拦截url并返回响应数据。
    
- [onPageBegin](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onpagebegin)事件：网页开始加载时触发该回调，且只在主frame（表示一个用于展示HTML页面的元素）触发。如果是iframe或者frameset（用于包含frame的HTML标签）的内容加载时则不会触发此回调。多frame页面可能同时加载，主frame加载结束时子frame可能仍在加载。同一页面导航或失败的导航不会触发该回调。
    
- [onProgressChange](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onprogresschange)事件：告知开发者当前页面加载的进度。多frame页面或者子frame可能还在继续加载而主frame已经加载结束，所以在[onPageEnd](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onpageend)事件后仍可能收到该事件。
    
- [onPageEnd](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onpageend)事件：网页加载完成时触发该回调，且只在主frame触发。多frame页面有可能同时开始加载，即使主frame已经加载结束，子frame也有可能才开始或者继续加载中。同一页面导航或失败的导航不会触发该回调。建议在此回调中执行JavaScript脚本。注意，收到该回调不能保证下一帧反映DOM状态。
    

## Web组件网页异常加载过程所涉及的状态说明

- [onOverrideUrlLoading](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onoverrideurlloading12)事件：当URL将要加载到当前Web中时，让宿主应用程序有机会获得控制权，回调函数返回true将导致当前Web中止加载URL，而返回false则会导致Web继续照常加载URL。onLoadIntercept接口和onOverrideUrlLoading接口行为不一致，触发时机也不同，所以在应用场景上存在一定区别。onLoadIntercept事件在LoadUrl和iframe加载时触发，但onOverrideUrlLoading事件在LoadUrl和特定iframe加载时不会触发。
    
- [onPageVisible](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onpagevisible9)事件：Web回调事件。渲染流程中当HTTP响应的主体开始加载，新页面即将可见时触发该回调。此时文档加载还处于早期，因此链接的资源比如在线CSS、在线图片等可能尚不可用。
    
- [onRenderExited](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onrenderexited9)事件：应用渲染进程异常退出时触发该回调，可以在此回调中进行系统资源的释放、数据的保存等操作。如果应用希望异常恢复，需要调用[loadUrl](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#loadurl)接口重新加载页面。详细用法参考[应用如何避免Web组件渲染子进程异常退出导致的页面卡死问题](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-event-sequence#%E5%BA%94%E7%94%A8%E5%A6%82%E4%BD%95%E9%81%BF%E5%85%8Dweb%E7%BB%84%E4%BB%B6%E6%B8%B2%E6%9F%93%E5%AD%90%E8%BF%9B%E7%A8%8B%E5%BC%82%E5%B8%B8%E9%80%80%E5%87%BA%E5%AF%BC%E8%87%B4%E7%9A%84%E9%A1%B5%E9%9D%A2%E5%8D%A1%E6%AD%BB%E9%97%AE%E9%A2%98)。
    
- [onDisAppear](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-events-show-hide#ondisappear)事件：组件卸载消失时触发此回调。该事件在组件卸载时触发。
    

应用侧代码。

1. // xxx.ets
2. import { webview } from '@kit.ArkWeb';
3. import { BusinessError } from '@kit.BasicServicesKit';

4. @Entry
5. @Component
6. struct WebComponent {
7.   controller: webview.WebviewController = new webview.WebviewController();
8.   responseWeb: WebResourceResponse = new WebResourceResponse();
9.   heads: Header[] = new Array();
10.   @State webData: string = "<!DOCTYPE html>\n" +
11.     "<html>\n" +
12.     "<head>\n" +
13.     "<title>intercept test</title>\n" +
14.     "</head>\n" +
15.     "<body>\n" +
16.     "<h1>intercept test</h1>\n" +
17.     "</body>\n" +
18.     "</html>";

19.   aboutToAppear(): void {
20.     try {
21.       webview.WebviewController.setWebDebuggingAccess(true);
22.     } catch (error) {
23.       console.error(`ErrorCode: ${(error as BusinessError).code},  Message: ${(error as BusinessError).message}`);
24.     }
25.   }

26.   build() {
27.     Column() {
28.       Web({ src: 'www.example.com', controller: this.controller })
29.         .onControllerAttached(() => {
30.           // 推荐在此loadUrl、设置自定义用户代理、注入JS对象等
31.           console.info('onControllerAttached execute')
32.         })
33.         .onLoadIntercept((event) => {
34.           if (event) {
35.             console.info('onLoadIntercept url:' + event.data.getRequestUrl())
36.             console.info('url:' + event.data.getRequestUrl())
37.             console.info('isMainFrame:' + event.data.isMainFrame())
38.             console.info('isRedirect:' + event.data.isRedirect())
39.             console.info('isRequestGesture:' + event.data.isRequestGesture())
40.           }
41.           // 返回true表示阻止此次加载，否则允许此次加载
42.           return false;
43.         })
44.         .onOverrideUrlLoading((webResourceRequest: WebResourceRequest) => {
45.           if (webResourceRequest && webResourceRequest.getRequestUrl() == "about:blank") {
46.             return true;
47.           }
48.           return false;
49.         })
50.         .onInterceptRequest((event) => {
51.           if (event) {
52.             console.info('url:' + event.request.getRequestUrl());
53.           }
54.           let head1: Header = {
55.             headerKey: "Connection",
56.             headerValue: "keep-alive"
57.           }
58.           let head2: Header = {
59.             headerKey: "Cache-Control",
60.             headerValue: "no-cache"
61.           }
62.           // 将新元素追加到数组的末尾，并返回数组的新长度。
63.           let length = this.heads.push(head1);
64.           length = this.heads.push(head2);
65.           console.info('The response header result length is :' + length);
66.           this.responseWeb.setResponseHeader(this.heads);
67.           this.responseWeb.setResponseData(this.webData);
68.           this.responseWeb.setResponseEncoding('utf-8');
69.           this.responseWeb.setResponseMimeType('text/html');
70.           this.responseWeb.setResponseCode(200);
71.           this.responseWeb.setReasonMessage('OK');
72.           // 返回响应数据则按照响应数据加载，无响应数据则返回null表示按照原来的方式加载
73.           return this.responseWeb;
74.         })
75.         .onPageBegin((event) => {
76.           if (event) {
77.             console.info('onPageBegin url:' + event.url);
78.           }
79.         })
80.         .onFirstContentfulPaint(event => {
81.           if (event) {
82.             console.info("onFirstContentfulPaint:" + "[navigationStartTick]:" +
83.             event.navigationStartTick + ", [firstContentfulPaintMs]:" +
84.             event.firstContentfulPaintMs);
85.           }
86.         })
87.         .onProgressChange((event) => {
88.           if (event) {
89.             console.info('newProgress:' + event.newProgress);
90.           }
91.         })
92.         .onPageEnd((event) => {
93.           // 推荐在此事件中执行JavaScript脚本
94.           if (event) {
95.             console.info('onPageEnd url:' + event.url);
96.           }
97.         })
98.         .onPageVisible((event) => {
99.           console.info('onPageVisible url:' + event.url);
100.         })
101.         .onRenderExited((event) => {
102.           if (event) {
103.             console.info('onRenderExited reason:' + event.renderExitReason);
104.           }
105.         })
106.         .onDisAppear(() => {
107.           this.getUIContext().getPromptAction().showToast({
108.             message: 'The web is hidden',
109.             duration: 2000
110.           })
111.         })
112.     }
113.   }
114. }

## Web组件网页加载的性能指标

网页加载过程中需要关注一些重要的性能指标。例如，FCP(First Contentful Paint)首次内容绘制，FMP(First Meaningful Paint)首次有效绘制，LCP(Largest Contentful Paint)最大内容绘制等。Web组件提供了如下接口来通知开发者，接口仅支持在线非PDF网页，不支持本地网页和PDF网页。

- [onFirstContentfulPaint](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onfirstcontentfulpaint10)事件：网页首次内容绘制的回调函数。首次绘制文本、图像、非空白Canvas或SVG的时间点。
    
- [onFirstMeaningfulPaint](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onfirstmeaningfulpaint12)事件：网页绘制页面主要内容的回调函数。首次绘制主要内容的时间点。
    
- [onLargestContentfulPaint](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onlargestcontentfulpaint12)事件：网页绘制页面最大内容的回调函数。绘制可视区域内最大图片、文本块或视频的时间点。
    

## 应用如何避免Web组件渲染子进程异常退出导致的页面卡死问题

ArkWeb（方舟Web）是一个Web组件平台，旨在为应用程序提供展示Web页面内容的功能，并向开发者提供一系列的能力，如页面加载、交互和调试等功能。使用ArkWeb相关应用时，可能因各种原因（例如前端偶现异常导致ArkWeb渲染子进程崩溃，或是打开的应用较多，系统资源紧张导致后台ArkWeb渲染子进程被终止）而出现页面卡死的问题，这时需要重新打开页面或重启应用来解决。

在ArkWeb渲染子进程异常退出导致页面卡死后，应用可通过监听[onRenderExited](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onrenderexited9)事件来获取具体的退出原因[RenderExitReason](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-e#renderexitreason9)，并在异常回调中根据退出的具体原因，执行相应的异常处理。

**开发实践案例**

1. import { webview } from '@kit.ArkWeb';

2. @Entry
3. @Component
4. struct WebComponent {
5.   needReloadWhenVisible: boolean = false ;  // Web组件不可见时render退出后阻止重新加载页面，在可见时重新加载页面。
6.   webIsVisible: boolean = false;            // 判断Web组件是否可见。

7.   // 此处是将子进程异常崩溃和其它异常原因做了区分，应用开发者可根据实际业务特点，细化对应异常的处理策略。
8.   renderReloadMaxForCrashed: number = 5;    // 设置因为异常崩溃后重新加载的最大重试次数，应用可根据业务特点，自行设置试错上限。
9.   renderReloadCountForCrashed: number = 0;  // 异常崩溃后重新加载的次数。
10.   renderReloadMaxForOthers: number = 10;    // 设置因为其它异常原因退出的最大重试次数，应用可根据业务特点，自行设置试错上限。
11.   renderReloadCountForOthers: number = 0;   // 其它异常原因退出后重新加载的次数。

12.   // 创建Web组件。
13.   controller: webview.WebviewController = new webview.WebviewController();

14.   // 指定加载的页面。
15.   url: string = "www.example.com";
16.   build() {
17.     Column() {
18.       Web({ src: this.url, controller: this.controller })
19.         .onVisibleAreaChange([0, 1.0], (isVisible) => {
20.           this.webIsVisible = isVisible;
21.           if (isVisible && this.needReloadWhenVisible) { // Web组件可见时重新加载页面。
22.             this.needReloadWhenVisible = false;
23.             this.controller.loadUrl(this.url);
24.           }
25.         })
26.         // 应用监听渲染子进程异常退出回调，并进行异常处理。
27.         .onRenderExited((event) => {
28.           if (!event) {
29.             return;
30.           }
31.           if (event.renderExitReason == RenderExitReason.ProcessCrashed) {
32.             if (this.renderReloadCountForCrashed >= this.renderReloadMaxForCrashed) {
33.               // 设置重试次数上限保护，避免必现问题导致页面被循环加载。
34.               return;
35.             }
36.             console.info('renderReloadCountForCrashed: ' + this.renderReloadCountForCrashed);
37.             this.renderReloadCountForCrashed++;
38.           } else {
39.             if (this.renderReloadCountForOthers >= this.renderReloadMaxForOthers) {
40.               // 设置重试次数上限保护, 避免必现问题导致页面被循环加载。
41.               return;
42.             }
43.             console.info('renderReloadCountForOthers: ' + this.renderReloadCountForOthers);
44.             this.renderReloadCountForOthers++;
45.           }
46.           if (this.webIsVisible) {
47.             // Web组件可见则立即重新加载。
48.             this.controller.loadUrl(this.url);
49.             return;
50.           }
51.           // Web组件不可见时不立即重新加载。
52.           this.needReloadWhenVisible = true;
53.         })
54.     }
55.   }
56. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web_component_process "ArkWeb进程")
# User-Agent开发指导

更新时间: 2025-12-16 16:38

User-Agent（简称UA）是一个特殊的字符串，包含设备类型、操作系统及版本等关键信息。在Web开发中，这个字符串使服务器能够识别请求的来源设备及其特性，从而根据这些信息提供定制化的内容和服务。如果页面无法正确识别UA，可能会导致多种异常情况。例如，为移动设备优化的页面布局可能会在桌面设备上显示错乱，反之亦然。此外，某些特定的浏览器功能或CSS样式可能仅在特定的浏览器版本中受支持，如果页面无法根据UA字符串做出正确的判断，就可能导致渲染问题或逻辑错误。

## 默认User-Agent结构

- 默认User-Agent定义
    
    1. Mozilla/5.0 ({DeviceType}; {OSName} {OSVersion}) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/{ChromeCompatibleVersion}.0.0.0 Safari/537.36  ArkWeb/{ArkWeb VersionCode} {DeviceCompat} {扩展区}
    
- 举例说明
    
    1. Mozilla/5.0 (Phone; OpenHarmony 5.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/114.0.0.0 Safari/537.36  ArkWeb/4.1.6.1 Mobile
    
- 字段说明
    
    |字段|含义|
    |:--|:--|
    |DeviceType|当前的设备类型。<br><br>取值范围：<br><br>- Phone：[手机](https://developer.huawei.com/consumer/cn/doc/design-guides/phone-0000001776694632)设备<br><br>- Tablet：[平板](https://developer.huawei.com/consumer/cn/doc/design-guides/pad-0000001823654157)设备<br><br>- PC：[2in1](https://developer.huawei.com/consumer/cn/doc/design-guides/2in1-0000001777531700)设备|
    |OSName|基础[操作系统名称](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/glossary#section15569823194110)。<br><br>默认取值：OpenHarmony|
    |OSVersion|基础操作系统版本，两位数字，M.S。<br><br>通过系统参数const.ohos.fullname解析版本号得到，取版本号部分M.S前两位。<br><br>默认取值：例如5.0|
    |ChromeCompatibleVersion|兼容Chrome主版本的版本号，从114版本开始演进。<br><br>默认取值：114|
    |ArkWeb|HarmonyOS版本Web内核名称。<br><br>默认取值：ArkWeb|
    |ArkWeb VersionCode|ArkWeb版本号，格式a.b.c.d。<br><br>默认取值：例如4.1.6.1|
    |DeviceCompat|前向兼容字段。<br><br>默认取值：Mobile|
    |扩展区|三方应用可以扩展的字段。<br><br>三方应用使用ArkWeb组件时，可以做UA扩展，例如加入APP相关信息标识。|
    

说明

- 当前默认User-Agent的ArkWeb字段前有两个空格。
    
- 当前通过User-Agent中是否含有"Mobile"字段来判断是否开启前端HTML页面中meta标签的viewport属性。当User-Agent中不含有"Mobile"字段时，meta标签中viewport属性默认关闭，此时可通过显性设置[metaViewport](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#metaviewport12)属性为true来覆盖关闭状态。
    
- 建议通过OpenHarmony关键字识别是否是HarmonyOS设备，同时可以通过DeviceType识别设备类型用于不同设备上的页面显示（ArkWeb关键字表示设备使用的web内核，OpenHarmony关键字表示设备使用的操作系统，因此推荐通过OpenHarmony关键字识别是否是HarmonyOS设备）。
    
- {DistributionOSName}和{DistributionOSVersion}字段在API version 15之前的版本中未启用，从API version 15版本开始不在默认User-Agent中体现。
    

注意

为了确保兼容性，部分浏览器可能会在用户代理（User-Agent）中增加非HarmonyOS的操作系统名称。针对用户代理中同时包含“HarmonyOS”和非HarmonyOS操作系统名称的场景，建议网页将HarmonyOS的处理逻辑放置在其他操作系统处理逻辑之前。

## 自定义User-Agent结构

在下面的示例中，通过调用[getUserAgent()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#getuseragent)接口获取当前默认的用户代理（User-Agent）字符串。这一接口提供的默认User-Agent信息为开发者提供了基础，使开发者能够基于这个默认信息进行定制或扩展。

1. // xxx.ets
2. import { webview } from '@kit.ArkWeb';
3. import { BusinessError } from '@kit.BasicServicesKit';

4. @Entry
5. @Component
6. struct WebComponent {
7.   controller: webview.WebviewController = new webview.WebviewController();

8.   build() {
9.     Column() {
10.       Button('getUserAgent')
11.         .onClick(() => {
12.           try {
13.             let userAgent = this.controller.getUserAgent();
14.             console.log("userAgent: " + userAgent);
15.           } catch (error) {
16.             console.error(`ErrorCode: ${(error as BusinessError).code},  Message: ${(error as BusinessError).message}`);
17.           }
18.         })
19.       Web({ src: 'www.example.com', controller: this.controller })
20.     }
21.   }
22. }

以下示例通过[setCustomUserAgent()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#setcustomuseragent10)接口设置自定义用户代理，但请注意，此操作会覆盖系统的用户代理。因此，我们建议将扩展字段追加在默认用户代理的末尾，比如三方应用程序的开发场景，可以在系统默认用户代理字符串的末尾追加特定的APP标识，这样既能保留原有用户代理信息，又能增加自定义的应用识别信息。

当Web组件src设置了url时，建议在onControllerAttached回调事件中设置User-Agent，设置方式请参考示例。不建议将User-Agent设置在onLoadIntercept回调事件中，会概率性出现设置失败。如果未在onControllerAttached回调事件中设置User-Agent。再调用setCustomUserAgent方法时，可能会出现加载的页面与实际设置User-Agent不符的异常现象。

当Web组件src设置为空字符串时，建议先调用setCustomUserAgent方法设置User-Agent，再通过loadUrl加载具体页面。

1. // xxx.ets
2. import { webview } from '@kit.ArkWeb';
3. import { BusinessError } from '@kit.BasicServicesKit';

4. @Entry
5. @Component
6. struct WebComponent {
7.   controller: webview.WebviewController = new webview.WebviewController();
8.   // 三方应用相关信息标识
9.   @State customUserAgent: string = ' DemoApp';

10.   build() {
11.     Column() {
12.       Web({ src: 'www.example.com', controller: this.controller })
13.       .onControllerAttached(() => {
14.         console.log("onControllerAttached");
15.         try {
16.           let userAgent = this.controller.getUserAgent() + this.customUserAgent;
17.           this.controller.setCustomUserAgent(userAgent);
18.         } catch (error) {
19.           console.error(`ErrorCode: ${(error as BusinessError).code},  Message: ${(error as BusinessError).message}`);
20.         }
21.       })
22.     }
23.   }
24. }

从API version 20开始，可通过[setAppCustomUserAgent()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#setappcustomuseragent20)接口设置应用级自定义用户代理，或者通过[setUserAgentForHosts()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#setuseragentforhosts20)对特定网站设置应用级自定义用户代理，覆盖系统的用户代理，应用内所有Web组件生效。

建议在Web组件创建前先调用静态接口[getDefaultUserAgent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#getdefaultuseragent14)获取默认的用户代理（User-Agent）字符串，然后调用setAppCustomUserAgent，setUserAgentForHosts方法设置User-Agent，再创建指定src的Web组件或通过loadUrl加载具体页面。

1. // xxx.ets
2. import { webview } from '@kit.ArkWeb';
3. import { BusinessError } from '@kit.BasicServicesKit';

4. @Entry
5. @Component
6. struct WebComponent {
7.   controller: webview.WebviewController = new webview.WebviewController();

8.   aboutToAppear(): void {
9.     try {
10.       webview.WebviewController.initializeWebEngine();
11.       let defaultUserAgent = webview.WebviewController.getDefaultUserAgent();
12.       let appUA = defaultUserAgent + " appUA";
13.       webview.WebviewController.setAppCustomUserAgent(appUA);
14.       webview.WebviewController.setUserAgentForHosts(
15.         appUA,
16.         [
17.           "www.example.com",
18.           "www.baidu.com"
19.         ]
20.       );
21.     } catch (error) {
22.       console.error(`ErrorCode: ${(error as BusinessError).code},  Message: ${(error as BusinessError).message}`);
23.     }
24.   }

25.   build() {
26.     Column() {
27.       Web({ src: 'www.example.com', controller: this.controller })
28.     }
29.   }
30. }

在下面的示例中，通过[getCustomUserAgent()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#getcustomuseragent10)接口获取自定义用户代理。

1. // xxx.ets
2. import { webview } from '@kit.ArkWeb';
3. import { BusinessError } from '@kit.BasicServicesKit';

4. @Entry
5. @Component
6. struct WebComponent {
7.   controller: webview.WebviewController = new webview.WebviewController();
8.   @State userAgent: string = '';

9.   build() {
10.     Column() {
11.       Button('getCustomUserAgent')
12.         .onClick(() => {
13.           try {
14.             this.userAgent = this.controller.getCustomUserAgent();
15.             console.log("userAgent: " + this.userAgent);
16.           } catch (error) {
17.             console.error(`ErrorCode: ${(error as BusinessError).code},  Message: ${(error as BusinessError).message}`);
18.           }
19.         })
20.       Web({ src: 'www.example.com', controller: this.controller })
21.     }
22.   }
23. }

## 相关User-Agent接口优先级

|接口名称|优先级|说明|
|:--|:--|:--|
|setCustomUserAgent|最高|对调用的Web组件生效。|
|setUserAgentForHosts|低于setCustomUserAgent|对应用中所有Web组件访问指定网站生效。|
|setAppCustomUserAgent|低于setUserAgentForHosts|对应用中所有Web组件生效。|
|ArkWeb默认UA|最低|对应用中所有Web组件生效，只读，通过getDefaultUserAgent获取。|

## 常见问题

### 如何通过User-Agent来识别HarmonyOS操作系统中不同设备

HarmonyOS设备的识别主要通过User-Agent中的系统、系统版本和设备类型三个维度来判断。建议同时检查系统、系统版本和设备类型，以确保更准确的设备识别。

1. 系统识别
    
    通过User-Agent中的{OSName}字段识别HarmonyOS系统。
    
    1. const isHarmonyOS = () => /OpenHarmony/i.test(navigator.userAgent);
    
2. 系统版本识别
    
    通过User-Agent中的{OSName}和{OSVersion}字段识别HarmonyOS NEXT系统及系统版本。格式为：OpenHarmony + 版本号。
    
    1. // 检测是否是HarmonyOS NEXT系统
    2. const matches = navigator.userAgent.match(/OpenHarmony (\d+\.?\d*)/);
    3. matches?.length && Number(matches[1]) >= 5;
    
3. 设备类型识别
    
    通过deviceType字段来识别不同设备类型。
    
    1. // 检测是否为手机设备
    2. const isPhone = () => /Phone/i.test(navigator.userAgent);
    
    3. // 检测是否为平板设备
    4. const isTablet = () => /Tablet/i.test(navigator.userAgent);
    
    5. // 检测是否为2in1设备
    6. const is2in1 = () => /PC/i.test(navigator.userAgent);
    

### 如何模拟HarmonyOS操作系统的User-Agent进行前端调试

在Windows/Mac/Linux等操作系统中，可以通过Chrome/Edge/Firefox等浏览器DevTools提供的User-Agent复写能力，模拟HarmonyOS User-Agent。

### 如何在HarmonyOS中自定义User-Agent以实现H5兼容性

HarmonyOS提供[setCustomUserAgent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#setcustomuseragent10)接口以支持User-Agent的自定义设置。为适配移动端H5页面通常依赖的UA标识检测（如Mobile、HarmonyOS等），并确保不覆盖系统默认UA信息，推荐按如下方式操作：首先通过[getDefaultUserAgent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#getdefaultuseragent14)接口获取系统默认User-Agent字符串，随后将H5兼容所需的自定义标识字段追加至该字符串末尾，最后调用setCustomUserAgent接口设置修改后的完整UA字符串。

## 示例代码

- [Web用户代理](https://gitcode.com/harmonyos_samples/web-user-agent)

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-set-attributes-events "设置基本属性和事件")
# 管理Cookie及数据存储

更新时间: 2025-12-16 16:38

Cookie是服务端发送客户端的数据。客户端持有Cookie，便于服务端快速识别身份和状态。

当Cookie的SameSite属性未指定时，默认值为SameSite=Lax。这种设置下，Cookie仅在用户导航到其源站点时发送，不会在跨站请求中发送。

## Cookie管理

Web组件提供[WebCookieManager](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webcookiemanager)类来管理Cookie信息。Cookie信息存储在应用沙箱路径下/proc/{pid}/root/data/storage/el2/base/cache/web/Cookies的文件中。

下面以[configCookieSync()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webcookiemanager#configcookiesync11)接口为例，为“www.example.com”设置单个Cookie的值“value=test”。其他Cookie的相关功能及使用，请参考[WebCookieManager()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webcookiemanager)接口文档。

1. // xxx.ets
2. import { webview } from '@kit.ArkWeb';
3. import { BusinessError } from '@kit.BasicServicesKit';

4. @Entry
5. @Component
6. struct WebComponent {
7.   controller: webview.WebviewController = new webview.WebviewController();

8.   build() {
9.     Column() {
10.       Button('configCookieSync')
11.         .onClick(() => {
12.           try {
13.             webview.WebCookieManager.configCookieSync('https://www.example.com', 'value=test');
14.           } catch (error) {
15.             console.error(`ErrorCode: ${(error as BusinessError).code},  Message: ${(error as BusinessError).message}`);
16.           }
17.         })
18.       Web({ src: 'www.example.com', controller: this.controller })
19.     }
20.   }
21. }

说明

Cookie每30s周期性保存到磁盘中，也可以使用接口[saveCookieAsync](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webcookiemanager#savecookieasync)进行强制落盘（PC/2in1和Tablet设备不会持久化session cookie，即使调用saveCookieAsync，也不会将session cookie写入磁盘）。

## 缓存与存储管理

在访问网站时，网络资源请求通常需要较长的时间。开发者可以通过Cache和Dom Storage等手段将资源保存到本地，以提高访问同一网站的速度。

### Cache

使用[cacheMode()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#cachemode)配置页面资源的缓存模式，Web组件为开发者提供四种缓存模式，分别为：

- Default：优先使用未过期的缓存。如果缓存不存在，则从网络获取。
    
- None：加载资源使用缓存。如果缓存中无该资源，则从网络中获取。
    
- Online：加载资源不使用缓存。全部从网络中获取。
    
- Only：只从缓存中加载资源。
    

在下面的示例中，缓存设置为None模式。

1. // xxx.ets
2. import { webview } from '@kit.ArkWeb';

3. @Entry
4. @Component
5. struct WebComponent {
6.   @State mode: CacheMode = CacheMode.None;
7.   controller: webview.WebviewController = new webview.WebviewController();

8.   build() {
9.     Column() {
10.       Web({ src: 'www.example.com', controller: this.controller })
11.         .cacheMode(this.mode)
12.     }
13.   }
14. }

为了获取最新资源，开发者可以通过[removeCache()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#removecache)接口清除已经缓存的资源，示例代码如下：

1. // xxx.ets
2. import { webview } from '@kit.ArkWeb';
3. import { BusinessError } from '@kit.BasicServicesKit';

4. @Entry
5. @Component
6. struct WebComponent {
7.   @State mode: CacheMode = CacheMode.None;
8.   controller: webview.WebviewController = new webview.WebviewController();

9.   build() {
10.     Column() {
11.       Button('removeCache')
12.         .onClick(() => {
13.           try {
14.             // 设置为true时同时清除rom和ram中的缓存，设置为false时只清除ram中的缓存
15.             this.controller.removeCache(true);
16.           } catch (error) {
17.             console.error(`ErrorCode: ${(error as BusinessError).code},  Message: ${(error as BusinessError).message}`);
18.           }
19.         })
20.       Web({ src: 'www.example.com', controller: this.controller })
21.         .cacheMode(this.mode)
22.     }
23.   }
24. }

### Dom Storage

Dom Storage包含了Session Storage和Local Storage两类。Session Storage为临时数据，其存储与释放跟随会话生命周期；Local Storage为持久化数据，保存在应用目录下。两者的数据均通过Key-Value的形式存储，在访问需要客户端存储的页面时使用。开发者可以通过Web组件的属性接口[domStorageAccess()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#domstorageaccess)进行使能配置，示例如下：

1. // xxx.ets
2. import { webview } from '@kit.ArkWeb';

3. @Entry
4. @Component
5. struct WebComponent {
6.   controller: webview.WebviewController = new webview.WebviewController();

7.   build() {
8.     Column() {
9.       Web({ src: 'www.example.com', controller: this.controller })
10.         .domStorageAccess(true)
11.     }
12.   }
13. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-default-useragent "User-Agent开发指导")
# Web深色模式适配

更新时间: 2025-12-16 16:38

系统提供浅色和深色的主题模式供用户选择。深色模式在低光环境下能够降低屏幕亮度，减少光线刺激，改善阅读体验。Web组件根据网页样式进行渲染。若网页未适配深色模式，会造成与系统主题的割裂感。网页开发者应考虑用户的主题偏好，适配深色模式，以保证用户体验的一致性。

ArkWeb提供灵活控制Web组件深色模式的能力，支持独立于系统进行设置。此外，ArkWeb还可以强制不同网页适配深色模式，以兼容不同的系统主题。

## 网页深色模式适配

在网页开发过程中，可以使用color-scheme和prefers-color-scheme属性进行深色模式适配。

- color-scheme是一个CSS属性，用于表示网页支持的配色方案，可以影响表单、滚动条和CSS系统颜色。CSS系统颜色指Web组件内置的颜色，是部分元素未定义样式时应用的默认颜色。
    
    当声明支持深色配色方案时，Web组件可以将网页内的表单、滚动条以及使用CSS系统颜色的元素切换为深色样式。如果元素自定义了颜色样式，则不受color-scheme的影响，保持自定义的颜色样式。
    
    color-scheme未设置时，默认为normal，表示未指定配色方案，使用Web组件的默认配色方案，表现与light一致。使用样例如下：
    
    1. /* 使用方式1：使用meta标签全局设置 */
    2. <meta name="color-scheme" content="light"> /* 只支持浅色模式 */
    
    3. /* 使用方式2：使用style全局设置 */
    4. :root {
    5.   color-scheme: light dark; /* 支持浅色和深色模式，跟随系统切换 */
    6. }
    
    7. /* 使用方式3：使用style针对特定元素设置 */
    8. div {
    9.   color-scheme: light; /* 只支持浅色模式 */
    10. }
    
    例如，color-scheme.html页面在Web深色模式关闭和开启时的渲染效果如下图所示。关闭深色模式，网页采用浅色配色方案，input2应用自定义背景样式。开启深色模式，网页采用深色配色方案，input2保持自定义样式，而网页背景、字体、表单、进度条及按钮的颜色均自动切换为深色配色。
    
    11. <!-- color-scheme.html -->
    12. <!DOCTYPE html>
    13. <html>
    14. <head>
    15.     <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    16.     <meta name="color-scheme" content="light dark">
    17. </head>
    18. <body>
    19.   <h1>Example page</h1>
    20.   <input name="input1" type="text" placeholder="please enter text">
    21.   <br><br>
    22.   <input name="input2" type="text" placeholder="please enter text" style="background-color: Lightgray;">
    23.   <br><br>
    24.   <progress value="50" max="100"></progress>
    25.   <br><br>
    26.   <input type="checkbox">
    27.   <input type="checkbox" checked>
    28.   <br><br>
    29.   <button>submit</button>
    30. </body>
    31. </html>
    
    **图1** color-scheme效果图
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163839.80930968023683318212460127844124:50001231000000:2800:2A8B7750A4DF4224AAE7A8471BB4CF7C2DC1D3F4972BFAF580D783933BA6680F.png)
    
- prefers-color-scheme是CSS中的一个媒体查询功能，可以检测系统的主题颜色。网页开发者可以通过该特性，为不同的系统主题颜色定义不同的网页CSS样式，以适应用户的主题偏好。使用样例如下：
    
    1. <style>
    2.   /* 默认样式 */
    3.   body { background-color: White; }
    
    4.   /* 浅色样式，Web关闭深色模式时覆盖默认样式 */
    5.   @media (prefers-color-scheme: light) {
    6.     body { background-color: Gray; }
    7.   }
    
    8.   /* 深色样式，Web开启深色模式时覆盖默认样式 */
    9.   @media (prefers-color-scheme: dark) {
    10.     body { background-color: Black; }
    11.   }
    12. </style>
    
    color-scheme可声明网页配色方案，切换网页元素的默认样式。然而，其作用范围有限，使用prefers-color-scheme可以更灵活地定义网页深色模式。prefers-color-scheme可以结合color-scheme使用。
    
    例如，在color-scheme.html中增加以下样式定义。当Web深色模式开启时，网页将应用深色配色，并应用@media (prefers-color-scheme: dark)中定义的样式，渲染效果如图2所示。
    
    13. <style>
    14.   @media (prefers-color-scheme: dark) {
    15.     body { background-color: Gray; color: LightYellow; }
    16.     input { background-color: Lightgray; }
    17.   }
    18. </style>
    
    **图2** prefers-color-scheme效果图
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163839.40290663821205916991271127198792:50001231000000:2800:92A897A7B650D704FADF78175139EF8C709ABF42AC4A1D6054F383ED9C0BABAA.png)
    

## Web深色模式设置

通过[darkMode()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#darkmode9)接口可以配置Web深色模式，默认状态为关闭。应用可设置[WebDarkMode.Auto](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-e#webdarkmode9)，表示Web深色模式跟随系统设置。也可以手动设置[WebDarkMode.On](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-e#webdarkmode9)或[WebDarkMode.Off](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-e#webdarkmode9)来控制深色模式的开启与关闭。

设置[WebDarkMode.On](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-e#webdarkmode9)，或设置[WebDarkMode.Auto](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-e#webdarkmode9)并启用系统深色模式时，Web将进入深色模式。在深色模式下，Web会应用媒体查询@media(prefers-color-scheme: dark)中定义的深色样式。如果网页未定义深色样式，则保持原有样式。

若要使未适配深色模式的网页强制转换为深色样式，可以使用[forceDarkAccess()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#forcedarkaccess9)接口开启强制深色模式。强制深色模式可以覆盖网页默认样式，转换网页背景和文字的颜色，以适应在深色模式下显示。强制深色模式无法保证所有颜色转换符合预期。

在强制深色模式下，高亮度色值将被转换为适合低光环境的色值，低亮度色值则保持不变。具体色值转换算法沿用Chromium内核标准，随Chromium内核的更新迭代。色值转换只针对不支持深色配色方案的元素。如果网页全局声明支持深色配色方案，则整个网页的色值均不会被Web转换。

说明

若在@media(prefers-color-scheme: dark)中定义了元素的深色样式但未通过color-scheme声明支持深色配色方案，Web会在该深色样式的色值基础上进行转换，如表1所示。

**表1** 深色模式/强制深色模式/color-scheme三者关系

|深色模式|强制深色模式|color-scheme|预期结果|
|:--|:--|:--|:--|
|关闭|无影响|-|网页采用color-scheme支持的配色方案。|
|开启|关闭|-|网页采用color-scheme支持的配色方案，并应用@media(prefers-color-scheme: dark)中定义的样式。|
|开启|开启|支持深色|网页采用深色配色方案，并应用@media(prefers-color-scheme: dark)中定义的样式。|
|开启|开启|不支持深色|根据算法转换网页高亮元素色值。若网页在@media(prefers-color-scheme: dark)中定义了样式，则会在该样式色值上进行转换。|

[forceDarkAccess()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#forcedarkaccess9)接口仅在Web深色模式开启时生效。在下面的示例中，应用设置Web深色模式跟随系统。系统开启深色模式时，Web进入强制深色模式。

1. // xxx.ets
2. import { webview } from '@kit.ArkWeb';

3. @Entry
4. @Component
5. struct WebComponent {
6.   controller: webview.WebviewController = new webview.WebviewController();
7.   @State mode: WebDarkMode = WebDarkMode.Auto;
8.   @State access: boolean = true;

9.   build() {
10.     Column() {
11.       Web({ src: $rawfile('index.html'), controller: this.controller })
12.         .darkMode(this.mode)
13.         .forceDarkAccess(this.access)
14.     }
15.   }
16. }

index.html页面代码如下：

1. <!-- index.html -->
2. <!DOCTYPE html>
3. <html>
4. <head>
5.     <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
6.     <style type="text/css">
7.         body { background: LightBlue; color: Black; }
8.         @media (prefers-color-scheme: dark) {
9.             body { background: LightGray; color: Brown; }
10.         }
11.     </style>
12. </head>
13. <body class="contentCss">
14.   <p>Dark mode debug page</p>
15.   <input name="input1" placeholder="please enter text" style="color-scheme: light dark;">
16.   <br><br>
17.   <input name="input2" placeholder="please enter text">
18. </body>
19. </html>

index.html页面在深色模式关闭、深色模式开启及强制深色模式开启时的样式如图3所示。关闭深色模式，网页采用默认样式。开启深色模式，input1的配色方案切换为深色，网页应用@media(prefers-color-scheme: dark)中定义的灰色背景、棕色文字样式。开启强制深色模式，input1的配色方案为深色，未被Web转换，而网页背景色、文字颜色及input2背景色均依据(2)中色值转换为(3)所示。

**图3** Web深色模式和强制深色模式效果图

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163839.29336252177490870034158104506380:50001231000000:2800:7AB966D9B9FEAC71BAE190DE182F8F0BBB5766DF8229700E80CE32405DED576D.png)

## Web组件背景色适配

Web组件发生旋转或大小改变等事件时，Web网页尺寸改变，变化过程中可能会漏出Web组件的背景色。深色模式下，建议将Web组件背景色置为黑色，与网页背景保持一致，以提升用户体验。

Web组件背景色可通过[backgroundColor()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-background#backgroundcolor)设置。未设置背景色时，Web组件默认背景色为白色。仅当强制深色模式下，默认背景色变为黑色。未开启强制深色模式时，可通过以下方法进行适配。

- 应用侧设置[WebDarkMode.On](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-e#webdarkmode9)和[WebDarkMode.Off](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-e#webdarkmode9)控制深色模式开启和关闭时，背景色跟随深色模式开启和关闭状态改变。
    
    1. // xxx.ets
    2. import { webview } from '@kit.ArkWeb';
    
    3. @Entry
    4. @Component
    5. struct WebComponent {
    6.   controller: webview.WebviewController = new webview.WebviewController();
    7.   @State isDark: boolean = false;
    
    8.   build() {
    9.     Column() {
    10.       Web({ src: $rawfile('index.html'), controller: this.controller })
    11.         .darkMode(this.isDark ? WebDarkMode.On : WebDarkMode.Off)
    12.         .backgroundColor(this.isDark ? Color.Black : Color.White)
    13.     }
    14.   }
    15. }
    
- 应用侧设置[WebDarkMode.Auto](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-e#webdarkmode9)跟随系统深色模式时，监听系统设置，背景色跟随系统改变。
    
    1. // EntryAbility.ets
    2. export default class EntryAbility extends UIAbility {
    3.   onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void {
    4.     // 将当前colorMode放在AppStorage中
    5.     AppStorage.setOrCreate<ConfigurationConstant.ColorMode>('currentColorMode', this.context.config.colorMode);
    6.     hilog.info(0x0000, 'testTag', '%{public}s', 'Ability onCreate');
    7.   }
    
    8.   // ...
    
    9.   onConfigurationUpdate(newConfig: Configuration): void {
    10.     // 动态更新深浅色状态
    11.     const currentColorMode: ConfigurationConstant.ColorMode | undefined = AppStorage.get('currentColorMode');
    12.     if (currentColorMode !== newConfig.colorMode) {
    13.       AppStorage.setOrCreate<ConfigurationConstant.ColorMode>('currentColorMode', newConfig.colorMode);
    14.     }
    15.   }
    16. }
    
    17. // xxx.ets
    18. import { webview } from '@kit.ArkWeb';
    19. import { ConfigurationConstant } from '@kit.AbilityKit';
    
    20. @Entry
    21. @Component
    22. struct WebComponent {
    23.   controller: webview.WebviewController = new webview.WebviewController();
    24.   @State bgColor: Color = Color.White;
    25.   @StorageProp('currentColorMode') @Watch('onCurrentColorModeChange')
    26.   currentColorMode: ConfigurationConstant.ColorMode = ConfigurationConstant.ColorMode.COLOR_MODE_NOT_SET;
    
    27.   build() {
    28.     Column() {
    29.       Web({ src: $rawfile('index.html'), controller: this.controller })
    30.         .darkMode(WebDarkMode.Auto)
    31.         .backgroundColor(this.bgColor)
    32.     }
    33.   }
    
    34.   onCurrentColorModeChange(): void {
    35.     // 根据系统设置切换背景色
    36.     if (this.currentColorMode === ConfigurationConstant.ColorMode.COLOR_MODE_DARK) {
    37.       this.bgColor = Color.Black;
    38.     } else {
    39.       this.bgColor = Color.White;
    40.     }
    41.   }
    42. }
    

## 常见问题

### 网页未切换为深色样式

**问题现象**

网页未切换为深色样式。

**解决措施**

网页未切换为深色样式的原因有多种，可以按以下步骤排查：

1. 检查Web是否开启深色模式。Web深色模式接口[darkMode()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#darkmode9)默认状态为关闭，需显式声明为[WebDarkMode.On](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-e#webdarkmode9)或[WebDarkMode.Auto](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-e#webdarkmode9)，才能开启深色模式。
    
2. Web已开启深色模式时，检查网页是否定义深色样式。网页的深色样式需要网页开发者适配。如果未定义深色样式，即使Web开启深色模式，网页样式也会保持不变。若需强制适配，可以使用[forceDarkAccess()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#forcedarkaccess9)接口开启强制深色模式。
    
3. Web已开启强制深色模式时，检查网页是否声明支持深色配色方案。通过color-scheme声明支持深色配色方案的网页，在强制深色模式下色值不会被Web转换。同时，如果网页内元素自定义了颜色样式，则不会被color-scheme影响。因此表现为网页样式未切换为深色样式。此时，需要网页开发者进行适配修改。
    

### 强制深色模式开启后，网页样式异常

**问题现象**

强制深色模式开启，网页样式转换显示异常，例如字体显示不清、样式不美观或颜色转换不当等。

**解决措施**

强制深色模式下，Web使用Chromium色值转换算法自动调整元素颜色样式。不同网页的布局和样式写法各异，算法无法确保所有转换均符合预期。建议网页开发者自定义深色样式。

### 未开启深色模式，但Web网页背景变深

**问题现象**

Web组件未开启深色模式，但Web网页背景变深。

**解决措施**

Web网页未设置背景颜色，或者设置背景颜色透明时，会呈现Web组件的背景颜色。因此出现该问题时，可排查Web组件是否设置了深色的[backgroundColor()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-background#backgroundcolor)。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-cookie-and-data-storage-mgmt "管理Cookie及数据存储")
# 在新窗口中打开页面

更新时间: 2025-12-16 16:38

Web组件提供了在新窗口打开页面的能力，开发者可以通过[multiWindowAccess()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#multiwindowaccess9)接口来设置是否允许网页在新窗口打开。当有新窗口打开时，应用侧会在[onWindowNew()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onwindownew9)接口中收到Web组件新窗口事件。开发者需要在此接口事件中新建窗口来处理Web组件的窗口请求。

说明

- [allowWindowOpenMethod()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#allowwindowopenmethod10)接口设置为true时，前端页面通过JavaScript函数调用的方式打开新窗口。
    
- 当在Web页面调用window.open(url, name)打开新窗口时，ArkWeb内核会根据name查找是否存在已绑定的Web组件。若存在，该Web组件将收到[onActivateContent()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onactivatecontent20)接口通知，以便应用可将其展示至前台；若不存在，ArkWeb内核将通过onWindowNew()接口通知应用创建新窗口。
    
- 如果在onWindowNew()接口通知中创建了新窗口，并将ControllerHandler.setWebController()接口的参数设置为新Web组件的WebviewController，则ArkWeb内核会完成name与该新Web组件的绑定。
    
- 如果在onWindowNew()接口通知中没有创建新窗口，需要将ControllerHandler.setWebController()接口的参数设置为null。
    

在下面的本地示例中，当用户点击“新窗口中打开网页”按钮时，应用会在onWindowNew()接口收到Web组件的新窗口事件。

说明

- 网页要求用户创建新的窗口时触发回调[OnWindowNewEvent()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-i#onwindownewevent12)，该回调函数中isUserTrigger参数，true代表用户触发，false代表非用户触发。

- 应用侧代码。
    
    1. // xxx.ets
    2. import { webview } from '@kit.ArkWeb';
    
    3. // 在同一界面有两个Web组件。在WebComponent新开窗口时，会跳转到NewWebViewComp。
    4. @CustomDialog
    5. struct NewWebViewComp {
    6.   controller?: CustomDialogController;
    7.   webviewController1: webview.WebviewController = new webview.WebviewController();
    
    8.   build() {
    9.     Column() {
    10.       Web({ src: "", controller: this.webviewController1 })
    11.         .javaScriptAccess(true)
    12.         .multiWindowAccess(false)
    13.         .onWindowExit(() => {
    14.           console.info("NewWebViewComp onWindowExit");
    15.           if (this.controller) {
    16.             this.controller.close();
    17.           }
    18.         })
    19.         .onActivateContent(() => {
    20.           //该Web需要展示到前台，建议应用在这里进行tab或window切换的动作
    21.           console.log("NewWebViewComp onActivateContent")
    22.         })
    23.     }
    24.   }
    25. }
    
    26. @Entry
    27. @Component
    28. struct WebComponent {
    29.   controller: webview.WebviewController = new webview.WebviewController();
    30.   dialogController: CustomDialogController | null = null;
    
    31.   build() {
    32.     Column() {
    33.       Web({ src: $rawfile("window.html"), controller: this.controller })
    34.         .javaScriptAccess(true)
    35.           // 需要使能multiWindowAccess
    36.         .multiWindowAccess(true)
    37.         .allowWindowOpenMethod(true)
    38.         .onWindowNew((event) => {
    39.           if (this.dialogController) {
    40.             this.dialogController.close()
    41.           }
    42.           let popController: webview.WebviewController = new webview.WebviewController();
    43.           this.dialogController = new CustomDialogController({
    44.             builder: NewWebViewComp({ webviewController1: popController }),
    45.             // isModal设置为false，防止新窗口被销毁而无法触发onActivateContent回调
    46.             isModal: false
    47.           })
    48.           this.dialogController.open();
    49.           // 将新窗口对应WebviewController返回给Web内核。
    50.           // 若不调用event.handler.setWebController接口，会造成render进程阻塞。
    51.           // 如果没有创建新窗口，调用event.handler.setWebController接口时设置成null，通知Web没有创建新窗口。
    52.           event.handler.setWebController(popController);
    53.         })
    54.     }
    55.   }
    56. }
    
- window.html页面代码。
    
    1. <!DOCTYPE html>
    2. <html>
    3. <head>
    4.     <meta name="viewport" content="width=device-width"/>
    5.     <title>WindowEvent</title>
    6. </head>
    7. <body>
    8. <input type="button" value="新窗口中打开网页" onclick="OpenNewWindow()">
    9. <script type="text/javascript">
    10.     function OpenNewWindow()
    11.     {
    12.         var txt = '打开的窗口';
    13.         let openedWindow = window.open("about:blank", "", "location=no,status=no,scrollbars=no");
    14.         openedWindow.document.write("<p>" + "<br><br>" + txt + "</p>");
    15.         openedWindow.focus();
    16.     }
    17. </script>
    18. </body>
    19. </html>
    

**图1** 新窗口中打开页面效果图

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163844.21464257099889092833947332226433:50001231000000:2800:04098DF7D560255F7DD38D40B2D35F2400FA723CE72E8C375C02D0BCB8313E00.png)

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-set-dark-mode "Web深色模式适配")
# 管理位置权限

更新时间: 2025-12-16 16:38

从API version 9开始，支持Web组件的[GeolocationPermissions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-geolocationpermissions)类和[onGeolocationShow](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#ongeolocationshow)方法对网页进行位置权限管理。更多信息请参见[应用数据安全](https://developer.huawei.com/consumer/cn/doc/best-practices/bpta-app-data-security)。

Web组件根据[GeolocationPermissions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-geolocationpermissions)类和[onGeolocationShow](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#ongeolocationshow)方法的响应结果，决定是否赋予前端页面权限。用户可以获取位置信息，以便使用出行导航、天气预报等服务。

## 需要权限

使用获取位置功能，需在module.json5中配置位置权限。具体添加方法请参考[在配置文件中声明权限](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/declare-permissions#%E5%9C%A8%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6%E4%B8%AD%E5%A3%B0%E6%98%8E%E6%9D%83%E9%99%90)。

1. "requestPermissions":[
2.    {
3.      "name" : "ohos.permission.LOCATION" // 精准定位
4.    },
5.    {
6.      "name" : "ohos.permission.APPROXIMATELY_LOCATION" // 模糊定位
7.    },
8.    {
9.      "name" : "ohos.permission.LOCATION_IN_BACKGROUND" // 后台定位
10.    }
11.  ]

## 申请位置权限

在下面的示例中，用户点击前端页面"获取位置"按钮，Web组件通过弹窗通知应用侧位置权限请求消息。

- 前端页面代码。
    
    1. <!DOCTYPE html>
    2. <html lang="en">
    3. <head>
    4.     <meta charset="UTF-8">
    5.     <meta name="viewport" content="width=device-width, initial-scale=1.0">
    6.     <title>位置信息</title>
    7. </head>
    8. <body>
    9.     <p id="locationInfo">位置信息</p>
    10.     <button onclick="getLocation()">获取位置</button>
    
    11.     <script>
    12.         var locationInfo=document.getElementById("locationInfo");
    13.         function getLocation(){
    14.             if (navigator.geolocation) {
    15.                 // 访问设备地理位置
    16.                 navigator.geolocation.getCurrentPosition(showPosition);
    17.             }
    18.         }
    19.         function showPosition(position){
    20.             locationInfo.innerHTML="Latitude: " + position.coords.latitude + "<br />Longitude: " + position.coords.longitude;
    21.         }
    22.     </script>
    23. </body>
    24. </html>
    
- 应用代码。
    
    1. import { webview } from '@kit.ArkWeb';
    2. import { BusinessError } from '@kit.BasicServicesKit';
    3. import { abilityAccessCtrl, common } from '@kit.AbilityKit';
    
    4. let atManager = abilityAccessCtrl.createAtManager();
    
    5. @Entry
    6. @Component
    7. struct WebComponent {
    8.   controller: webview.WebviewController = new webview.WebviewController();
    9.   uiContext: UIContext = this.getUIContext();
    
    10.   // 组件的生命周期函数，创建组件实例后触发
    11.   aboutToAppear(): void {
    12.     let context : Context | undefined = this.uiContext.getHostContext() as common.UIAbilityContext;
    13.     if (!context) {
    14.       console.error("context is undefined");
    15.       return;
    16.     }
    17.     // 向用户请求位置权限，对整个应用生效
    18.     atManager.requestPermissionsFromUser(context, ["ohos.permission.APPROXIMATELY_LOCATION"]).then((data) => {
    19.       console.info('data:' + JSON.stringify(data));
    20.       console.info('data permissions:' + data.permissions);
    21.       console.info('data authResults:' + data.authResults);
    22.     }).catch((error: BusinessError) => {
    23.       console.error(`Failed to request permissions from user. Code is ${error.code}, message is ${error.message}`);
    24.     })
    25.   }
    
    26.   build() {
    27.     Column() {
    28.       // Web组件的geolocationAccess属性默认为true，可以显式配置为false以禁止Web组件获取地理位置信息
    29.       Web({ src: $rawfile('getLocation.html'), controller: this.controller })
    30.         .geolocationAccess(true)
    31.         .onGeolocationShow((event) => {
    32.           // 位置权限申请通知仅对当前Web组件生效，应用内的其他Web组件不受影响
    33.           this.uiContext.showAlertDialog({
    34.             title: '位置权限请求',
    35.             message: '是否允许获取位置信息',
    36.             primaryButton: {
    37.               value: 'cancel',
    38.               action: () => {
    39.                 if (event) {
    40.                   // 不允许此站点位置权限请求
    41.                   // 注意invoke的第3个参数表示是否记住当前选择，如果传true，则下次不再弹框
    42.                   event.geolocation.invoke(event.origin, false, false);
    43.                 }
    44.               }
    45.             },
    46.             secondaryButton: {
    47.               value: 'ok',
    48.               action: () => {
    49.                 if (event) {
    50.                   // 允许此站点位置权限请求
    51.                   // 注意invoke的第3个参数表示是否记住当前选择，如果传true，则下次不再弹框
    52.                   event.geolocation.invoke(event.origin, true, false);
    53.                 }
    54.               }
    55.             },
    56.             cancel: () => {
    57.               if (event) {
    58.                 // 不允许此站点位置权限请求
    59.                 // 注意invoke的第3个参数表示是否记住当前选择，如果传true，则下次不再弹框
    60.                 event.geolocation.invoke(event.origin, false, false);
    61.               }
    62.             }
    63.           })
    64.         })
    65.     }
    66.   }
    67. }
    

## 管理位置权限

通过Web组件的[GeolocationPermissions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-geolocationpermissions)类管理网页的位置权限，提供了新增（[allowgeolocation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-geolocationpermissions#allowgeolocation)）、查看（[getaccessiblegeolocation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-geolocationpermissions#getaccessiblegeolocation)）和删除（[deleteallgeolocation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-geolocationpermissions#deleteallgeolocation)）网页位置权限的方法。例如查看网页是否已申请位置权限、将网页已申请的位置权限删除。

1. import { webview } from '@kit.ArkWeb';
2. import { BusinessError } from '@kit.BasicServicesKit';

3. @Entry
4. @Component
5. struct WebComponent {
6.   controller: webview.WebviewController = new webview.WebviewController();
7.   origin: string = "www.example.com";

8.   build() {
9.     Column() {
10.       // 新增指定源的位置权限，再次获取位置信息时则不再触发onGeolocationShow的回调
11.       Button('allowGeolocation')
12.         .onClick(() => {
13.           try {
14.             webview.GeolocationPermissions.allowGeolocation(this.origin);
15.           } catch (error) {
16.             console.error(`ErrorCode: ${(error as BusinessError).code},  Message: ${(error as BusinessError).message}`);
17.           }
18.         })

19.       // 删除指定源的位置权限，再次获取位置信息时则触发onGeolocationShow的回调
20.       Button('deleteGeolocation')
21.         .onClick(() => {
22.           try {
23.             webview.GeolocationPermissions.deleteGeolocation(this.origin);
24.           } catch (error) {
25.             console.error(`ErrorCode: ${(error as BusinessError).code},  Message: ${(error as BusinessError).message}`);
26.           }
27.         })

28.       // 查询指定源的位置权限
29.       Button('getAccessibleGeolocation')
30.         .onClick(() => {
31.           try {
32.             webview.GeolocationPermissions.getAccessibleGeolocation(this.origin)
33.               .then(result => {
34.                 console.info('getAccessibleGeolocationPromise result: ' + result);
35.               }).catch((error: BusinessError) => {
36.               console.error(`getAccessibleGeolocationPromise error, ErrorCode: ${error.code},  Message: ${error.message}`);
37.             });
38.           } catch (error) {
39.             console.error(`ErrorCode: ${(error as BusinessError).code},  Message: ${(error as BusinessError).message}`);
40.           }
41.         })

42.       // 注意添加网络权限ohos.permission.INTERNET
43.       Web({ src: 'www.example.com', controller: this.controller })
44.     }
45.   }
46. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-open-in-new-window "在新窗口中打开页面")
# 使用隐私模式

更新时间: 2025-12-16 16:38

开发者在创建Web组件时，可以将可选参数[incognitoMode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-i#weboptions)设置为true，来开启Web组件的隐私模式。当使用隐私模式时，浏览网页时的Cookie、Cache Data等数据不会保存在本地的持久化文件，当隐私模式的Web组件被销毁时，Cookie、Cache Data等数据将不被记录下来。

- 创建隐私模式的[Web组件](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web)。
    
    1. // xxx.ets
    2. import { webview } from '@kit.ArkWeb';
    
    3. @Entry
    4. @Component
    5. struct WebComponent {
    6.  controller: webview.WebviewController = new webview.WebviewController();
    
    7.  build() {
    8.    Column() {
    9.      Web({ src: 'www.example.com', controller: this.controller, incognitoMode: true })
    10.    }
    11.  }
    12. }
    
- 通过[isIncognitoMode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#isincognitomode11) 判断当前Web组件是否是隐私模式。
    
    1. // xxx.ets
    2. import { webview } from '@kit.ArkWeb';
    3. import { BusinessError } from '@kit.BasicServicesKit';
    
    4. @Entry
    5. @Component
    6. struct WebComponent {
    7.   controller: webview.WebviewController = new webview.WebviewController();
    
    8.   build() {
    9.     Column() {
    10.       Button('isIncognitoMode')
    11.         .onClick(() => {
    12.           try {
    13.             let result = this.controller.isIncognitoMode();
    14.             console.info('isIncognitoMode' + result);
    15.           } catch (error) {
    16.             console.error(`ErrorCode: ${(error as BusinessError).code},  Message: ${(error as BusinessError).message}`);
    17.           }
    18.         })
    19.       Web({ src: 'www.example.com', controller: this.controller })
    20.     }
    21.   }
    22. }
    

隐私模式提供了一系列接口，用于操作地理位置、Cookie以及Cache Data。

- 通过[allowGeolocation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-geolocationpermissions#allowgeolocation)设置隐私模式下的Web组件允许指定来源使用地理位置。
    
    1. // xxx.ets
    2. import { webview } from '@kit.ArkWeb';
    3. import { BusinessError } from '@kit.BasicServicesKit';
    
    4. @Entry
    5. @Component
    6. struct WebComponent {
    7.   controller: webview.WebviewController = new webview.WebviewController();
    8.   origin: string = "file:///";
    
    9.   build() {
    10.     Column() {
    11.       Button('allowGeolocation')
    12.         .onClick(() => {
    13.           try {
    14.             // allowGeolocation第二个参数表示隐私模式（true）或非隐私模式（false）下，允许指定来源使用地理位置。
    15.             webview.GeolocationPermissions.allowGeolocation(this.origin, true);
    16.           } catch (error) {
    17.             console.error(`ErrorCode: ${(error as BusinessError).code},  Message: ${(error as BusinessError).message}`);
    18.           }
    19.         })
    20.       Web({ src: 'www.example.com', controller: this.controller, incognitoMode: true })
    21.     }
    22.   }
    23. }
    
- 通过[deleteGeolocation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-geolocationpermissions#deletegeolocation)清除隐私模式下指定来源的地理位置权限状态。
    
    1. // xxx.ets
    2. import { webview } from '@kit.ArkWeb';
    3. import { BusinessError } from '@kit.BasicServicesKit';
    
    4. @Entry
    5. @Component
    6. struct WebComponent {
    7.   controller: webview.WebviewController = new webview.WebviewController();
    8.   origin: string = "file:///";
    
    9.   build() {
    10.     Column() {
    11.       Button('deleteGeolocation')
    12.         .onClick(() => {
    13.           try {
    14.             // deleteGeolocation第二个参数表示隐私模式（true）或非隐私模式（false）下，清除指定来源的地理位置权限状态。
    15.             webview.GeolocationPermissions.deleteGeolocation(this.origin, true);
    16.           } catch (error) {
    17.             console.error(`ErrorCode: ${(error as BusinessError).code},  Message: ${(error as BusinessError).message}`);
    18.           }
    19.         })
    20.       Web({ src: 'www.example.com', controller: this.controller, incognitoMode: true })
    21.     }
    22.   }
    23. }
    
- 通过[getAccessibleGeolocation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-geolocationpermissions#getaccessiblegeolocation)以回调方式异步获取隐私模式下指定源的地理位置权限状态。
    
    1. // xxx.ets
    2. import { webview } from '@kit.ArkWeb';
    3. import { BusinessError } from '@kit.BasicServicesKit';
    
    4. @Entry
    5. @Component
    6. struct WebComponent {
    7.   controller: webview.WebviewController = new webview.WebviewController();
    8.   origin: string = "file:///";
    
    9.   build() {
    10.     Column() {
    11.       Button('getAccessibleGeolocation')
    12.         .onClick(() => {
    13.           try {
    14.             // getAccessibleGeolocation第三个参数表示隐私模式（true）或非隐私模式（false）下，以回调方式异步获取指定源的地理位置权限状态。
    15.             webview.GeolocationPermissions.getAccessibleGeolocation(this.origin, (error, result) => {
    16.               if (error) {
    17.                 console.error(`getAccessibleGeolocationAsync error: + Code: ${error.code}, message: ${error.message}`);
    18.                 return;
    19.               }
    20.               console.info('getAccessibleGeolocationAsync result: ' + result);
    21.             }, true);
    22.           } catch (error) {
    23.             console.error(`ErrorCode: ${(error as BusinessError).code},  Message: ${(error as BusinessError).message}`);
    24.           }
    25.         })
    26.       Web({ src: 'www.example.com', controller: this.controller, incognitoMode: true })
    27.     }
    28.   }
    29. }
    
- 通过[deleteAllData](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webstorage#deletealldata)清除隐私模式下Web SQL当前使用的所有存储。
    
    1. // xxx.ets
    2. import { webview } from '@kit.ArkWeb';
    3. import { BusinessError } from '@kit.BasicServicesKit';
    
    4. @Entry
    5. @Component
    6. struct WebComponent {
    7.   controller: webview.WebviewController = new webview.WebviewController();
    
    8.   build() {
    9.     Column() {
    10.       Button('deleteAllData')
    11.         .onClick(() => {
    12.           try {
    13.             // deleteAllData参数表示删除所有隐私模式（true）或非隐私模式（false）下，内存中的web数据。
    14.             webview.WebStorage.deleteAllData(true);
    15.           } catch (error) {
    16.             console.error(`ErrorCode: ${(error as BusinessError).code},  Message: ${(error as BusinessError).message}`);
    17.           }
    18.         })
    19.       Web({ src: $rawfile('index.html'), controller: this.controller, incognitoMode: true })
    20.         .databaseAccess(true)
    21.     }
    22.   }
    23. }
    
    加载的html文件。
    
    24. <!-- index.html -->
    25. <!DOCTYPE html>
    26. <html>
    27. <head>
    28.  <meta charset="UTF-8">
    29.  <title>test</title>
    30.  <script type="text/javascript">
    
    31.    var db = openDatabase('mydb','1.0','Test DB',2 * 1024 * 1024);
    32.    var msg;
    
    33.    db.transaction(function(tx){
    34.      tx.executeSql('INSERT INTO LOGS (id,log) VALUES(1,"test1")');
    35.      tx.executeSql('INSERT INTO LOGS (id,log) VALUES(2,"test2")');
    36.      msg = '<p>数据表已创建,且插入了两条数据。</p>';
    
    37.      document.querySelector('#status').innerHTML = msg;
    38.    });
    
    39.    db.transaction(function(tx){
    40.      tx.executeSql('SELECT * FROM LOGS', [], function (tx, results) {
    41.        var len = results.rows.length,i;
    42.        msg = "<p>查询记录条数：" + len + "</p>";
    
    43.        document.querySelector('#status').innerHTML += msg;
    
    44.            for(i = 0; i < len; i++){
    45.              msg = "<p><b>" + results.rows.item(i).log + "</b></p>";
    
    46.        document.querySelector('#status').innerHTML += msg;
    47.        }
    48.      },null);
    49.    });
    
    50.    </script>
    51. </head>
    52. <body>
    53. <div id="status" name="status">状态信息</div>
    54. </body>
    55. </html>
    
- 通过[fetchCookieSync](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webcookiemanager#fetchcookiesync11)获取隐私模式下指定url对应cookie的值。
    
    1. // xxx.ets
    2. import { webview } from '@kit.ArkWeb';
    3. import { BusinessError } from '@kit.BasicServicesKit';
    
    4. @Entry
    5. @Component
    6. struct WebComponent {
    7.   controller: webview.WebviewController = new webview.WebviewController();
    
    8.   build() {
    9.     Column() {
    10.       Button('fetchCookieSync')
    11.         .onClick(() => {
    12.           try {
    13.             // fetchCookieSync第二个参数表示获取隐私模式（true）或非隐私模式（false）下，webview的内存cookies。
    14.             let value = webview.WebCookieManager.fetchCookieSync('https://www.example.com', true);
    15.             console.info("fetchCookieSync cookie = " + value);
    16.           } catch (error) {
    17.             console.error(`ErrorCode: ${(error as BusinessError).code},  Message: ${(error as BusinessError).message}`);
    18.           }
    19.         })
    20.       Web({ src: 'www.example.com', controller: this.controller, incognitoMode: true })
    21.     }
    22.   }
    23. }
    
- 通过[configCookieSync](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webcookiemanager#configcookiesync11)设置隐私模式下指定url的单个cookie的值。
    
    1. // xxx.ets
    2. import { webview } from '@kit.ArkWeb';
    3. import { BusinessError } from '@kit.BasicServicesKit';
    
    4. @Entry
    5. @Component
    6. struct WebComponent {
    7.   controller: webview.WebviewController = new webview.WebviewController();
    
    8.   build() {
    9.     Column() {
    10.       Button('configCookieSync')
    11.         .onClick(() => {
    12.           try {
    13.             // configCookieSync第三个参数表示获取隐私模式（true）或非隐私模式（false）下，对应url的cookies。
    14.             webview.WebCookieManager.configCookieSync('https://www.example.com', 'a=b', true);
    15.           } catch (error) {
    16.             console.error(`ErrorCode: ${(error as BusinessError).code},  Message: ${(error as BusinessError).message}`);
    17.           }
    18.         })
    19.       Web({ src: 'www.example.com', controller: this.controller, incognitoMode: true })
    20.     }
    21.   }
    22. }
    
- 通过[existCookie](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webcookiemanager#existcookie)查询隐私模式下是否存在cookie。
    
    1. // xxx.ets
    2. import { webview } from '@kit.ArkWeb';
    
    3. @Entry
    4. @Component
    5. struct WebComponent {
    6.   controller: webview.WebviewController = new webview.WebviewController();
    
    7.   build() {
    8.     Column() {
    9.       Button('existCookie')
    10.         .onClick(() => {
    11.           // existCookie参数表示隐私模式（true）或非隐私模式（false）下，查询是否存在cookies。
    12.           let result = webview.WebCookieManager.existCookie(true);
    13.           console.info("result: " + result);
    14.         })
    15.       Web({ src: 'www.example.com', controller: this.controller, incognitoMode: true })
    16.     }
    17.   }
    18. }
    
- 通过[clearAllCookiesSync](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webcookiemanager#clearallcookiessync11)清除隐私模式下所有cookie。
    
    1. // xxx.ets
    2. import { webview } from '@kit.ArkWeb';
    
    3. @Entry
    4. @Component
    5. struct WebComponent {
    6.   controller: webview.WebviewController = new webview.WebviewController();
    
    7.   build() {
    8.     Column() {
    9.       Button('clearAllCookiesSync')
    10.         .onClick(() => {
    11.           // clearAllCookiesSync参数表示清除隐私模式（true）或非隐私模式（false）下，webview的所有内存cookies。
    12.           webview.WebCookieManager.clearAllCookiesSync(true);
    13.         })
    14.       Web({ src: 'www.example.com', controller: this.controller, incognitoMode: true })
    15.     }
    16.   }
    17. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-geolocation-permission "管理位置权限")
# 使用运动和方向传感器监测设备状态

更新时间: 2025-12-16 16:38

## 概述

运动和方向传感器，如加速度计、陀螺仪等，能够监测设备的运动状态和方向变化，例如设备的旋转、倾斜等。

通过W3C标准协议接口，Web组件能够访问这些传感器的数据，进而实现更加丰富的用户交互功能。例如，开发者在网页应用中可以利用加速度计识别运动模式，指导用户进行健身运动，利用陀螺仪捕获玩家手中设备的倾斜和旋转动作，实现无按钮操控的游戏体验。

通过在JavaScript中调用以下支持的W3C标准协议接口，可以访问运动和方向传感器。

|接口|名称|说明|
|:--|:--|:--|
|Accelerometer|加速度|可获取设备X、Y、Z轴方向的加速度数据。|
|Gyroscope|陀螺仪|可获取设备X、Y、Z轴方向的角速度数据。|
|AbsoluteOrientationSensor|绝对定位|可获取表示设备绝对定位方向的四元数，包含X、Y、Z和W分量。|
|RelativeOrientationSensor|相对定位|可获取表示设备相对定位方向的四元数，包含X、Y、Z和W分量。|
|DeviceMotionEvent|设备运动事件|通过监听该事件，可获取设备在X、Y、Z轴方向上的加速度数据，设备在X、Y、Z轴方向上包含重力的加速度数据，以及设备在alpha、beta、gamma轴方向上旋转的速率数据。|
|DeviceOrientationEvent|设备方向事件|通过监听该事件，可获取设备绕X、Y、Z轴的角度。|

## 需要权限

使用加速度、陀螺仪及设备运动事件接口时，需在配置文件module.json5中声明相应的传感器权限。具体配置方法请参考[在配置文件中声明权限](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/declare-permissions#%E5%9C%A8%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6%E4%B8%AD%E5%A3%B0%E6%98%8E%E6%9D%83%E9%99%90)。

1.     "requestPermissions":[
2.       {
3.         "name" : "ohos.permission.ACCELEROMETER" // 加速度权限
4.       },
5.       {
6.         "name" : "ohos.permission.GYROSCOPE"     // 陀螺仪权限
7.       }
8.     ]

Web组件在对接运动和方向传感器时，需配置[onPermissionRequest](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onpermissionrequest9)接口，通过该接口接收权限请求通知。

## 开发步骤

1. 应用侧代码中，Web组件配置[onPermissionRequest](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onpermissionrequest9)接口，可通过[PermissionRequest](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-permissionrequest)的[getAccessibleResource](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-permissionrequest#getaccessibleresource9)接口获取请求权限的资源类型，当资源类型为TYPE_SENSOR时，进行传感器授权处理。
    
    1. import { UIContext } from '@kit.ArkUI';
    2. import { webview } from '@kit.ArkWeb';
    3. import { abilityAccessCtrl, PermissionRequestResult } from '@kit.AbilityKit';
    4. import { BusinessError } from '@kit.BasicServicesKit';
    
    5. @Entry
    6. @Component
    7. struct WebComponent {
    8.   controller: webview.WebviewController = new webview.WebviewController();
    9.   uiContext: UIContext = this.getUIContext();
    
    10.   aboutToAppear() {
    11.     // 配置Web开启调试模式
    12.     webview.WebviewController.setWebDebuggingAccess(true);
    13.     // 访问控制管理, 获取访问控制模块对象。
    14.     let atManager = abilityAccessCtrl.createAtManager();
    15.     try {
    16.       atManager.requestPermissionsFromUser(this.uiContext.getHostContext(), ['ohos.permission.ACCELEROMETER', 'ohos.permission.GYROSCOPE']
    17.         , (err: BusinessError, data: PermissionRequestResult) => {
    18.         if (err) {
    19.           console.error(`requestPermissionsFromUser fail, err->${JSON.stringify(err)}`);
    20.         } else {
    21.           console.info('data permissions:' + data.permissions);
    22.           console.info('data authResults:' + data.authResults);
    23.         }
    24.       })
    25.     } catch (error) {
    26.       console.error(`ErrorCode: ${(error as BusinessError).code}, Message: ${(error as BusinessError).message}`);
    27.     }
    28.   }
    
    29.   build() {
    30.     Column() {
    31.       Web({ src: $rawfile('index.html'), controller: this.controller })
    32.         .onPermissionRequest((event) => {
    33.           if (event) {
    34.              this.uiContext.showAlertDialog({
    35.               title: 'title',
    36.               message: 'text',
    37.               primaryButton: {
    38.                 value: 'deny',
    39.                 action: () => {
    40.                   event.request.deny();
    41.                 }
    42.               },
    43.               secondaryButton: {
    44.                 value: 'onConfirm',
    45.                 action: () => {
    46.                   event.request.grant(event.request.getAccessibleResource());
    47.                 }
    48.               },
    49.               autoCancel: false,
    50.               cancel: () => {
    51.                 event.request.deny();
    52.               }
    53.             })
    54.           }
    55.         })
    56.     }
    57.   }
    58. }
    
2. 在前端页面代码中，利用JavaScript调用传感器相关的W3C标准协议接口。
    
    1. <!DOCTYPE HTML>
    2. <html>
    3. <head>
    4.     <meta charset="utf-8" />
    5.     <meta name="viewport" content="initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />
    6.     <meta name="msapplication-tap-highlight" content="no" />
    7.     <meta name="HandheldFriendly" content="true" />
    8.     <meta name="MobileOptimized" content="320" />
    9.     <title>运动和方向传感器</title>
    10.     <style>
    11.         body {
    12.             font-family: Arial, sans-serif;
    13.         }
    14.     </style>
    15.     <script type="text/javascript">
    16.         // 访问设备的加速度计传感器，并获取其数据。
    17.         function getAccelerometer() {
    18.             var acc = new Accelerometer({frequency: 60});
    19.             acc.addEventListener('activate', () => console.info('Ready to measure.'));
    20.             acc.addEventListener('error', error => console.info('Error type: ' + error.type + ', error: ' + error.error ));
    21.             acc.addEventListener('reading', () => {
    22.                 console.info(`Accelerometer ${acc.timestamp}, ${acc.x}, ${acc.y}, ${acc.z}.`);
    23.             });
    24.             acc.start();
    25.         }
    
    26.         // 访问设备的陀螺仪传感器，并获取其数据。
    27.         function getGyroscope() {
    28.             var gyr = new Gyroscope({frequency: 60});
    29.             gyr.addEventListener('activate', () => console.info('Ready to measure.'));
    30.             gyr.addEventListener('error', error => console.info('Error type: ' + error.type + ', error: ' + error.error ));
    31.             gyr.addEventListener('reading', () => {
    32.                 console.info(`Gyroscope ${gyr.timestamp}, ${gyr.x}, ${gyr.y}, ${gyr.z}.`);
    33.             });
    34.             gyr.start();
    35.         }
    
    36.         // 访问设备的方向传感器，并获取其数据。
    37.         function getAbsoluteOrientationSensor() {
    38.             var aos = new AbsoluteOrientationSensor({frequency: 60});
    39.             aos.addEventListener('activate', () => console.info('Ready to measure.'));
    40.             aos.addEventListener('error', error => console.info('Error type: ' + error.type + ', error: ' + error.error ));
    41.             aos.addEventListener('reading', () => {
    42.                 console.info(`AbsoluteOrientationSensor data: ${aos.timestamp}, ${aos.quaternion}`);
    43.             });
    44.             aos.start();
    45.         }
    
    46.         // 监听设备的运动事件，并执行相应的处理逻辑。
    47.         function listenDeviceMotionEvent() {
    48.             removeDeviceMotionEvent();
    49.             if ('DeviceMotionEvent' in window) {
    50.                 window.addEventListener('devicemotion', handleMotionEvent, false);
    51.             } else {
    52.               console.info('不支持DeviceMotionEvent');
    53.             }
    54.         }
    
    55.         // 移除之前添加的设备运动事件监听器。
    56.         function removeDeviceMotionEvent() {
    57.             if ('DeviceMotionEvent' in window) {
    58.               window.removeEventListener('devicemotion', handleMotionEvent, false);
    59.             } else {
    60.               console.info('不支持DeviceMotionEvent');
    61.             }
    62.         }
    
    63.         // 处理运动事件。
    64.         function handleMotionEvent(event) {
    65.             const x = event.accelerationIncludingGravity.x;
    66.             const y = event.accelerationIncludingGravity.y;
    67.             const z = event.accelerationIncludingGravity.z;
    68.             console.info(`DeviceMotionEvent data: ${event.timeStamp}, ${x}, ${y}, ${z}`);
    69.         }
    
    70.         // 监听设备方向的变化，并执行相应的处理逻辑。
    71.         function listenDeviceOrientationEvent() {
    72.             removeDeviceOrientationEvent();
    73.             if ('DeviceOrientationEvent' in window) {
    74.                 window.addEventListener('deviceorientation', handleOrientationEvent, false);
    75.             } else {
    76.                 console.info('不支持DeviceOrientationEvent');
    77.             }
    78.         }
    
    79.         // 移除之前添加的设备方向事件监听器。
    80.         function removeDeviceOrientationEvent() {
    81.             if ('DeviceOrientationEvent' in window) {
    82.               window.removeEventListener('deviceorientation', handleOrientationEvent, false);
    83.             } else {
    84.               console.info('不支持DeviceOrientationEvent');
    85.             }
    86.         }
    
    87.         // 监听设备方向的变化，并执行相应的处理逻辑。
    88.         function listenDeviceOrientationEvent2() {
    89.             removeDeviceOrientationEvent2();
    90.             if ('DeviceOrientationEvent' in window) {
    91.                 window.addEventListener('deviceorientationabsolute', handleOrientationEvent, false);
    92.             } else {
    93.                 console.info('不支持DeviceOrientationEvent');
    94.             }
    95.         }
    
    96.         // 移除之前添加的设备方向事件监听器。
    97.         function removeDeviceOrientationEvent2() {
    98.             if ('DeviceOrientationEvent' in window) {
    99.               window.removeEventListener('deviceorientationabsolute', handleOrientationEvent, false);
    100.             } else {
    101.               console.info('不支持DeviceOrientationEvent');
    102.             }
    103.         }
    
    104.         // 处理方向事件。
    105.         function handleOrientationEvent(event) {
    106.             console.info(`DeviceOrientationEvent data: ${event.timeStamp}, ${event.absolute}, ${event.alpha}, ${event.beta}, ${event.gamma}`);
    107.         }
    108.     </script>
    109. </head>
    110. <body>
    111. <div id="dcontent" class="dcontent">
    112.     <h3>运动和方向:</h3>
    113.     <ul class="dlist">
    114.         <li><button type="button" onclick="getAccelerometer()">加速度</button></li>
    115.         <li><button type="button" onclick="getGyroscope()">陀螺仪</button></li>
    116.         <li><button type="button" onclick="getAbsoluteOrientationSensor()">设备方向(绝对定位)</button></li>
    117.         <li><button type="button" onclick="listenDeviceMotionEvent()">设备运动事件</button></li>
    118.         <li><button type="button" onclick="listenDeviceOrientationEvent()">设备方向事件</button></li>
    119.         <li><button type="button" onclick="listenDeviceOrientationEvent2()">设备方向事件(绝对定位)</button></li>
    120.     </ul>
    121. </div>
    122. </body>
    123. </html>
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-incognito-mode "使用隐私模式")
# Web组件渲染模式

更新时间: 2025-12-16 16:38

Web组件提供了两种可配置的渲染模式，能够根据不同的容器大小进行适配，从而满足使用场景中对容器尺寸的需求。

## 异步渲染模式（默认）

异步渲染模式下（renderMode: [RenderMode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-e#rendermode12).ASYNC_RENDER），Web组件作为图形surface节点，独立送显。建议在仅由Web组件构成的应用页面中使用此模式，以提高性能并降低功耗。

- Web组件的宽高不能超过7,680px（物理像素），超过会导致白屏。
- 不支持动态切换模式。

开发者预期Web组件作为主体显示应用页面，如图一所示，在此场景下，Web组件高度正好为一屏或接近一屏（内嵌在navigation中）。加载的H5页面高度大于Web组件高度，Web内部将产生滚动条，用户可以通过在Web内部滑动来浏览H5页面的信息。只需使用Web组件即可实现应用业务主体内容，建议采用异步渲染模式以提升性能。

**图一 异步渲染模式场景**

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163827.05751976633199677627579576649614:50001231000000:2800:3DAFB4CD47BCAF28143226AD8CB4303A73FE02AEAF4D3C830F5C2F84933C19D9.png)

## 同步渲染模式

同步渲染模式下（renderMode: [RenderMode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-e#rendermode12).SYNC_RENDER），Web组件作为图形canvas节点，Web渲染跟随系统组件一起送显，可以渲染更长Web组件内容，但会增加性能消耗。

- 不支持DSS合成。
- 不支持动态切换模式。

开发者预期Web作为富文本显示的载体，成为应用页面的一部分，与其他ArkUI组件共同滑动交互。如图二所示，H5页面与Web组件高度一致，Web内部不生成滚动条，作为一个超长组件展示，通过Scroll组件实现应用内部的滚动，确保用户能够平滑浏览Web内容及其他ArkUI组件的内容。需要Web作为业务内容的一部分渲染超长组件，不允许Web内部生成滚动条，与其余ArkUI组件协同完成页面布局，建议采用同步渲染模式，支持超长页面的渲染。

**图二 同步渲染模式场景**

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163827.31988821380052647829857521945139:50001231000000:2800:2F1B24BAFE52562CEE934457AD2DD20C5F5CEC6A605876D6E9A413D2E7B3778F.png)

## 示例代码

1. // renderMode.ets
2. import { webview } from '@kit.ArkWeb';

3. @Entry
4. @Component
5. struct WebHeightPage {
6.   private webviewController: WebviewController = new webview.WebviewController()

7.   build() {
8.      Column() {
9.          Web({
10.              src: "https://www.example.com/",
11.              controller: this.webviewController,
12.              renderMode: RenderMode.ASYNC_RENDER // 设置渲染模式
13.          })
14.      }
15.   }
16. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-render-layout "Web渲染和布局")
# 优化跳转至新Web组件过程中的页面闪烁现象

更新时间: 2025-12-16 16:38

应用使用Navigation等路由策略导航至Web组件页面时，在网页加载过程中，页面底部可能出现闪烁现象，这会影响用户体验。

## 闪烁原因

使用Navigation等路由策略导航至Web组件页面时，通常根据网页的回调通知判断是否隐藏系统导航栏。若决定隐藏，Web组件布局会进行调整。这一布局调整过程可简化为如下四个阶段：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163839.54989753851903657116523479349651:50001231000000:2800:2339FA91EDA171275BD309DB915EA05360EC046F44D8AA78B2AA24CA6E03F16C.png)

图中四个状态的说明（从左至右）：

1. 将应用路由至Web页面，页面顶部为系统导航栏，底部是Web组件。在此情况下，网页能够正常加载。
    
2. 在网页加载过程中，系统会回调通知应用侧隐藏系统导航栏，以便切换至网页端的导航栏。此时系统导航栏被隐藏，Web组件的布局随即进行调整，页面底部最初会显露出Web组件的背景色（假设为灰色）。
    
3. 网页继续根据新的尺寸加载并显示，首先呈现的是HTML网页的背景色（假设为白色）。
    
4. 最后，网页内容完全加载，展现出完整的HTML网页内容。
    

在上述流程中，如果Web组件的背景色与网页背景色不同，跳转时可能会出现闪烁。闪烁的概率取决于网页的复杂度和网络状况。

## 优化方法

应用可以通过设置与网页背景色相同的Web组件的背景色，避免视觉闪烁，提升用户体验。例如，将Web组件的背景色设置为白色。

在类似情况下，如果Web组件的默认背景色为白色，而网页背景色为灰色，导航到新的Web页面时可能会出现白色闪烁。同理，将Web组件的背景色设置为灰色可以解决此问题。

以下为设置Web组件背景色的接口示例（示例中将Web组件背景色设置为灰色，若不设置，Web组件背景色默认为白色）：

1. Web({ src: $rawfile('xxx.html'),  controller: this.webController})
2.   .backgroundColor(Color.Gray)

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-fit-content "Web组件大小自适应页面内容布局")
# 获取网页内容高度

更新时间: 2025-12-16 16:38

通过调用[getPageHeight](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#getpageheight)可获取当前网页内容的实际高度，开发者可以根据具体需求选择合适的方法。

## 使用场景

在网页加载过程中，获取的高度可能不够精确，特别是在网页还未渲染完成时。因为动态内容加载后会更新这个值。网页内容可能需要长时间加载。现在网站为了优化首次加载速度，会使用动态网页加载技术，用户在看到网页首帧时，网页后台还在动态加载页面，特别是包含图片、动态内容的页面。

非静态网页不建议在[onPageEnd](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onpageend)、[onPageVisible](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onpagevisible9)、[onFirstContentfulPaint](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onfirstcontentfulpaint10)、[onFirstMeaningfulPaint](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onfirstmeaningfulpaint12)事件等Web组件生命周期回调和Web性能指标回调中获取。需要根据当前网页的特点，通过JSBridge或延迟等方案，在前端特定的回调通知里获取当前网页内容的实际高度。

## 普通静态展示页面

普通静态网页，可以在onPageEnd等Web组件生命周期回调和Web性能指标回调中通过getPageHeight获取网页内容的高度。

应用侧代码

1. // xxx.ets
2. import { webview } from '@kit.ArkWeb';

3. @Entry
4. @Component
5. struct Index {
6.   controller: webview.WebviewController = new webview.WebviewController();

7.   build() {
8.     Row() {
9.       Column() {
10.         Web({ src: $rawfile('index.html'), controller: this.controller })
11.           .onPageEnd(() => {
12.             console.info("page height: onPageEnd: " + this.controller.getPageHeight());
13.           })
14.       }
15.       .width('100%')
16.       .height('100%')
17.     }
18.     .height('100%')
19.   }
20. }

## 复杂动态网页使用JSBridge传递特定回调

动态网页可以通过JSBridge传递特定回调，通知到应用侧调用。

应用侧代码

1. // xxx.ets
2. import { webview } from '@kit.ArkWeb';

3. class TestClass {
4.   testController: webview.WebviewController;

5.   constructor(controller: webview.WebviewController) {
6.     this.testController = controller;
7.   }

8.   notifyToGet(): void {
9.     console.info("page height:" + this.testController.getPageHeight());
10.   }
11. }

12. @Entry
13. @Component
14. struct Index {
15.   controller: webview.WebviewController = new webview.WebviewController();
16.   @State jsbObj: TestClass = new TestClass(this.controller);

17.   build() {
18.     Row() {
19.       Column() {
20.         Web({ src: $rawfile('index.html'), controller: this.controller })
21.           .javaScriptAccess(true)
22.           .javaScriptProxy({
23.             object: this.jsbObj,
24.             name: "jsbObj",
25.             methodList: ["notifyToGet"],
26.             controller: this.controller
27.           })
28.       }
29.       .width('100%')
30.       .height('100%')
31.     }
32.     .height('100%')
33.   }
34. }

### 加载普通网页

普通网页可以通过load事件，在网页的所有资源都完全加载完成后触发。

前端代码

1. <!--index.html-->
2. <!DOCTYPE html>
3. <html lang="en">
4. <head>
5.     <meta charset="UTF-8">
6.     <title>Title</title>
7. </head>
8. <body>
9. <script>
10.     window.addEventListener("load", function() {
11.         if (typeof jsbObj !== 'undefined') {
12.             jsbObj.notifyToGet();
13.         } else {
14.             console.info("jsbObj is error");
15.         }
16.     })
17. </script>
18. </body>
19. </html>

### 加载大图片的网页

当网页含有大图片时，可使用图片加载完成回调触发。

在前端代码中，请替换图片为真实图片。

1. <!--index.html-->
2. <!DOCTYPE html>
3. <html lang="en">
4. <head>
5.     <meta charset="UTF-8">
6.     <title>Title</title>
7. </head>
8. <body>
9. <img src="example.jpg" id="largeImage" alt="Large Image">
10. <script>
11.     var img = document.getElementById('largeImage');

12.     img.addEventListener('load', function() {
13.         if (typeof jsbObj !== 'undefined') {
14.             jsbObj.notifyToGet();
15.         } else {
16.             console.info("jsbObj is error");
17.         }
18.     });
19. </script>
20. </body>
21. </html>

### 加载大量图片的网页

针对图片密集网页，在所有图片加载完成后触发。

在前端代码中，请替换图片为真实图片。

1. <!--index.html-->
2. <!DOCTYPE html>
3. <html lang="en">
4. <head>
5.     <meta charset="UTF-8">
6.     <title>Title</title>
7. </head>
8. <body>
9.     <img src="example1.jpg" >
10.     <img src="example2.jpg" >
11. <script>
12.     function waitForImages() {
13.         const images = Array.from(document.images);
14.         const promises = images.map(img => {
15.             if (img.complete) return Promise.resolve();
16.             return new Promise(resolve => {
17.                 img.onload = img.onerror = resolve;
18.             });
19.         });

20.         return Promise.all(promises).then(() => {
21.             if (typeof jsbObj !== 'undefined') {
22.                 jsbObj.notifyToGet();
23.             } else {
24.                 console.info("jsbObj is error");
25.             }
26.         })
27.     }
28.     document.addEventListener("DOMContentLoaded", waitForImages);
29. </script>
30. </body>
31. </html>

## 无法使用JSBridge场景

在无法使用JSBridge的场景下，可以通过添加setTimeout等函数来延迟获取当前页面的高度。具体的延迟时间可以根据网页的复杂度来确定。

应用侧代码

1. // xxx.ets
2. import { webview } from '@kit.ArkWeb';

3. @Entry
4. @Component
5. struct Index {
6.   controller: webview.WebviewController = new webview.WebviewController();

7.   build() {
8.     Row() {
9.       Column() {
10.         Web({ src: $rawfile('index.html'), controller: this.controller })
11.           .onPageEnd(() => {
12.             setTimeout(()=>{
13.                 console.info("page height: onPageEnd: setTimeout: " + this.controller.getPageHeight());
14.             },2000)
15.           })
16.       }
17.       .width('100%')
18.       .height('100%')
19.     }
20.     .height('100%')
21.   }
22. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-router-flash-optimization "优化跳转至新Web组件过程中的页面闪烁现象")
# 获取网页内容高度

更新时间: 2025-12-16 16:38

通过调用[getPageHeight](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#getpageheight)可获取当前网页内容的实际高度，开发者可以根据具体需求选择合适的方法。

## 使用场景

在网页加载过程中，获取的高度可能不够精确，特别是在网页还未渲染完成时。因为动态内容加载后会更新这个值。网页内容可能需要长时间加载。现在网站为了优化首次加载速度，会使用动态网页加载技术，用户在看到网页首帧时，网页后台还在动态加载页面，特别是包含图片、动态内容的页面。

非静态网页不建议在[onPageEnd](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onpageend)、[onPageVisible](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onpagevisible9)、[onFirstContentfulPaint](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onfirstcontentfulpaint10)、[onFirstMeaningfulPaint](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onfirstmeaningfulpaint12)事件等Web组件生命周期回调和Web性能指标回调中获取。需要根据当前网页的特点，通过JSBridge或延迟等方案，在前端特定的回调通知里获取当前网页内容的实际高度。

## 普通静态展示页面

普通静态网页，可以在onPageEnd等Web组件生命周期回调和Web性能指标回调中通过getPageHeight获取网页内容的高度。

应用侧代码

1. // xxx.ets
2. import { webview } from '@kit.ArkWeb';

3. @Entry
4. @Component
5. struct Index {
6.   controller: webview.WebviewController = new webview.WebviewController();

7.   build() {
8.     Row() {
9.       Column() {
10.         Web({ src: $rawfile('index.html'), controller: this.controller })
11.           .onPageEnd(() => {
12.             console.info("page height: onPageEnd: " + this.controller.getPageHeight());
13.           })
14.       }
15.       .width('100%')
16.       .height('100%')
17.     }
18.     .height('100%')
19.   }
20. }

## 复杂动态网页使用JSBridge传递特定回调

动态网页可以通过JSBridge传递特定回调，通知到应用侧调用。

应用侧代码

1. // xxx.ets
2. import { webview } from '@kit.ArkWeb';

3. class TestClass {
4.   testController: webview.WebviewController;

5.   constructor(controller: webview.WebviewController) {
6.     this.testController = controller;
7.   }

8.   notifyToGet(): void {
9.     console.info("page height:" + this.testController.getPageHeight());
10.   }
11. }

12. @Entry
13. @Component
14. struct Index {
15.   controller: webview.WebviewController = new webview.WebviewController();
16.   @State jsbObj: TestClass = new TestClass(this.controller);

17.   build() {
18.     Row() {
19.       Column() {
20.         Web({ src: $rawfile('index.html'), controller: this.controller })
21.           .javaScriptAccess(true)
22.           .javaScriptProxy({
23.             object: this.jsbObj,
24.             name: "jsbObj",
25.             methodList: ["notifyToGet"],
26.             controller: this.controller
27.           })
28.       }
29.       .width('100%')
30.       .height('100%')
31.     }
32.     .height('100%')
33.   }
34. }

### 加载普通网页

普通网页可以通过load事件，在网页的所有资源都完全加载完成后触发。

前端代码

1. <!--index.html-->
2. <!DOCTYPE html>
3. <html lang="en">
4. <head>
5.     <meta charset="UTF-8">
6.     <title>Title</title>
7. </head>
8. <body>
9. <script>
10.     window.addEventListener("load", function() {
11.         if (typeof jsbObj !== 'undefined') {
12.             jsbObj.notifyToGet();
13.         } else {
14.             console.info("jsbObj is error");
15.         }
16.     })
17. </script>
18. </body>
19. </html>

### 加载大图片的网页

当网页含有大图片时，可使用图片加载完成回调触发。

在前端代码中，请替换图片为真实图片。

1. <!--index.html-->
2. <!DOCTYPE html>
3. <html lang="en">
4. <head>
5.     <meta charset="UTF-8">
6.     <title>Title</title>
7. </head>
8. <body>
9. <img src="example.jpg" id="largeImage" alt="Large Image">
10. <script>
11.     var img = document.getElementById('largeImage');

12.     img.addEventListener('load', function() {
13.         if (typeof jsbObj !== 'undefined') {
14.             jsbObj.notifyToGet();
15.         } else {
16.             console.info("jsbObj is error");
17.         }
18.     });
19. </script>
20. </body>
21. </html>

### 加载大量图片的网页

针对图片密集网页，在所有图片加载完成后触发。

在前端代码中，请替换图片为真实图片。

1. <!--index.html-->
2. <!DOCTYPE html>
3. <html lang="en">
4. <head>
5.     <meta charset="UTF-8">
6.     <title>Title</title>
7. </head>
8. <body>
9.     <img src="example1.jpg" >
10.     <img src="example2.jpg" >
11. <script>
12.     function waitForImages() {
13.         const images = Array.from(document.images);
14.         const promises = images.map(img => {
15.             if (img.complete) return Promise.resolve();
16.             return new Promise(resolve => {
17.                 img.onload = img.onerror = resolve;
18.             });
19.         });

20.         return Promise.all(promises).then(() => {
21.             if (typeof jsbObj !== 'undefined') {
22.                 jsbObj.notifyToGet();
23.             } else {
24.                 console.info("jsbObj is error");
25.             }
26.         })
27.     }
28.     document.addEventListener("DOMContentLoaded", waitForImages);
29. </script>
30. </body>
31. </html>

## 无法使用JSBridge场景

在无法使用JSBridge的场景下，可以通过添加setTimeout等函数来延迟获取当前页面的高度。具体的延迟时间可以根据网页的复杂度来确定。

应用侧代码

1. // xxx.ets
2. import { webview } from '@kit.ArkWeb';

3. @Entry
4. @Component
5. struct Index {
6.   controller: webview.WebviewController = new webview.WebviewController();

7.   build() {
8.     Row() {
9.       Column() {
10.         Web({ src: $rawfile('index.html'), controller: this.controller })
11.           .onPageEnd(() => {
12.             setTimeout(()=>{
13.                 console.info("page height: onPageEnd: setTimeout: " + this.controller.getPageHeight());
14.             },2000)
15.           })
16.       }
17.       .width('100%')
18.       .height('100%')
19.     }
20.     .height('100%')
21.   }
22. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-router-flash-optimization "优化跳转至新Web组件过程中的页面闪烁现象")
# 应用侧调用前端页面函数

更新时间: 2025-12-16 16:38

应用侧可以通过[runJavaScript()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#runjavascript)和[runJavaScriptExt()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#runjavascriptext10)方法调用前端页面的JavaScript相关函数。

[runJavaScript()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#runjavascript)和[runJavaScriptExt()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#runjavascriptext10)在参数类型上有以下差异：[runJavaScriptExt()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#runjavascriptext10)支持string和ArrayBuffer类型参数，而[runJavaScript()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#runjavascript)仅支持string类型参数。

在下面的示例中，点击应用侧的“runJavaScript”按钮时，触发前端页面的htmlTest()方法。

- 前端页面代码。
    
    1. <!-- index.html -->
    2. <!DOCTYPE html>
    3. <html>
    4. <head>
    5.     <meta name="viewport" content="width=device-width, initial-scale=1.0">
    6. </head>
    7. <body>
    8. <button type="button" onclick="callArkTS()">Click Me!</button>
    9. <h1 id="text">这是一个测试信息，默认字体为黑色，调用runJavaScript方法后字体为黄色、调用runJavaScriptParam方法后字体为绿色、调用runJavaScriptCodePassed方法后字体为红色</h1>
    10. <script>
    11.     // 有参函数。
    12.     var param = "param: JavaScript Hello World!";
    13.     function htmlTestParam(param) {
    14.         document.getElementById('text').style.color = 'green';
    15.         console.log(param);
    16.     }
    17.     // 无参函数。
    18.     function htmlTest() {
    19.         document.getElementById('text').style.color = 'yellow';
    20.     }
    21.     // 点击“Click Me！”按钮，触发前端页面callArkTS()函数执行JavaScript传递的代码。
    22.     function callArkTS() {
    23.         changeColor();
    24.     }
    25. </script>
    26. </body>
    27. </html>
    
- 应用侧代码。
    
    1. // xxx.ets
    2. import { webview } from '@kit.ArkWeb';
    
    3. @Entry
    4. @Component
    5. struct WebComponent {
    6.   webviewController: webview.WebviewController = new webview.WebviewController();
    
    7.   aboutToAppear() {
    8.     // 配置Web开启调试模式
    9.     webview.WebviewController.setWebDebuggingAccess(true);
    10.   }
    
    11.   build() {
    12.     Column() {
    13.       Button('runJavaScriptParam')
    14.         .onClick(() => {
    15.           // 调用前端页面有参函数。
    16.           this.webviewController.runJavaScript('htmlTestParam(param)');
    17.         })
    18.       Button('runJavaScript')
    19.         .onClick(() => {
    20.           // 调用前端页面无参函数。
    21.           this.webviewController.runJavaScript('htmlTest()');
    22.         })
    23.       Button('runJavaScriptCodePassed')
    24.         .onClick(() => {
    25.           // 传递runJavaScript侧代码方法。
    26.           this.webviewController.runJavaScript(`function changeColor(){document.getElementById('text').style.color = 'red'}`);
    27.         })
    28.       Web({ src: $rawfile('index.html'), controller: this.webviewController })
    29.     }
    30.   }
    31. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-use-frontend-page-js "在应用中使用前端页面JavaScript")
# 建立应用侧与前端页面数据通道

更新时间: 2025-12-16 16:38

前端页面和应用侧之间可以用[createWebMessagePorts()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#createwebmessageports)接口创建消息端口来实现两端的通信。

在下面的示例中，应用侧页面中通过createWebMessagePorts方法创建两个消息端口，再把其中一个端口通过[postMessage()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#postmessage)接口发送到前端页面，便可以在前端页面和应用侧之间互相发送消息。端口使用完毕后或Webview对象销毁前通过[close](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webmessageport#close)接口关闭端口。

- 应用侧代码。
    
    1. // xxx.ets
    2. import { webview } from '@kit.ArkWeb';
    3. import { BusinessError } from '@kit.BasicServicesKit';
    
    4. @Entry
    5. @Component
    6. struct WebComponent {
    7.   controller: webview.WebviewController = new webview.WebviewController();
    8.   ports: webview.WebMessagePort[] = [];
    9.   @State sendFromEts: string = 'Send this message from ets to HTML';
    10.   @State receivedFromHtml: string = 'Display received message send from HTML';
    
    11.   build() {
    12.     Column() {
    13.       // 展示接收到的来自HTML的内容
    14.       Text(this.receivedFromHtml);
    15.       // 输入框的内容发送到HTML
    16.       TextInput({ placeholder: 'Send this message from ets to HTML' })
    17.         .onChange((value: string) => {
    18.           this.sendFromEts = value;
    19.         })
    
    20.       // 该内容可以放在onPageEnd生命周期中调用。
    21.       Button('postMessage')
    22.         .onClick(() => {
    23.           try {
    24.             // 1、创建两个消息端口。
    25.             this.ports = this.controller.createWebMessagePorts();
    26.             if (this.ports && this.ports[0] && this.ports[1]) {
    27.               // 2、在应用侧的消息端口(如端口1)上注册回调事件。
    28.               this.ports[1].onMessageEvent((result: webview.WebMessage) => {
    29.                 let msg = 'Got msg from HTML:';
    30.                 if (typeof (result) === 'string') {
    31.                   console.info(`received string message from html5, string is: ${result}`);
    32.                   msg = msg + result;
    33.                 } else if (typeof (result) === 'object') {
    34.                   if (result instanceof ArrayBuffer) {
    35.                     console.info(`received arraybuffer from html5, length is: ${result.byteLength}`);
    36.                     msg = msg + 'length is ' + result.byteLength;
    37.                   } else {
    38.                     console.info('not support');
    39.                   }
    40.                 } else {
    41.                   console.info('not support');
    42.                 }
    43.                 this.receivedFromHtml = msg;
    44.               })
    45.               // 3、将另一个消息端口(如端口0)发送到HTML侧，由HTML侧保存并使用。
    46.               this.controller.postMessage('__init_port__', [this.ports[0]], '*');
    47.             } else {
    48.               console.error(`ports is null, Please initialize first`);
    49.             }
    50.           } catch (error) {
    51.             console.error(`ErrorCode: ${(error as BusinessError).code},  Message: ${(error as BusinessError).message}`);
    52.           }
    53.         })
    
    54.       // 4、使用应用侧的端口给另一个已经发送到html的端口发送消息。
    55.       Button('SendDataToHTML')
    56.         .onClick(() => {
    57.           try {
    58.             if (this.ports && this.ports[1]) {
    59.               this.ports[1].postMessageEvent(this.sendFromEts);
    60.             } else {
    61.               console.error(`ports is null, Please initialize first`);
    62.             }
    63.           } catch (error) {
    64.             console.error(`ErrorCode: ${(error as BusinessError).code},  Message: ${(error as BusinessError).message}`);
    65.           }
    66.         })
    
    67.       // 5、关闭端口。
    68.       Button('closePort')
    69.       .onClick(() => {
    70.         try {
    71.           if (this.ports && this.ports.length == 2) {
    72.             this.ports[0].close();
    73.             this.ports = [];
    74.           } else {
    75.             console.error("ports is null, not need close");
    76.           }
    77.         } catch (error) {
    78.           console.error(`ErrorCode: ${(error as BusinessError).code},  Message: ${(error as BusinessError).message}`);
    79.         }
    80.       })
    81.       Web({ src: $rawfile('index.html'), controller: this.controller })
    82.     }
    83.   }
    84. }
    
- 前端页面代码。
    
    1. <!--index.html-->
    2. <!DOCTYPE html>
    3. <html>
    4. <head>
    5.     <meta name="viewport" content="width=device-width, initial-scale=1.0">
    6.     <title>WebView Message Port Demo</title>
    7. </head>
    8. <body>
    9.     <h1>WebView Message Port Demo</h1>
    10.     <div>
    11.         <input type="button" value="SendToEts" onclick="PostMsgToEts(msgFromJS.value);"/><br/>
    12.         <input id="msgFromJS" type="text" value="send this message from HTML to ets"/><br/>
    13.     </div>
    14.     <p class="output">display received message send from ets</p>
    15. </body>
    16. <script>
    17. var h5Port;
    18. var output = document.querySelector('.output');
    19. window.addEventListener('message', function (event) {
    20.     if (event.data === '__init_port__') {
    21.         if (event.ports[0] !== null) {
    22.             h5Port = event.ports[0]; // 1. 保存从应用侧发送过来的端口。
    23.             h5Port.onmessage = function (event) {
    24.               // 2. 接收ets侧发送过来的消息。
    25.               var msg = 'Got message from ets:';
    26.               var result = event.data;
    27.               if (typeof(result) === 'string') {
    28.                 console.info(`received string message from ets, string is: ${result}`);
    29.                 msg = msg + result;
    30.               } else if (typeof(result) === 'object') {
    31.                 if (result instanceof ArrayBuffer) {
    32.                   console.info(`received arraybuffer from ets, length is: ${result.byteLength}`);
    33.                   msg = msg + 'length is ' + result.byteLength;
    34.                 } else {
    35.                   console.info('not support');
    36.                 }
    37.               } else {
    38.                 console.info('not support');
    39.               }
    40.               output.innerHTML = msg;
    41.             }
    42.         }
    43.     }
    44. })
    
    45. // 3. 使用h5Port向应用侧发送消息。
    46. function PostMsgToEts(data) {
    47.     if (h5Port) {
    48.       h5Port.postMessage(data);
    49.     } else {
    50.       console.error('h5Port is null, Please initialize first');
    51.     }
    52. }
    53. </script>
    54. </html>
    

## 常见问题

### 为什么H5向应用侧发送消息接收不到？

检查传递的数据类型是否正确，WebMessage支持的数据类型有string和ArrayBuffer。

如果想要传递对象类型则需要将对象类型通过JSON.stringify方法转换为string类型再进行传递。示例如下：

1.   function PostMsgToEts(data) {
2.       if (h5Port) {
3.         let obj = {name:'exampleName',id:10}
4.         h5Port.postMessage(JSON.stringify(obj));
5.       } else {
6.         console.error('h5Port is null. Please initialize it first.');
7.       }
8.   }

### onControllerAttached与javaScriptOnDocumentStart的执行顺序是什么？

[javaScriptOnDocumentStart](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#javascriptondocumentstart11)在[onControllerAttached](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#oncontrollerattached10)之后执行。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-in-page-app-function-invoking "前端页面调用应用侧函数")
# 建立应用侧与前端页面数据通道

更新时间: 2025-12-16 16:38

前端页面和应用侧之间可以用[createWebMessagePorts()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#createwebmessageports)接口创建消息端口来实现两端的通信。

在下面的示例中，应用侧页面中通过createWebMessagePorts方法创建两个消息端口，再把其中一个端口通过[postMessage()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#postmessage)接口发送到前端页面，便可以在前端页面和应用侧之间互相发送消息。端口使用完毕后或Webview对象销毁前通过[close](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webmessageport#close)接口关闭端口。

- 应用侧代码。
    
    1. // xxx.ets
    2. import { webview } from '@kit.ArkWeb';
    3. import { BusinessError } from '@kit.BasicServicesKit';
    
    4. @Entry
    5. @Component
    6. struct WebComponent {
    7.   controller: webview.WebviewController = new webview.WebviewController();
    8.   ports: webview.WebMessagePort[] = [];
    9.   @State sendFromEts: string = 'Send this message from ets to HTML';
    10.   @State receivedFromHtml: string = 'Display received message send from HTML';
    
    11.   build() {
    12.     Column() {
    13.       // 展示接收到的来自HTML的内容
    14.       Text(this.receivedFromHtml);
    15.       // 输入框的内容发送到HTML
    16.       TextInput({ placeholder: 'Send this message from ets to HTML' })
    17.         .onChange((value: string) => {
    18.           this.sendFromEts = value;
    19.         })
    
    20.       // 该内容可以放在onPageEnd生命周期中调用。
    21.       Button('postMessage')
    22.         .onClick(() => {
    23.           try {
    24.             // 1、创建两个消息端口。
    25.             this.ports = this.controller.createWebMessagePorts();
    26.             if (this.ports && this.ports[0] && this.ports[1]) {
    27.               // 2、在应用侧的消息端口(如端口1)上注册回调事件。
    28.               this.ports[1].onMessageEvent((result: webview.WebMessage) => {
    29.                 let msg = 'Got msg from HTML:';
    30.                 if (typeof (result) === 'string') {
    31.                   console.info(`received string message from html5, string is: ${result}`);
    32.                   msg = msg + result;
    33.                 } else if (typeof (result) === 'object') {
    34.                   if (result instanceof ArrayBuffer) {
    35.                     console.info(`received arraybuffer from html5, length is: ${result.byteLength}`);
    36.                     msg = msg + 'length is ' + result.byteLength;
    37.                   } else {
    38.                     console.info('not support');
    39.                   }
    40.                 } else {
    41.                   console.info('not support');
    42.                 }
    43.                 this.receivedFromHtml = msg;
    44.               })
    45.               // 3、将另一个消息端口(如端口0)发送到HTML侧，由HTML侧保存并使用。
    46.               this.controller.postMessage('__init_port__', [this.ports[0]], '*');
    47.             } else {
    48.               console.error(`ports is null, Please initialize first`);
    49.             }
    50.           } catch (error) {
    51.             console.error(`ErrorCode: ${(error as BusinessError).code},  Message: ${(error as BusinessError).message}`);
    52.           }
    53.         })
    
    54.       // 4、使用应用侧的端口给另一个已经发送到html的端口发送消息。
    55.       Button('SendDataToHTML')
    56.         .onClick(() => {
    57.           try {
    58.             if (this.ports && this.ports[1]) {
    59.               this.ports[1].postMessageEvent(this.sendFromEts);
    60.             } else {
    61.               console.error(`ports is null, Please initialize first`);
    62.             }
    63.           } catch (error) {
    64.             console.error(`ErrorCode: ${(error as BusinessError).code},  Message: ${(error as BusinessError).message}`);
    65.           }
    66.         })
    
    67.       // 5、关闭端口。
    68.       Button('closePort')
    69.       .onClick(() => {
    70.         try {
    71.           if (this.ports && this.ports.length == 2) {
    72.             this.ports[0].close();
    73.             this.ports = [];
    74.           } else {
    75.             console.error("ports is null, not need close");
    76.           }
    77.         } catch (error) {
    78.           console.error(`ErrorCode: ${(error as BusinessError).code},  Message: ${(error as BusinessError).message}`);
    79.         }
    80.       })
    81.       Web({ src: $rawfile('index.html'), controller: this.controller })
    82.     }
    83.   }
    84. }
    
- 前端页面代码。
    
    1. <!--index.html-->
    2. <!DOCTYPE html>
    3. <html>
    4. <head>
    5.     <meta name="viewport" content="width=device-width, initial-scale=1.0">
    6.     <title>WebView Message Port Demo</title>
    7. </head>
    8. <body>
    9.     <h1>WebView Message Port Demo</h1>
    10.     <div>
    11.         <input type="button" value="SendToEts" onclick="PostMsgToEts(msgFromJS.value);"/><br/>
    12.         <input id="msgFromJS" type="text" value="send this message from HTML to ets"/><br/>
    13.     </div>
    14.     <p class="output">display received message send from ets</p>
    15. </body>
    16. <script>
    17. var h5Port;
    18. var output = document.querySelector('.output');
    19. window.addEventListener('message', function (event) {
    20.     if (event.data === '__init_port__') {
    21.         if (event.ports[0] !== null) {
    22.             h5Port = event.ports[0]; // 1. 保存从应用侧发送过来的端口。
    23.             h5Port.onmessage = function (event) {
    24.               // 2. 接收ets侧发送过来的消息。
    25.               var msg = 'Got message from ets:';
    26.               var result = event.data;
    27.               if (typeof(result) === 'string') {
    28.                 console.info(`received string message from ets, string is: ${result}`);
    29.                 msg = msg + result;
    30.               } else if (typeof(result) === 'object') {
    31.                 if (result instanceof ArrayBuffer) {
    32.                   console.info(`received arraybuffer from ets, length is: ${result.byteLength}`);
    33.                   msg = msg + 'length is ' + result.byteLength;
    34.                 } else {
    35.                   console.info('not support');
    36.                 }
    37.               } else {
    38.                 console.info('not support');
    39.               }
    40.               output.innerHTML = msg;
    41.             }
    42.         }
    43.     }
    44. })
    
    45. // 3. 使用h5Port向应用侧发送消息。
    46. function PostMsgToEts(data) {
    47.     if (h5Port) {
    48.       h5Port.postMessage(data);
    49.     } else {
    50.       console.error('h5Port is null, Please initialize first');
    51.     }
    52. }
    53. </script>
    54. </html>
    

## 常见问题

### 为什么H5向应用侧发送消息接收不到？

检查传递的数据类型是否正确，WebMessage支持的数据类型有string和ArrayBuffer。

如果想要传递对象类型则需要将对象类型通过JSON.stringify方法转换为string类型再进行传递。示例如下：

1.   function PostMsgToEts(data) {
2.       if (h5Port) {
3.         let obj = {name:'exampleName',id:10}
4.         h5Port.postMessage(JSON.stringify(obj));
5.       } else {
6.         console.error('h5Port is null. Please initialize it first.');
7.       }
8.   }

### onControllerAttached与javaScriptOnDocumentStart的执行顺序是什么？

[javaScriptOnDocumentStart](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#javascriptondocumentstart11)在[onControllerAttached](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#oncontrollerattached10)之后执行。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-in-page-app-function-invoking "前端页面调用应用侧函数")
# 应用侧与前端页面的相互调用(C/C++)

更新时间: 2025-12-16 16:38

本指导适用于ArkWeb应用侧与前端网页通信场景，开发者可根据应用架构选择使用ArkWeb Native接口完成业务通信机制（以下简称Native JSBridge）。

针对JSBridge进行性能优化可参考[JSBridge优化解决方案](https://developer.huawei.com/consumer/cn/doc/best-practices/bpta-web-develop-optimization#section58781855115017)

## 适用的应用架构

应用使用ArkTS、C++语言混合开发，或本身应用架构较贴近于小程序架构，自带C++侧环境，推荐使用ArkWeb在Native侧提供的[ArkWeb_ControllerAPI](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-web-arkweb-controllerapi)、[ArkWeb_ComponentAPI](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-web-arkweb-componentapi)实现JSBridge功能。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163844.00876047452510399031376388495108:50001231000000:2800:14D9D8D0644F9FC946EB673EDFF9E34B905E261F0136DDC0824FA99D91783786.png)

上图展示了具有普遍适用性的小程序的通用架构。在这一架构中，逻辑层依赖于应用程序自带的JavaScript运行时，该运行时在一个已有的C++环境中运行。通过Native接口，逻辑层能够直接在C++环境中与视图层（其中ArkWeb充当渲染器）进行通信，无需回退至ArkTS环境使用ArkTS JSBridge接口。

左图是使用ArkTS JSBridge接口构建小程序的方案，如红框所示，应用需要先调用到ArkTS环境，再调用到C++环境。右图是使用Native JSBridge接口构建小程序的方案，不需要ArkTS环境和C++环境的切换，执行效率更高。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163844.06698074369186965169427447244791:50001231000000:2800:74B046CBC940ECEF96E1A1DE740BBF7892B55E841E588427BC55FBCA86E09326.png)

Native JSBridge方案解决了ArkTS环境的冗余切换，同时允许回调在非UI线程上运行，避免造成UI阻塞。

## 使用Native接口实现JSBridge通信（推荐）

原先，Native同步接口不支持返回值，其返回类型固定为void。然而，为满足业务扩展需求，自API version 18起，引入了替代接口，支持bool、string和buffer类型的返回值。

另外针对同步接口[registerJavaScriptProxyEx](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-web-arkweb-controllerapi#registerjavascriptproxyex)和异步接口[registerAsyncJavaScriptProxyEx](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-web-arkweb-controllerapi#registerasyncjavascriptproxyex)，新增了参数[permission](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkweb-ndk-jsbridge#%E5%89%8D%E7%AB%AF%E9%A1%B5%E9%9D%A2%E8%B0%83%E7%94%A8%E5%BA%94%E7%94%A8%E4%BE%A7%E5%87%BD%E6%95%B0)字段，用于调用权限控制。

### 接口替代关系

|不推荐的接口|替代接口|说明|
|:--|:--|:--|
|ArkWeb_OnJavaScriptProxyCallback|ArkWeb_OnJavaScriptProxyCallbackWithResult|Proxy方法被执行的回调。|
|ArkWeb_ProxyMethod|ArkWeb_ProxyMethodWithResult|注入的Proxy方法通用结构体。|
|ArkWeb_ProxyObject|ArkWeb_ProxyObjectWithResult|注入的Proxy对象通用结构体。|
|registerJavaScriptProxy|registerJavaScriptProxyEx|注入JavaScript对象到window对象中，并在window对象中调用该对象的同步方法。|
|registerAsyncJavaScriptProxy|registerAsyncJavaScriptProxyEx|注入JavaScript对象到window对象中，并在window对象中调用该对象的异步方法。|

### 使用Native接口绑定ArkWeb

- ArkWeb组件声明在ArkTS侧，需要用户自定义一个标识webTag，并将webTag通过Node-API传至应用Native侧，后续ArkWeb Native接口使用，均需webTag作为对应组件的唯一标识。
    
- ArkTS侧
    
    1. // 自定义webTag，在WebviewController创建时作为入参传入，建立controller与webTag的映射关系
    2. webTag: string = 'ArkWeb1';
    3. controller: webview.WebviewController = new webview.WebviewController(this.webTag);
    
    4. // 在aboutToAppear方法中，通过Node-API接口将webTag传入C++侧，C++侧使用webTag作为ArkWeb组件的唯一标识
    5. aboutToAppear() {
    6.   console.info("aboutToAppear")
    7.   //初始化web ndk
    8.   testNapi.nativeWebInit(this.webTag);
    9. }
    
- C++侧
    
    1. // 解析存储webTag
    2. static napi_value NativeWebInit(napi_env env, napi_callback_info info) {
    3.     OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk NativeWebInit start");
    4.     size_t argc = 1;
    5.     napi_value args[1] = {nullptr};
    6.     napi_get_cb_info(env, info, &argc, args, nullptr, nullptr);
    7.     // 获取第一个参数webTag
    8.     size_t webTagSize = 0;
    9.     napi_get_value_string_utf8(env, args[0], nullptr, 0, &webTagSize);
    10.     char *webTagValue = new (std::nothrow) char[webTagSize + 1];
    11.     size_t webTagLength = 0;
    12.     napi_get_value_string_utf8(env, args[0], webTagValue, webTagSize + 1, &webTagLength);
    13.     OH_LOG_Print(LOG_APP, LOG_ERROR, LOG_PRINT_DOMAIN, "ArkWeb", "ndk NativeWebInit webTag:%{public}s", webTagValue);
    
    14.     // 将webTag保存在实例对象中
    15.     jsbridge_object_ptr = std::make_shared<JSBridgeObject>(webTagValue);
    16.     // ...
    17. }
    

### 使用Native接口获取API结构体

在ArkWeb Native侧，需要先获取API结构体，才能调用结构体里的Native API。ArkWeb Native侧API通过函数[OH_ArkWeb_GetNativeAPI](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-arkweb-interface-h#oh_arkweb_getnativeapi)获取，根据入参type不同，可分别获取[ArkWeb_ControllerAPI](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-web-arkweb-controllerapi)、[ArkWeb_ComponentAPI](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-web-arkweb-componentapi)结构体。其中，[ArkWeb_ControllerAPI](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-web-arkweb-controllerapi)对应ArkTS侧[web_webview.WebviewController API](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller)，[ArkWeb_ComponentAPI](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-web-arkweb-componentapi)对应ArkTS侧[ArkWeb组件API](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web)。

1. static ArkWeb_ControllerAPI *controller = nullptr;
2. static ArkWeb_ComponentAPI *component = nullptr;
3. // ...
4. controller = reinterpret_cast<ArkWeb_ControllerAPI *>(OH_ArkWeb_GetNativeAPI(ARKWEB_NATIVE_CONTROLLER));
5. component = reinterpret_cast<ArkWeb_ComponentAPI *>(OH_ArkWeb_GetNativeAPI(ARKWEB_NATIVE_COMPONENT));

### Native侧注册组件生命周期回调

通过[ArkWeb_ComponentAPI](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-web-arkweb-componentapi)注册组件生命周期回调，调用接口前，建议通过[ARKWEB_MEMBER_MISSING](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-arkweb-type-h#%E5%AE%8F%E5%AE%9A%E4%B9%89)校验该函数结构体中是否存在对应函数指针，以避免SDK与设备ROM不匹配导致crash问题。

1. if (!ARKWEB_MEMBER_MISSING(component, onControllerAttached)) {
2.     component->onControllerAttached(webTagValue, ValidCallback,
3.                                     static_cast<void *>(jsbridge_object_ptr->GetWeakPtr()));
4. } else {
5.     OH_LOG_Print(LOG_APP, LOG_ERROR, LOG_PRINT_DOMAIN, "ArkWeb", "component onControllerAttached func not exist");
6. }

7. if (!ARKWEB_MEMBER_MISSING(component, onPageBegin)) {
8.     component->onPageBegin(webTagValue, LoadStartCallback,
9.                                     static_cast<void *>(jsbridge_object_ptr->GetWeakPtr()));
10. } else {
11.     OH_LOG_Print(LOG_APP, LOG_ERROR, LOG_PRINT_DOMAIN, "ArkWeb", "component onPageBegin func not exist");
12. }

13. if (!ARKWEB_MEMBER_MISSING(component, onPageEnd)) {
14.     component->onPageEnd(webTagValue, LoadEndCallback,
15.                                     static_cast<void *>(jsbridge_object_ptr->GetWeakPtr()));
16. } else {
17.     OH_LOG_Print(LOG_APP, LOG_ERROR, LOG_PRINT_DOMAIN, "ArkWeb", "component onPageEnd func not exist");
18. }

19. if (!ARKWEB_MEMBER_MISSING(component, onDestroy)) {
20.     component->onDestroy(webTagValue, DestroyCallback,
21.                                     static_cast<void *>(jsbridge_object_ptr->GetWeakPtr()));
22. } else {
23.     OH_LOG_Print(LOG_APP, LOG_ERROR, LOG_PRINT_DOMAIN, "ArkWeb", "component onDestroy func not exist");
24. }

### 前端页面调用应用侧函数

通过[registerJavaScriptProxyEx](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-web-arkweb-controllerapi#registerjavascriptproxyex)将应用侧函数注册至前端页面，注册后在下次加载或者重新加载后生效。

1. // 注册对象
2. OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk registerJavaScriptProxyEx begin");
3. ArkWeb_ProxyMethodWithResult method1 = {"method1", ProxyMethod1, static_cast<void *>(jsbridge_object_ptr->GetWeakPtr())};
4. ArkWeb_ProxyMethodWithResult method2 = {"method2", ProxyMethod2, static_cast<void *>(jsbridge_object_ptr->GetWeakPtr())};
5. ArkWeb_ProxyMethodWithResult methodList[2] = {method1, method2};
6. // 调用ndk接口注册对象
7. // 如此注册的情况下，在H5页面就可以使用proxy.method1、proxy.method2调用此文件下的ProxyMethod1和ProxyMethod2方法了
8. ArkWeb_ProxyObjectWithResult proxyObject = {"ndkProxy", methodList, 2};
9. // 参数permission为空，表示不进行权限管控
10. controller->registerJavaScriptProxyEx(webTag, &proxyObject, /*permission*/"");

- 参数permission是一个JSON字符串，示例如下：

1. {
2.   "javascriptProxyPermission": {
3.     "urlPermissionList": [       // Object级权限，如果匹配，所有Method都授权
4.       {
5.         "scheme": "resource",    // 精确匹配，不能为空
6.         "host": "rawfile",       // 精确匹配，不能为空
7.         "port": "",              // 精确匹配，为空不检查
8.         "path": ""               // 前缀匹配，为空不检查
9.       },
10.       {
11.         "scheme": "https",       // 精确匹配，不能为空
12.         "host": "xxx.com",       // 精确匹配，不能为空
13.         "port": "8080",          // 精确匹配，为空不检查
14.         "path": "a/b/c"          // 前缀匹配，为空不检查
15.       }
16.     ],
17.     "methodList": [
18.       {
19.         "methodName": "test",
20.         "urlPermissionList": [   // Method级权限
21.           {
22.             "scheme": "https",   // 精确匹配，不能为空
23.             "host": "xxx.com",   // 精确匹配，不能为空
24.             "port": "",          // 精确匹配，为空不检查
25.             "path": ""           // 前缀匹配，为空不检查
26.           },
27.           {
28.             "scheme": "resource",// 精确匹配，不能为空
29.             "host": "rawfile",   // 精确匹配，不能为空
30.             "port": "",          // 精确匹配，为空不检查
31.             "path": ""           // 前缀匹配，为空不检查
32.           }
33.         ]
34.       },
35.       {
36.         "methodName": "test11",
37.         "urlPermissionList": [   // Method级权限
38.           {
39.             "scheme": "q",       // 精确匹配，不能为空
40.             "host": "r",         // 精确匹配，不能为空
41.             "port": "",          // 精确匹配，为空不检查
42.             "path": "t"          // 前缀匹配，为空不检查
43.           },
44.           {
45.             "scheme": "u",       // 精确匹配，不能为空
46.             "host": "v",         // 精确匹配，不能为空
47.             "port": "",          // 精确匹配，为空不检查
48.             "path": ""           // 前缀匹配，为空不检查
49.           }
50.         ]
51.       }
52.     ]
53.   }
54. }

### 应用侧调用前端页面函数

使用[runJavaScript](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-web-arkweb-controllerapi#runjavascript)调用前端页面函数。

1. // 构造runJS执行的结构体
2. char* jsCode = "runJSRetStr()";
3. ArkWeb_JavaScriptObject object = {(uint8_t *)jsCode, bufferSize, &JSBridgeObject::StaticRunJavaScriptCallback,
4.                                      static_cast<void *>(jsbridge_object_ptr->GetWeakPtr())};
5. // 调用前端页面runJSRetStr()函数
6. controller->runJavaScript(webTagValue, &object);

### 完整示例

- 前端页面代码
    
    1. <!-- entry/src/main/resources/rawfile/runJS.html -->
    2. <!-- runJS.html -->
    3. <!DOCTYPE html>
    4. <html lang="en-gb">
    5. <head>
    6.     <meta name="viewport" content="width=device-width, initial-scale=1.0">
    7.     <title>run javascript demo</title>
    8. </head>
    9. <body>
    10. <h1>run JavaScript Ext demo</h1>
    11. <p id="webDemo"></p>
    12. <br>
    13. <button type="button" style="height:30px;width:200px" onclick="testNdkProxyObjMethod1()">test ndk method1 ! </button>
    14. <br>
    15. <br>
    16. <button type="button" style="height:30px;width:200px" onclick="testNdkProxyObjMethod2()">test ndk method2 ! </button>
    17. <br>
    
    18. </body>
    19. <script type="text/javascript">
    
    20. function testNdkProxyObjMethod1() {
    21.       if (window.ndkProxy == undefined) {
    22.             document.getElementById("webDemo").innerHTML = "ndkProxy undefined"
    23.             return "objName undefined"
    24.       }
    
    25.       if (window.ndkProxy.method1 == undefined) {
    26.             document.getElementById("webDemo").innerHTML = "ndkProxy method1 undefined"
    27.             return "objName  test undefined"
    28.       }
    
    29.       let retStr = window.ndkProxy.method1("hello", "world", [1.2, -3.4, 123.456], ["Saab", "Volvo", "BMW", undefined], 1.23456, 123789, true, false, 0,  undefined);
    30.       console.info("ndkProxy and method1 is ok, " + retStr + ", type:" + typeof(retStr));
    31. }
    
    32. function testNdkProxyObjMethod2() {
    33.       if (window.ndkProxy == undefined) {
    34.             document.getElementById("webDemo").innerHTML = "ndkProxy undefined"
    35.             return "objName undefined"
    36.       }
    
    37.       if (window.ndkProxy.method2 == undefined) {
    38.             document.getElementById("webDemo").innerHTML = "ndkProxy method2 undefined"
    39.             return "objName  test undefined"
    40.       }
    
    41.     var student = {
    42.             name:"zhang",
    43.             sex:"man",
    44.             age:25
    45.     };
    46.     var cars = [student, 456, false, 4.567];
    47.     let params = "[\"{\\\"scope\\\"]";
    
    48.     let retStr = window.ndkProxy.method2("hello", "world", false, cars, params);
    49.     console.info("ndkProxy and method2 is ok, " + retStr + ", type:" + typeof(retStr));
    50. }
    
    51. function runJSRetStr(data) {
    52.     const d = new Date();
    53.     let time = d.getTime();
    54.     return JSON.stringify(time)
    55. }
    56. </script>
    57. </html>
    
- ArkTS侧代码
    
    1. // entry/src/main/ets/pages/Index.ets
    2. import testNapi from 'libentry.so';
    3. import { webview } from '@kit.ArkWeb';
    
    4. class testObj {
    5.   constructor() {
    6.   }
    
    7.   test(): string {
    8.     console.info('ArkUI Web Component');
    9.     return "ArkUI Web Component";
    10.   }
    
    11.   toString(): void {
    12.     console.info('Web Component toString');
    13.   }
    14. }
    
    15. @Entry
    16. @Component
    17. struct Index {
    18.   webTag: string = 'ArkWeb1';
    19.   controller: webview.WebviewController = new webview.WebviewController(this.webTag);
    20.   @State testObjtest: testObj = new testObj();
    
    21.   aboutToAppear() {
    22.     console.info("aboutToAppear")
    23.     //初始化web ndk
    24.     testNapi.nativeWebInit(this.webTag);
    25.   }
    
    26.   build() {
    27.     Column() {
    28.       Row() {
    29.         Button('runJS hello')
    30.           .fontSize(12)
    31.           .onClick(() => {
    32.             testNapi.runJavaScript(this.webTag, "runJSRetStr(\"" + "hello" + "\")");
    33.           })
    34.       }.height('20%')
    
    35.       Row() {
    36.         Web({ src: $rawfile('runJS.html'), controller: this.controller })
    37.           .javaScriptAccess(true)
    38.           .fileAccess(true)
    39.           .onControllerAttached(() => {
    40.             console.error("ndk onControllerAttached webId: " + this.controller.getWebId());
    41.           })
    42.       }.height('80%')
    43.     }
    44.   }
    45. }
    
- Node-API侧暴露ArkTS接口
    
    1. // entry/src/main/cpp/types/libentry/index.d.ts
    2. export const nativeWebInit: (webName: string) => void;
    3. export const runJavaScript: (webName: string, jsCode: string) => void;
    
- Node-API侧编译配置entry/src/main/cpp/CMakeLists.txt
    
    1. # the minimum version of CMake.
    2. cmake_minimum_required(VERSION 3.4.1)
    3. project(NDKJSBridg)
    
    4. set(NATIVERENDER_ROOT_PATH ${CMAKE_CURRENT_SOURCE_DIR})
    
    5. if(DEFINED PACKAGE_FIND_FILE)
    6.     include(${PACKAGE_FIND_FILE})
    7. endif()
    
    8. include_directories(${NATIVERENDER_ROOT_PATH}
    9.                     ${NATIVERENDER_ROOT_PATH}/include)
    
    10. add_library(entry SHARED hello.cpp jsbridge_object.cpp)
    
    11. find_library(
    12.     # Sets the name of the path variable.
    13.     hilog-lib
    14.     # Specifies the name of the NDK library that
    15.     # you want CMake to locate.
    16.     hilog_ndk.z
    17. )
    
    18. target_link_libraries(entry PUBLIC libace_napi.z.so ${hilog-lib} libohweb.so)
    
- Node-API层代码
    
    1. // entry/src/main/cpp/hello.cpp
    2. #include "napi/native_api.h"
    3. #include <bits/alltypes.h>
    4. #include <memory>
    5. #include <string>
    6. #include <sys/types.h>
    7. #include <thread>
    
    8. #include "hilog/log.h"
    9. #include "web/arkweb_interface.h"
    10. #include "jsbridge_object.h"
    
    11. constexpr unsigned int LOG_PRINT_DOMAIN = 0xFF00;
    12. std::shared_ptr<JSBridgeObject> jsbridge_object_ptr = nullptr;
    13. static ArkWeb_ControllerAPI *controller = nullptr;
    14. static ArkWeb_ComponentAPI *component = nullptr;
    15. ArkWeb_JavaScriptValueAPI *javaScriptValueApi = nullptr;
    
    16. // 发送JS脚本到H5侧执行，该方法为执行结果的回调。
    17. static void RunJavaScriptCallback(const char *webTag, const char *result, void *userData) {
    18.     OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk RunJavaScriptCallback webTag:%{public}s", webTag);
    19.     if (!userData) {
    20.         OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk RunJavaScriptCallback userData is nullptr");
    21.         return;
    22.     }
    23.     std::weak_ptr<JSBridgeObject> jsb_weak_ptr = *static_cast<std::weak_ptr<JSBridgeObject> *>(userData);
    24.     if (auto jsb_ptr = jsb_weak_ptr.lock()) {
    25.         jsb_ptr->RunJavaScriptCallback(result);
    26.     } else {
    27.         OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb",
    28.                      "ndk RunJavaScriptCallback jsb_weak_ptr lock failed");
    29.     }
    30. }
    
    31. // 示例代码 ，注册了1个对象，2个方法
    32. static ArkWeb_JavaScriptValuePtr ProxyMethod1(const char *webTag, const ArkWeb_JavaScriptBridgeData *dataArray, size_t arraySize, void *userData) {
    33.     OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk ProxyMethod1 webTag:%{public}s", webTag);
    34.     if (!userData) {
    35.         OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk ProxyMethod1 userData is nullptr");
    36.         return nullptr;
    37.     }
    38.     std::weak_ptr<JSBridgeObject> jsb_weak_ptr = *static_cast<std::weak_ptr<JSBridgeObject> *>(userData);
    39.     if (auto jsb_ptr = jsb_weak_ptr.lock()) {
    40.         jsb_ptr->ProxyMethod1(dataArray, arraySize);
    41.     } else {
    42.         OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk ProxyMethod1 jsb_weak_ptr lock failed");
    43.     }
    
    44.     bool boolValue = true;
    45.     return javaScriptValueApi->createJavaScriptValue(ArkWeb_JavaScriptValueType::ARKWEB_JAVASCRIPT_BOOL, (void*)(&boolValue), 1);
    46. }
    
    47. static ArkWeb_JavaScriptValuePtr ProxyMethod2(const char *webTag, const ArkWeb_JavaScriptBridgeData *dataArray, size_t arraySize, void *userData) {
    48.     OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk ProxyMethod2 webTag:%{public}s", webTag);
    49.     if (!userData) {
    50.         OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk ProxyMethod2 userData is nullptr");
    51.         return nullptr;
    52.     }
    53.     std::weak_ptr<JSBridgeObject> jsb_weak_ptr = *static_cast<std::weak_ptr<JSBridgeObject> *>(userData);
    
    54.     std::string jsCode = "runJSRetStr()";
    55.     ArkWeb_JavaScriptObject object = {(uint8_t *)jsCode.c_str(), jsCode.size(),
    56.                                      &JSBridgeObject::StaticRunJavaScriptCallback,
    57.                                      static_cast<void *>(jsbridge_object_ptr->GetWeakPtr())};
    58.     controller->runJavaScript(webTag, &object);
    
    59.     if (auto jsb_ptr = jsb_weak_ptr.lock()) {
    60.         jsb_ptr->ProxyMethod2(dataArray, arraySize);
    61.     } else {
    62.         OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk ProxyMethod2 jsb_weak_ptr lock failed");
    63.     }
    
    64.     std::string str = "this is a string";
    65.     return javaScriptValueApi->createJavaScriptValue(ArkWeb_JavaScriptValueType::ARKWEB_JAVASCRIPT_STRING, (void*)str.c_str(), str.length() + 1);
    66. }
    
    67. void ValidCallback(const char *webTag, void *userData) {
    68.     OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk ValidCallback webTag: %{public}s", webTag);
    69.     if (!userData) {
    70.         OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk ValidCallback userData is nullptr");
    71.         return;
    72.     }
    73.     std::weak_ptr<JSBridgeObject> jsb_weak_ptr = *static_cast<std::weak_ptr<JSBridgeObject> *>(userData);
    74.     if (auto jsb_ptr = jsb_weak_ptr.lock()) {
    75.         jsb_ptr->SaySomething("ValidCallback");
    76.     } else {
    77.         OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk ValidCallback jsb_weak_ptr lock failed");
    78.     }
    
    79.     // 注册对象
    80.     OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk registerJavaScriptProxyEx begin");
    81.     ArkWeb_ProxyMethodWithResult method1 = {"method1", ProxyMethod1, static_cast<void *>(jsbridge_object_ptr->GetWeakPtr())};
    82.     ArkWeb_ProxyMethodWithResult method2 = {"method2", ProxyMethod2, static_cast<void *>(jsbridge_object_ptr->GetWeakPtr())};
    83.     ArkWeb_ProxyMethodWithResult methodList[2] = {method1, method2};
    84.     // 调用ndk接口注册对象
    85.     // 如此注册的情况下，在H5页面就可以使用proxy.method1、proxy.method2调用此文件下的ProxyMethod1和ProxyMethod2方法了
    86.     ArkWeb_ProxyObjectWithResult proxyObject = {"ndkProxy", methodList, 2};
    87.     controller->registerJavaScriptProxyEx(webTag, &proxyObject, "");
    
    88.     OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk registerJavaScriptProxyEx end");
    89. }
    
    90. void LoadStartCallback(const char *webTag, void *userData) {
    91.     OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk LoadStartCallback webTag: %{public}s", webTag);
    92.     if (!userData) {
    93.         OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk LoadStartCallback userData is nullptr");
    94.         return;
    95.     }
    96.     std::weak_ptr<JSBridgeObject> jsb_weak_ptr = *static_cast<std::weak_ptr<JSBridgeObject> *>(userData);
    97.     if (auto jsb_ptr = jsb_weak_ptr.lock()) {
    98.         jsb_ptr->SaySomething("LoadStartCallback");
    99.     } else {
    100.         OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk LoadStartCallback jsb_weak_ptr lock failed");
    101.     }
    102. }
    
    103. void LoadEndCallback(const char *webTag, void *userData) {
    104.     OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk LoadEndCallback webTag: %{public}s", webTag);
    105.     if (!userData) {
    106.         OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk LoadEndCallback userData is nullptr");
    107.         return;
    108.     }
    109.     std::weak_ptr<JSBridgeObject> jsb_weak_ptr = *static_cast<std::weak_ptr<JSBridgeObject> *>(userData);
    110.     if (auto jsb_ptr = jsb_weak_ptr.lock()) {
    111.         jsb_ptr->SaySomething("LoadEndCallback");
    112.     } else {
    113.         OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk LoadEndCallback jsb_weak_ptr lock failed");
    114.     }
    115. }
    
    116. void DestroyCallback(const char *webTag, void *userData) {
    117.     OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk DestroyCallback webTag: %{public}s", webTag);
    118.     if (!userData) {
    119.         OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk DestroyCallback userData is nullptr");
    120.         return;
    121.     }
    122.     std::weak_ptr<JSBridgeObject> jsb_weak_ptr = *static_cast<std::weak_ptr<JSBridgeObject> *>(userData);
    123.     if (auto jsb_ptr = jsb_weak_ptr.lock()) {
    124.         jsb_ptr->SaySomething("DestroyCallback");
    125.     } else {
    126.         OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk DestroyCallback jsb_weak_ptr lock failed");
    127.     }
    128. }
    
    129. void SetComponentCallback(ArkWeb_ComponentAPI * component, const char* webTagValue) {
    130.     if (!ARKWEB_MEMBER_MISSING(component, onControllerAttached)) {
    131.         component->onControllerAttached(webTagValue, ValidCallback,
    132.                                         static_cast<void *>(jsbridge_object_ptr->GetWeakPtr()));
    133.     } else {
    134.         OH_LOG_Print(LOG_APP, LOG_ERROR, LOG_PRINT_DOMAIN, "ArkWeb", "component onControllerAttached func not exist");
    135.     }
    
    136.     if (!ARKWEB_MEMBER_MISSING(component, onPageBegin)) {
    137.         component->onPageBegin(webTagValue, LoadStartCallback,
    138.                                         static_cast<void *>(jsbridge_object_ptr->GetWeakPtr()));
    139.     } else {
    140.         OH_LOG_Print(LOG_APP, LOG_ERROR, LOG_PRINT_DOMAIN, "ArkWeb", "component onPageBegin func not exist");
    141.     }
    
    142.     if (!ARKWEB_MEMBER_MISSING(component, onPageEnd)) {
    143.         component->onPageEnd(webTagValue, LoadEndCallback,
    144.                                         static_cast<void *>(jsbridge_object_ptr->GetWeakPtr()));
    145.     } else {
    146.         OH_LOG_Print(LOG_APP, LOG_ERROR, LOG_PRINT_DOMAIN, "ArkWeb", "component onPageEnd func not exist");
    147.     }
    
    148.     if (!ARKWEB_MEMBER_MISSING(component, onDestroy)) {
    149.         component->onDestroy(webTagValue, DestroyCallback,
    150.                                         static_cast<void *>(jsbridge_object_ptr->GetWeakPtr()));
    151.     } else {
    152.         OH_LOG_Print(LOG_APP, LOG_ERROR, LOG_PRINT_DOMAIN, "ArkWeb", "component onDestroy func not exist");
    153.     }
    154. }
    
    155. // 解析存储webTag
    156. static napi_value NativeWebInit(napi_env env, napi_callback_info info) {
    157.   OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk NativeWebInit start");
    158.   size_t argc = 1;
    159.   napi_value args[1] = {nullptr};
    160.   napi_get_cb_info(env, info, &argc, args, nullptr, nullptr);
    161.   // 获取第一个参数 webTag
    162.   size_t webTagSize = 0;
    163.   napi_get_value_string_utf8(env, args[0], nullptr, 0, &webTagSize);
    164.   char *webTagValue = new (std::nothrow) char[webTagSize + 1];
    165.   size_t webTagLength = 0;
    166.   napi_get_value_string_utf8(env, args[0], webTagValue, webTagSize + 1, &webTagLength);
    167.   OH_LOG_Print(LOG_APP, LOG_ERROR, LOG_PRINT_DOMAIN, "ArkWeb", "ndk NativeWebInit webTag:%{public}s", webTagValue);
    
    168.   jsbridge_object_ptr = std::make_shared<JSBridgeObject>(webTagValue);
    169.   if (jsbridge_object_ptr)
    170.       jsbridge_object_ptr->Init();
    
    171.   controller = reinterpret_cast<ArkWeb_ControllerAPI *>(OH_ArkWeb_GetNativeAPI(ARKWEB_NATIVE_CONTROLLER));
    172.   if (controller)
    173.       OH_LOG_Print(LOG_APP, LOG_ERROR, LOG_PRINT_DOMAIN, "ArkWeb", "get ArkWeb_ControllerAPI success");
    
    174.   component = reinterpret_cast<ArkWeb_ComponentAPI *>(OH_ArkWeb_GetNativeAPI(ARKWEB_NATIVE_COMPONENT));
    175.   if (component)
    176.       OH_LOG_Print(LOG_APP, LOG_ERROR, LOG_PRINT_DOMAIN, "ArkWeb", "get ArkWeb_ComponentAPI success");
    
    177.   javaScriptValueApi =
    178.       reinterpret_cast<ArkWeb_JavaScriptValueAPI *>(OH_ArkWeb_GetNativeAPI(ARKWEB_NATIVE_JAVASCRIPT_VALUE));
    179.   if (javaScriptValueApi)
    180.       OH_LOG_Print(LOG_APP, LOG_ERROR, LOG_PRINT_DOMAIN, "ArkWeb", "get ArkWeb_JavaScriptValueAPI success");
    181.   else
    182.       OH_LOG_Print(LOG_APP, LOG_ERROR, LOG_PRINT_DOMAIN, "ArkWeb", "get ArkWeb_JavaScriptValueAPI failed");
    
    183.   SetComponentCallback(component, webTagValue);
    
    184.   OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk NativeWebInit end");
    
    185.   delete[] webTagValue;
    
    186.   return nullptr;
    187. }
    
    188. // 发送JS脚本到H5侧执行
    189. static napi_value RunJavaScript(napi_env env, napi_callback_info info) {
    190.     size_t argc = 2;
    191.     napi_value args[2] = {nullptr};
    192.     napi_get_cb_info(env, info, &argc, args, nullptr, nullptr);
    
    193.     // 获取第一个参数webTag
    194.     size_t webTagSize = 0;
    195.     napi_get_value_string_utf8(env, args[0], nullptr, 0, &webTagSize);
    196.     char *webTagValue = new (std::nothrow) char[webTagSize + 1];
    197.     size_t webTagLength = 0;
    198.     napi_get_value_string_utf8(env, args[0], webTagValue, webTagSize + 1, &webTagLength);
    199.     OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk OH_NativeArkWeb_RunJavaScript webTag:%{public}s",
    200.                  webTagValue);
    
    201.     // 获取第二个参数 jsCode
    202.     size_t bufferSize = 0;
    203.     napi_get_value_string_utf8(env, args[1], nullptr, 0, &bufferSize);
    204.     char *jsCode = new (std::nothrow) char[bufferSize + 1];
    205.     size_t byteLength = 0;
    206.     napi_get_value_string_utf8(env, args[1], jsCode, bufferSize + 1, &byteLength);
    
    207.     OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb",
    208.                  "ndk OH_NativeArkWeb_RunJavaScript jsCode len:%{public}zu", strlen(jsCode));
    
    209.     // 构造runJS执行的结构体
    210.     ArkWeb_JavaScriptObject object = {(uint8_t *)jsCode, bufferSize, &JSBridgeObject::StaticRunJavaScriptCallback,
    211.                                      static_cast<void *>(jsbridge_object_ptr->GetWeakPtr())};
    212.     controller->runJavaScript(webTagValue, &object);
    
    213.     delete[] webTagValue;
    
    214.     delete[] jsCode;
    
    215.     return nullptr;
    216. }
    
    217. EXTERN_C_START
    218. static napi_value Init(napi_env env, napi_value exports) {
    219.     napi_property_descriptor desc[] = {
    220.         {"nativeWebInit", nullptr, NativeWebInit, nullptr, nullptr, nullptr, napi_default, nullptr},
    221.         {"runJavaScript", nullptr, RunJavaScript, nullptr, nullptr, nullptr, napi_default, nullptr},
    222.     };
    223.     napi_define_properties(env, exports, sizeof(desc) / sizeof(desc[0]), desc);
    224.     return exports;
    225. }
    226. EXTERN_C_END
    
    227. static napi_module demoModule = {
    228.     .nm_version = 1,
    229.     .nm_flags = 0,
    230.     .nm_filename = nullptr,
    231.     .nm_register_func = Init,
    232.     .nm_modname = "entry",
    233.     .nm_priv = ((void *)0),
    234.     .reserved = {0},
    235. };
    
    236. extern "C" __attribute__((constructor)) void RegisterEntryModule(void) { napi_module_register(&demoModule); }
    
- Native侧业务代码
    
    1. // entry/src/main/cpp/jsbridge_object.h
    2. #include "web/arkweb_type.h"
    3. #include <string>
    
    4. class JSBridgeObject : public std::enable_shared_from_this<JSBridgeObject> {
    5. public:
    6.     JSBridgeObject(const char* webTag);
    7.     ~JSBridgeObject() = default;
    8.     void Init();
    9.     std::weak_ptr<JSBridgeObject>* GetWeakPtr();
    10.     static void StaticRunJavaScriptCallback(const char *webTag, const ArkWeb_JavaScriptBridgeData *data, void *userData);
    11.     void RunJavaScriptCallback(const char *result);
    12.     void ProxyMethod1(const ArkWeb_JavaScriptBridgeData *dataArray, int32_t arraySize);
    13.     void ProxyMethod2(const ArkWeb_JavaScriptBridgeData *dataArray, int32_t arraySize);
    14.     void SaySomething(const char* say);
    
    15. private:
    16.     std::string webTag_;
    17.     std::weak_ptr<JSBridgeObject> weak_ptr_;
    18. };
    
    19. // entry/src/main/cpp/jsbridge_object.cpp
    20. #include "jsbridge_object.h"
    
    21. #include "hilog/log.h"
    
    22. constexpr unsigned int LOG_PRINT_DOMAIN = 0xFF00;
    
    23. JSBridgeObject::JSBridgeObject(const char *webTag) : webTag_(webTag) {}
    
    24. void JSBridgeObject::Init() { weak_ptr_ = shared_from_this(); }
    
    25. std::weak_ptr<JSBridgeObject> *JSBridgeObject::GetWeakPtr() { return &weak_ptr_; }
    
    26. void JSBridgeObject::StaticRunJavaScriptCallback(const char *webTag, const ArkWeb_JavaScriptBridgeData *data,
    27.                                                  void *userData) {
    28.     OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb",
    29.                  "JSBridgeObject StaticRunJavaScriptCallback webTag:%{public}s", webTag);
    30.     if (!userData) {
    31.         OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb",
    32.                      "JSBridgeObject StaticRunJavaScriptCallback userData is nullptr");
    33.         return;
    34.     }
    35.     std::weak_ptr<JSBridgeObject> jsb_weak_ptr = *static_cast<std::weak_ptr<JSBridgeObject> *>(userData);
    36.     if (auto jsb_ptr = jsb_weak_ptr.lock()) {
    37.         std::string result((char *)data->buffer, data->size);
    38.         jsb_ptr->RunJavaScriptCallback(result.c_str());
    39.     } else {
    40.         OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb",
    41.                      "JSBridgeObject StaticRunJavaScriptCallback jsb_weak_ptr lock failed");
    42.     }
    43. }
    
    44. void JSBridgeObject::RunJavaScriptCallback(const char *result) {
    45.     OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb",
    46.                  "JSBridgeObject OH_NativeArkWeb_RunJavaScript result:%{public}s", result);
    47. }
    
    48. void JSBridgeObject::ProxyMethod1(const ArkWeb_JavaScriptBridgeData *dataArray, int32_t arraySize) {
    49.     OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "JSBridgeObject ProxyMethod1 argc:%{public}d",
    50.                  arraySize);
    51.     for (int i = 0; i < arraySize; i++) {
    52.         std::string result((char *)dataArray[i].buffer, dataArray[i].size);
    53.         OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb",
    54.                      "JSBridgeObject ProxyMethod1 argv[%{public}d]:%{public}s, size:%{public}d", i, result.c_str(),
    55.                      dataArray[i].size);
    56.     }
    57. }
    
    58. void JSBridgeObject::ProxyMethod2(const ArkWeb_JavaScriptBridgeData *dataArray, int32_t arraySize) {
    59.     OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "JSBridgeObject ProxyMethod2 argc:%{public}d",
    60.                  arraySize);
    61.     for (int i = 0; i < arraySize; i++) {
    62.         std::string result((char *)dataArray[i].buffer, dataArray[i].size);
    63.         OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb",
    64.                      "JSBridgeObject ProxyMethod2 argv[%{public}d]:%{public}s, size:%{public}d", i, result.c_str(),
    65.                      dataArray[i].size);
    66.     }
    67. }
    
    68. void JSBridgeObject::SaySomething(const char *say) {
    69.     OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "JSBridgeObject SaySomething argc:%{public}s", say);
    70. }
    

## 使用Native接口实现JSBridge通信

### 使用Native接口绑定ArkWeb

- ArkWeb组件声明在ArkTS侧，需要用户自定义一个标识webTag，并将webTag通过Node-API传至应用Native侧，后续ArkWeb Native接口使用，均需webTag作为对应组件的唯一标识。
    
- ArkTS侧
    
    1. // 自定义webTag，在WebviewController创建时作为入参传入，建立controller与webTag的映射关系
    2. webTag: string = 'ArkWeb1';
    3. controller: webview.WebviewController = new webview.WebviewController(this.webTag);
    4. // ...
    5. // aboutToAppear中将webTag通过Node-API接口传入C++侧，作为C++侧ArkWeb组件的唯一标识
    6. aboutToAppear() {
    7.   console.info("aboutToAppear")
    8.   //初始化web ndk
    9.   testNapi.nativeWebInit(this.webTag);
    10. }
    11. // ...
    
- C++侧
    
    1. // 解析存储webTag
    2. static napi_value NativeWebInit(napi_env env, napi_callback_info info) {
    3.     OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk NativeWebInit start");
    4.     size_t argc = 1;
    5.     napi_value args[1] = {nullptr};
    6.     napi_get_cb_info(env, info, &argc, args, nullptr, nullptr);
    7.     // 获取第一个参数webTag
    8.     size_t webTagSize = 0;
    9.     napi_get_value_string_utf8(env, args[0], nullptr, 0, &webTagSize);
    10.     char *webTagValue = new (std::nothrow) char[webTagSize + 1];
    11.     size_t webTagLength = 0;
    12.     napi_get_value_string_utf8(env, args[0], webTagValue, webTagSize + 1, &webTagLength);
    13.     OH_LOG_Print(LOG_APP, LOG_ERROR, LOG_PRINT_DOMAIN, "ArkWeb", "ndk NativeWebInit webTag:%{public}s", webTagValue);
    
    14.     // 将webTag保存在实例对象中
    15.     jsbridge_object_ptr = std::make_shared<JSBridgeObject>(webTagValue);
    16.     // ...
    17. }
    

### 使用Native接口获取API结构体

ArkWeb Native侧得先获取API结构体，才能调用结构体里的Native API。ArkWeb Native侧API通过函数[OH_ArkWeb_GetNativeAPI](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-arkweb-interface-h#oh_arkweb_getnativeapi)获取，根据入参type不同，可分别获取[ArkWeb_ControllerAPI](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-web-arkweb-controllerapi)、[ArkWeb_ComponentAPI](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-web-arkweb-componentapi)函数指针结构体。其中，[ArkWeb_ControllerAPI](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-web-arkweb-controllerapi)对应ArkTS侧[web_webview.WebviewController API](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller)，[ArkWeb_ComponentAPI](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-web-arkweb-componentapi)对应ArkTS侧[ArkWeb组件API](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web)。

1. static ArkWeb_ControllerAPI *controller = nullptr;
2. static ArkWeb_ComponentAPI *component = nullptr;
3. // ...
4. controller = reinterpret_cast<ArkWeb_ControllerAPI *>(OH_ArkWeb_GetNativeAPI(ARKWEB_NATIVE_CONTROLLER));
5. component = reinterpret_cast<ArkWeb_ComponentAPI *>(OH_ArkWeb_GetNativeAPI(ARKWEB_NATIVE_COMPONENT));

### Native侧注册组件生命周期回调

通过[ArkWeb_ComponentAPI](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-web-arkweb-componentapi)注册组件生命周期回调，在调用接口前建议通过[ARKWEB_MEMBER_MISSING](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-arkweb-type-h#%E5%AE%8F%E5%AE%9A%E4%B9%89)校验该函数结构体是否有对应函数指针，避免SDK与设备ROM不匹配导致crash问题。

1. if (!ARKWEB_MEMBER_MISSING(component, onControllerAttached)) {
2.     component->onControllerAttached(webTagValue, ValidCallback,
3.                                     static_cast<void *>(jsbridge_object_ptr->GetWeakPtr()));
4. } else {
5.     OH_LOG_Print(LOG_APP, LOG_ERROR, LOG_PRINT_DOMAIN, "ArkWeb", "component onControllerAttached func not exist");
6. }

7. if (!ARKWEB_MEMBER_MISSING(component, onPageBegin)) {
8.     component->onPageBegin(webTagValue, LoadStartCallback,
9.                                     static_cast<void *>(jsbridge_object_ptr->GetWeakPtr()));
10. } else {
11.     OH_LOG_Print(LOG_APP, LOG_ERROR, LOG_PRINT_DOMAIN, "ArkWeb", "component onPageBegin func not exist");
12. }

13. if (!ARKWEB_MEMBER_MISSING(component, onPageEnd)) {
14.     component->onPageEnd(webTagValue, LoadEndCallback,
15.                                     static_cast<void *>(jsbridge_object_ptr->GetWeakPtr()));
16. } else {
17.     OH_LOG_Print(LOG_APP, LOG_ERROR, LOG_PRINT_DOMAIN, "ArkWeb", "component onPageEnd func not exist");
18. }

19. if (!ARKWEB_MEMBER_MISSING(component, onDestroy)) {
20.     component->onDestroy(webTagValue, DestroyCallback,
21.                                     static_cast<void *>(jsbridge_object_ptr->GetWeakPtr()));
22. } else {
23.     OH_LOG_Print(LOG_APP, LOG_ERROR, LOG_PRINT_DOMAIN, "ArkWeb", "component onDestroy func not exist");
24. }

### 前端页面调用应用侧函数

通过[registerJavaScriptProxy](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-web-arkweb-controllerapi#registerjavascriptproxy)将应用侧函数注册至前端页面，注册后在下次加载或者重新加载后生效。

1. // 注册对象
2. OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk RegisterJavaScriptProxy begin");
3. ArkWeb_ProxyMethod method1 = {"method1", ProxyMethod1, static_cast<void *>(jsbridge_object_ptr->GetWeakPtr())};
4. ArkWeb_ProxyMethod method2 = {"method2", ProxyMethod2, static_cast<void *>(jsbridge_object_ptr->GetWeakPtr())};
5. ArkWeb_ProxyMethod methodList[2] = {method1, method2};
6. // 调用ndk接口注册对象
7. // 如此注册的情况下，在H5页面就可以使用proxy.method1、proxy.method2调用此文件下的ProxyMethod1和ProxyMethod2方法了
8. ArkWeb_ProxyObject proxyObject = {"ndkProxy", methodList, 2};
9. controller->registerJavaScriptProxy(webTag, &proxyObject);

### 应用侧调用前端页面函数

通过[runJavaScript](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-web-arkweb-controllerapi#runjavascript)调用前端页面函数。

1. // 构造runJS执行的结构体
2. const char* jsCode = "runJSRetStr()";
3. ArkWeb_JavaScriptObject object = {(uint8_t *)jsCode, bufferSize, &JSBridgeObject::StaticRunJavaScriptCallback,
4.                                      static_cast<void *>(jsbridge_object_ptr->GetWeakPtr())};
5. // 调用前端页面runJSRetStr()函数
6. controller->runJavaScript(webTagValue, &object);

### 完整示例

- 前端页面代码
    
    1. <!-- entry/src/main/resources/rawfile/runJS.html -->
    2. <!-- runJS.html -->
    3. <!DOCTYPE html>
    4. <html lang="en-gb">
    5. <head>
    6.     <meta name="viewport" content="width=device-width, initial-scale=1.0">
    7.     <title>run javascript demo</title>
    8. </head>
    9. <body>
    10. <h1>run JavaScript Ext demo</h1>
    11. <p id="webDemo"></p>
    12. <br>
    13. <button type="button" style="height:30px;width:200px" onclick="testNdkProxyObjMethod1()">test ndk method1 ! </button>
    14. <br>
    15. <br>
    16. <button type="button" style="height:30px;width:200px" onclick="testNdkProxyObjMethod2()">test ndk method2 ! </button>
    17. <br>
    
    18. </body>
    19. <script type="text/javascript">
    
    20. function testNdkProxyObjMethod1() {
    21.       if (window.ndkProxy == undefined) {
    22.             document.getElementById("webDemo").innerHTML = "ndkProxy undefined"
    23.             return "objName undefined"
    24.       }
    
    25.       if (window.ndkProxy.method1 == undefined) {
    26.             document.getElementById("webDemo").innerHTML = "ndkProxy method1 undefined"
    27.             return "objName  test undefined"
    28.       }
    
    29.       window.ndkProxy.method1("hello", "world", [1.2, -3.4, 123.456], ["Saab", "Volvo", "BMW", undefined], 1.23456, 123789, true, false, 0,  undefined);
    30. }
    
    31. function testNdkProxyObjMethod2() {
    32.       if (window.ndkProxy == undefined) {
    33.             document.getElementById("webDemo").innerHTML = "ndkProxy undefined"
    34.             return "objName undefined"
    35.       }
    
    36.       if (window.ndkProxy.method2 == undefined) {
    37.             document.getElementById("webDemo").innerHTML = "ndkProxy method2 undefined"
    38.             return "objName  test undefined"
    39.       }
    
    40.     var student = {
    41.             name:"zhang",
    42.             sex:"man",
    43.             age:25
    44.     };
    45.     var cars = [student, 456, false, 4.567];
    46.     let params = "[\"{\\\"scope\\\"]";
    
    47.     window.ndkProxy.method2("hello", "world", false, cars, params);
    48. }
    
    49. function runJSRetStr(data) {
    50.     const d = new Date();
    51.     let time = d.getTime();
    52.     return JSON.stringify(time)
    53. }
    54. </script>
    55. </html>
    
- ArkTS侧代码
    
    1. // entry/src/main/ets/pages/Index.ets
    2. import testNapi from 'libentry.so';
    3. import { webview } from '@kit.ArkWeb';
    
    4. class testObj {
    5.   constructor() {
    6.   }
    
    7.   test(): string {
    8.     console.info('ArkUI Web Component');
    9.     return "ArkUI Web Component";
    10.   }
    
    11.   toString(): void {
    12.     console.info('Web Component toString');
    13.   }
    14. }
    
    15. @Entry
    16. @Component
    17. struct Index {
    18.   webTag: string = 'ArkWeb1';
    19.   controller: webview.WebviewController = new webview.WebviewController(this.webTag);
    20.   @State testObjtest: testObj = new testObj();
    
    21.   aboutToAppear() {
    22.     console.info("aboutToAppear")
    23.     //初始化web ndk
    24.     testNapi.nativeWebInit(this.webTag);
    25.   }
    
    26.   build() {
    27.     Column() {
    28.       Row() {
    29.         Button('runJS hello')
    30.           .fontSize(12)
    31.           .onClick(() => {
    32.             testNapi.runJavaScript(this.webTag, "runJSRetStr(\"" + "hello" + "\")");
    33.           })
    34.       }.height('20%')
    
    35.       Row() {
    36.         Web({ src: $rawfile('runJS.html'), controller: this.controller })
    37.           .javaScriptAccess(true)
    38.           .fileAccess(true)
    39.           .onControllerAttached(() => {
    40.             console.error("ndk onControllerAttached webId: " + this.controller.getWebId());
    41.           })
    42.       }.height('80%')
    43.     }
    44.   }
    45. }
    
- Node-API侧暴露ArkTS接口
    
    1. // entry/src/main/cpp/types/libentry/index.d.ts
    2. export const nativeWebInit: (webName: string) => void;
    3. export const runJavaScript: (webName: string, jsCode: string) => void;
    
- Node-API侧编译配置entry/src/main/cpp/CMakeLists.txt
    
    1. # the minimum version of CMake.
    2. cmake_minimum_required(VERSION 3.4.1)
    3. project(NDKJSBridg)
    
    4. set(NATIVERENDER_ROOT_PATH ${CMAKE_CURRENT_SOURCE_DIR})
    
    5. if(DEFINED PACKAGE_FIND_FILE)
    6.     include(${PACKAGE_FIND_FILE})
    7. endif()
    
    8. include_directories(${NATIVERENDER_ROOT_PATH}
    9.                     ${NATIVERENDER_ROOT_PATH}/include)
    
    10. add_library(entry SHARED hello.cpp jsbridge_object.cpp)
    
    11. find_library(
    12.     # Sets the name of the path variable.
    13.     hilog-lib
    14.     # Specifies the name of the NDK library that
    15.     # you want CMake to locate.
    16.     hilog_ndk.z
    17. )
    
    18. target_link_libraries(entry PUBLIC libace_napi.z.so ${hilog-lib} libohweb.so)
    
- Node-API层代码
    
    1. // entry/src/main/cpp/hello.cpp
    2. #include "napi/native_api.h"
    3. #include <bits/alltypes.h>
    4. #include <memory>
    5. #include <string>
    6. #include <sys/types.h>
    7. #include <thread>
    
    8. #include "hilog/log.h"
    9. #include "web/arkweb_interface.h"
    10. #include "jsbridge_object.h"
    
    11. constexpr unsigned int LOG_PRINT_DOMAIN = 0xFF00;
    12. std::shared_ptr<JSBridgeObject> jsbridge_object_ptr = nullptr;
    13. static ArkWeb_ControllerAPI *controller = nullptr;
    14. static ArkWeb_ComponentAPI *component = nullptr;
    
    15. // 发送JS脚本到H5侧执行，该方法为执行结果的回调。
    16. static void RunJavaScriptCallback(const char *webTag, const char *result, void *userData) {
    17.     OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk RunJavaScriptCallback webTag:%{public}s", webTag);
    18.     if (!userData) {
    19.         OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk RunJavaScriptCallback userData is nullptr");
    20.         return;
    21.     }
    22.     std::weak_ptr<JSBridgeObject> jsb_weak_ptr = *static_cast<std::weak_ptr<JSBridgeObject> *>(userData);
    23.     if (auto jsb_ptr = jsb_weak_ptr.lock()) {
    24.         jsb_ptr->RunJavaScriptCallback(result);
    25.     } else {
    26.         OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb",
    27.                      "ndk RunJavaScriptCallback jsb_weak_ptr lock failed");
    28.     }
    29. }
    
    30. // 示例代码 ，注册了1个对象，2个方法
    31. static void ProxyMethod1(const char *webTag, const ArkWeb_JavaScriptBridgeData *dataArray, size_t arraySize, void *userData) {
    32.     OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk ProxyMethod1 webTag:%{public}s", webTag);
    33.     if (!userData) {
    34.         OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk ProxyMethod1 userData is nullptr");
    35.         return;
    36.     }
    37.     std::weak_ptr<JSBridgeObject> jsb_weak_ptr = *static_cast<std::weak_ptr<JSBridgeObject> *>(userData);
    38.     if (auto jsb_ptr = jsb_weak_ptr.lock()) {
    39.         jsb_ptr->ProxyMethod1(dataArray, arraySize);
    40.     } else {
    41.         OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk ProxyMethod1 jsb_weak_ptr lock failed");
    42.     }
    43. }
    
    44. static void ProxyMethod2(const char *webTag, const ArkWeb_JavaScriptBridgeData *dataArray, size_t arraySize, void *userData) {
    45.     OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk ProxyMethod2 webTag:%{public}s", webTag);
    46.     if (!userData) {
    47.         OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk ProxyMethod2 userData is nullptr");
    48.         return;
    49.     }
    50.     std::weak_ptr<JSBridgeObject> jsb_weak_ptr = *static_cast<std::weak_ptr<JSBridgeObject> *>(userData);
    
    51.     std::string jsCode = "runJSRetStr()";
    52.     ArkWeb_JavaScriptObject object = {(uint8_t *)jsCode.c_str(), jsCode.size(),
    53.                                      &JSBridgeObject::StaticRunJavaScriptCallback,
    54.                                      static_cast<void *>(jsbridge_object_ptr->GetWeakPtr())};
    55.     controller->runJavaScript(webTag, &object);
    
    56.     if (auto jsb_ptr = jsb_weak_ptr.lock()) {
    57.         jsb_ptr->ProxyMethod2(dataArray, arraySize);
    58.     } else {
    59.         OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk ProxyMethod2 jsb_weak_ptr lock failed");
    60.     }
    61. }
    
    62. void ValidCallback(const char *webTag, void *userData) {
    63.     OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk ValidCallback webTag: %{public}s", webTag);
    64.     if (!userData) {
    65.         OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk ValidCallback userData is nullptr");
    66.         return;
    67.     }
    68.     std::weak_ptr<JSBridgeObject> jsb_weak_ptr = *static_cast<std::weak_ptr<JSBridgeObject> *>(userData);
    69.     if (auto jsb_ptr = jsb_weak_ptr.lock()) {
    70.         jsb_ptr->SaySomething("ValidCallback");
    71.     } else {
    72.         OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk ValidCallback jsb_weak_ptr lock failed");
    73.     }
    
    74.     // 注册对象
    75.     OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk RegisterJavaScriptProxy begin");
    76.     ArkWeb_ProxyMethod method1 = {"method1", ProxyMethod1, static_cast<void *>(jsbridge_object_ptr->GetWeakPtr())};
    77.     ArkWeb_ProxyMethod method2 = {"method2", ProxyMethod2, static_cast<void *>(jsbridge_object_ptr->GetWeakPtr())};
    78.     ArkWeb_ProxyMethod methodList[2] = {method1, method2};
    79.     // 调用ndk接口注册对象
    80.     // 如此注册的情况下，在H5页面就可以使用proxy.method1、proxy.method2调用此文件下的ProxyMethod1和ProxyMethod2方法了
    81.     ArkWeb_ProxyObject proxyObject = {"ndkProxy", methodList, 2};
    82.     controller->registerJavaScriptProxy(webTag, &proxyObject);
    
    83.     OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk RegisterJavaScriptProxy end");
    84. }
    
    85. void LoadStartCallback(const char *webTag, void *userData) {
    86.     OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk LoadStartCallback webTag: %{public}s", webTag);
    87.     if (!userData) {
    88.         OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk LoadStartCallback userData is nullptr");
    89.         return;
    90.     }
    91.     std::weak_ptr<JSBridgeObject> jsb_weak_ptr = *static_cast<std::weak_ptr<JSBridgeObject> *>(userData);
    92.     if (auto jsb_ptr = jsb_weak_ptr.lock()) {
    93.         jsb_ptr->SaySomething("LoadStartCallback");
    94.     } else {
    95.         OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk LoadStartCallback jsb_weak_ptr lock failed");
    96.     }
    97. }
    
    98. void LoadEndCallback(const char *webTag, void *userData) {
    99.     OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk LoadEndCallback webTag: %{public}s", webTag);
    100.     if (!userData) {
    101.         OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk LoadEndCallback userData is nullptr");
    102.         return;
    103.     }
    104.     std::weak_ptr<JSBridgeObject> jsb_weak_ptr = *static_cast<std::weak_ptr<JSBridgeObject> *>(userData);
    105.     if (auto jsb_ptr = jsb_weak_ptr.lock()) {
    106.         jsb_ptr->SaySomething("LoadEndCallback");
    107.     } else {
    108.         OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk LoadEndCallback jsb_weak_ptr lock failed");
    109.     }
    110. }
    
    111. void DestroyCallback(const char *webTag, void *userData) {
    112.     OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk DestroyCallback webTag: %{public}s", webTag);
    113.     if (!userData) {
    114.         OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk DestroyCallback userData is nullptr");
    115.         return;
    116.     }
    117.     std::weak_ptr<JSBridgeObject> jsb_weak_ptr = *static_cast<std::weak_ptr<JSBridgeObject> *>(userData);
    118.     if (auto jsb_ptr = jsb_weak_ptr.lock()) {
    119.         jsb_ptr->SaySomething("DestroyCallback");
    120.     } else {
    121.         OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk DestroyCallback jsb_weak_ptr lock failed");
    122.     }
    123. }
    
    124. void SetComponentCallback(ArkWeb_ComponentAPI * component, const char* webTagValue) {
    125.     if (!ARKWEB_MEMBER_MISSING(component, onControllerAttached)) {
    126.         component->onControllerAttached(webTagValue, ValidCallback,
    127.                                         static_cast<void *>(jsbridge_object_ptr->GetWeakPtr()));
    128.     } else {
    129.         OH_LOG_Print(LOG_APP, LOG_ERROR, LOG_PRINT_DOMAIN, "ArkWeb", "component onControllerAttached func not exist");
    130.     }
    
    131.     if (!ARKWEB_MEMBER_MISSING(component, onPageBegin)) {
    132.         component->onPageBegin(webTagValue, LoadStartCallback,
    133.                                         static_cast<void *>(jsbridge_object_ptr->GetWeakPtr()));
    134.     } else {
    135.         OH_LOG_Print(LOG_APP, LOG_ERROR, LOG_PRINT_DOMAIN, "ArkWeb", "component onPageBegin func not exist");
    136.     }
    
    137.     if (!ARKWEB_MEMBER_MISSING(component, onPageEnd)) {
    138.         component->onPageEnd(webTagValue, LoadEndCallback,
    139.                                         static_cast<void *>(jsbridge_object_ptr->GetWeakPtr()));
    140.     } else {
    141.         OH_LOG_Print(LOG_APP, LOG_ERROR, LOG_PRINT_DOMAIN, "ArkWeb", "component onPageEnd func not exist");
    142.     }
    
    143.     if (!ARKWEB_MEMBER_MISSING(component, onDestroy)) {
    144.         component->onDestroy(webTagValue, DestroyCallback,
    145.                                         static_cast<void *>(jsbridge_object_ptr->GetWeakPtr()));
    146.     } else {
    147.         OH_LOG_Print(LOG_APP, LOG_ERROR, LOG_PRINT_DOMAIN, "ArkWeb", "component onDestroy func not exist");
    148.     }
    149. }
    
    150. // 解析存储webTag
    151. static napi_value NativeWebInit(napi_env env, napi_callback_info info) {
    152.     OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk NativeWebInit start");
    153.     size_t argc = 1;
    154.     napi_value args[1] = {nullptr};
    155.     napi_get_cb_info(env, info, &argc, args, nullptr, nullptr);
    156.     // 获取第一个参数webTag
    157.     size_t webTagSize = 0;
    158.     napi_get_value_string_utf8(env, args[0], nullptr, 0, &webTagSize);
    159.     char *webTagValue = new (std::nothrow) char[webTagSize + 1];
    160.     size_t webTagLength = 0;
    161.     napi_get_value_string_utf8(env, args[0], webTagValue, webTagSize + 1, &webTagLength);
    162.     OH_LOG_Print(LOG_APP, LOG_ERROR, LOG_PRINT_DOMAIN, "ArkWeb", "ndk NativeWebInit webTag:%{public}s", webTagValue);
    
    163.     // 将webTag保存在实例对象中
    164.     jsbridge_object_ptr = std::make_shared<JSBridgeObject>(webTagValue);
    165.     if (jsbridge_object_ptr)
    166.         jsbridge_object_ptr->Init();
    
    167.     controller = reinterpret_cast<ArkWeb_ControllerAPI *>(OH_ArkWeb_GetNativeAPI(ARKWEB_NATIVE_CONTROLLER));
    168.     component = reinterpret_cast<ArkWeb_ComponentAPI *>(OH_ArkWeb_GetNativeAPI(ARKWEB_NATIVE_COMPONENT));
    169.     SetComponentCallback(component, webTagValue);
    
    170.     OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk NativeWebInit end");
    171.     delete[] webTagValue;
    172.     return nullptr;
    173. }
    
    174. // 发送JS脚本到H5侧执行
    175. static napi_value RunJavaScript(napi_env env, napi_callback_info info) {
    176.     size_t argc = 2;
    177.     napi_value args[2] = {nullptr};
    178.     napi_get_cb_info(env, info, &argc, args, nullptr, nullptr);
    
    179.     // 获取第一个参数webTag
    180.     size_t webTagSize = 0;
    181.     napi_get_value_string_utf8(env, args[0], nullptr, 0, &webTagSize);
    182.     char *webTagValue = new (std::nothrow) char[webTagSize + 1];
    183.     size_t webTagLength = 0;
    184.     napi_get_value_string_utf8(env, args[0], webTagValue, webTagSize + 1, &webTagLength);
    185.     OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "ndk OH_NativeArkWeb_RunJavaScript webTag:%{public}s",
    186.                  webTagValue);
    
    187.     // 获取第二个参数 jsCode
    188.     size_t bufferSize = 0;
    189.     napi_get_value_string_utf8(env, args[1], nullptr, 0, &bufferSize);
    190.     char *jsCode = new (std::nothrow) char[bufferSize + 1];
    191.     size_t byteLength = 0;
    192.     napi_get_value_string_utf8(env, args[1], jsCode, bufferSize + 1, &byteLength);
    
    193.     OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb",
    194.                  "ndk OH_NativeArkWeb_RunJavaScript jsCode len:%{public}zu", strlen(jsCode));
    
    195.     // 构造runJS执行的结构体
    196.     ArkWeb_JavaScriptObject object = {(uint8_t *)jsCode, bufferSize, &JSBridgeObject::StaticRunJavaScriptCallback,
    197.                                      static_cast<void *>(jsbridge_object_ptr->GetWeakPtr())};
    198.     controller->runJavaScript(webTagValue, &object);
    199.     delete[] webTagValue;
    200.     delete[] jsCode;
    201.     return nullptr;
    202. }
    
    203. EXTERN_C_START
    204. static napi_value Init(napi_env env, napi_value exports) {
    205.     napi_property_descriptor desc[] = {
    206.         {"nativeWebInit", nullptr, NativeWebInit, nullptr, nullptr, nullptr, napi_default, nullptr},
    207.         {"runJavaScript", nullptr, RunJavaScript, nullptr, nullptr, nullptr, napi_default, nullptr},
    208.     };
    209.     napi_define_properties(env, exports, sizeof(desc) / sizeof(desc[0]), desc);
    210.     return exports;
    211. }
    212. EXTERN_C_END
    
    213. static napi_module demoModule = {
    214.     .nm_version = 1,
    215.     .nm_flags = 0,
    216.     .nm_filename = nullptr,
    217.     .nm_register_func = Init,
    218.     .nm_modname = "entry",
    219.     .nm_priv = ((void *)0),
    220.     .reserved = {0},
    221. };
    
    222. extern "C" __attribute__((constructor)) void RegisterEntryModule(void) { napi_module_register(&demoModule); }
    
- Native侧业务代码
    
    1. // entry/src/main/cpp/jsbridge_object.h
    2. #include "web/arkweb_type.h"
    3. #include <string>
    
    4. class JSBridgeObject : public std::enable_shared_from_this<JSBridgeObject> {
    5. public:
    6.     JSBridgeObject(const char* webTag);
    7.     ~JSBridgeObject() = default;
    8.     void Init();
    9.     std::weak_ptr<JSBridgeObject>* GetWeakPtr();
    10.     static void StaticRunJavaScriptCallback(const char *webTag, const ArkWeb_JavaScriptBridgeData *data, void *userData);
    11.     void RunJavaScriptCallback(const char *result);
    12.     void ProxyMethod1(const ArkWeb_JavaScriptBridgeData *dataArray, int32_t arraySize);
    13.     void ProxyMethod2(const ArkWeb_JavaScriptBridgeData *dataArray, int32_t arraySize);
    14.     void SaySomething(const char* say);
    
    15. private:
    16.     std::string webTag_;
    17.     std::weak_ptr<JSBridgeObject> weak_ptr_;
    18. };
    
    19. // entry/src/main/cpp/jsbridge_object.cpp
    20. #include "jsbridge_object.h"
    
    21. #include "hilog/log.h"
    
    22. constexpr unsigned int LOG_PRINT_DOMAIN = 0xFF00;
    
    23. JSBridgeObject::JSBridgeObject(const char *webTag) : webTag_(webTag) {}
    
    24. void JSBridgeObject::Init() { weak_ptr_ = shared_from_this(); }
    
    25. std::weak_ptr<JSBridgeObject> *JSBridgeObject::GetWeakPtr() { return &weak_ptr_; }
    
    26. void JSBridgeObject::StaticRunJavaScriptCallback(const char *webTag, const ArkWeb_JavaScriptBridgeData *data,
    27.                                                  void *userData) {
    28.     OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb",
    29.                  "JSBridgeObject StaticRunJavaScriptCallback webTag:%{public}s", webTag);
    30.     if (!userData) {
    31.         OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb",
    32.                      "JSBridgeObject StaticRunJavaScriptCallback userData is nullptr");
    33.         return;
    34.     }
    35.     std::weak_ptr<JSBridgeObject> jsb_weak_ptr = *static_cast<std::weak_ptr<JSBridgeObject> *>(userData);
    36.     if (auto jsb_ptr = jsb_weak_ptr.lock()) {
    37.         std::string result((char *)data->buffer, data->size);
    38.         jsb_ptr->RunJavaScriptCallback(result.c_str());
    39.     } else {
    40.         OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb",
    41.                      "JSBridgeObject StaticRunJavaScriptCallback jsb_weak_ptr lock failed");
    42.     }
    43. }
    
    44. void JSBridgeObject::RunJavaScriptCallback(const char *result) {
    45.     OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb",
    46.                  "JSBridgeObject OH_NativeArkWeb_RunJavaScript result:%{public}s", result);
    47. }
    
    48. void JSBridgeObject::ProxyMethod1(const ArkWeb_JavaScriptBridgeData *dataArray, int32_t arraySize) {
    49.     OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "JSBridgeObject ProxyMethod1 argc:%{public}d",
    50.                  arraySize);
    51.     for (int i = 0; i < arraySize; i++) {
    52.         std::string result((char *)dataArray[i].buffer, dataArray[i].size);
    53.         OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb",
    54.                      "JSBridgeObject ProxyMethod1 argv[%{public}d]:%{public}s, size:%{public}d", i, result.c_str(),
    55.                      dataArray[i].size);
    56.     }
    57. }
    
    58. void JSBridgeObject::ProxyMethod2(const ArkWeb_JavaScriptBridgeData *dataArray, int32_t arraySize) {
    59.     OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "JSBridgeObject ProxyMethod2 argc:%{public}d",
    60.                  arraySize);
    61.     for (int i = 0; i < arraySize; i++) {
    62.         std::string result((char *)dataArray[i].buffer, dataArray[i].size);
    63.         OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb",
    64.                      "JSBridgeObject ProxyMethod2 argv[%{public}d]:%{public}s, size:%{public}d", i, result.c_str(),
    65.                      dataArray[i].size);
    66.     }
    67. }
    
    68. void JSBridgeObject::SaySomething(const char *say) {
    69.     OH_LOG_Print(LOG_APP, LOG_INFO, LOG_PRINT_DOMAIN, "ArkWeb", "JSBridgeObject SaySomething argc:%{public}s", say);
    70. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-app-page-data-channel "建立应用侧与前端页面数据通道")
# Web组件嵌套滚动

更新时间: 2025-12-16 16:38

Web组件嵌套滚动的典型应用场景为，在页面中，多个独立区域需进行滚动，当用户滚动Web区域内容时，可联动其他滚动区域，实现上下左右全方位滑动页面的嵌套滚动体验。内嵌于可滚动容器（[Grid](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-grid)、[List](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-list)、[Scroll](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-scroll)、[Swiper](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-swiper)、[Tabs](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-tabs)、[WaterFlow](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-waterflow)、[Refresh](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-refresh)、[bindSheet](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-sheet-transition#bindsheet)）中的Web组件，接收到滑动手势事件后，需要设置ArkUI的[NestedScrollMode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-appendix-enums#nestedscrollmode10)枚举属性，实现Web组件与ArkUI可滚动容器的嵌套滚动。

Web组件嵌套滚动可通过[方案1：使用nestedScroll属性实现嵌套滚动](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-nested-scrolling#%E4%BD%BF%E7%94%A8nestedscroll%E5%B1%9E%E6%80%A7%E5%AE%9E%E7%8E%B0%E5%B5%8C%E5%A5%97%E6%BB%9A%E5%8A%A8)或[方案2：滚动偏移量由滚动父组件统一派发](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-nested-scrolling#%E6%BB%9A%E5%8A%A8%E5%81%8F%E7%A7%BB%E9%87%8F%E7%94%B1%E6%BB%9A%E5%8A%A8%E7%88%B6%E7%BB%84%E4%BB%B6%E7%BB%9F%E4%B8%80%E6%B4%BE%E5%8F%91)两个方案实现，方案的选择应取决于应用嵌套滚动的具体业务场景。如果只是简单的Web组件与其他父组件联动滚动建议通过方案1实现；如果应用需要自定义控制Web组件和其他滚动组件滚动，以及一些复杂场景建议使用方案2。

说明

如果Web组件用到了全量展开的场景（layoutMode为WebLayoutMode.FIT_CONTENT），需要显式指明渲染模式(RenderMode.SYNC_RENDER)，详见[layoutMode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#layoutmode11)。

## 使用nestedScroll属性实现嵌套滚动

使用Web组件[nestedScroll](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#nestedscroll11)属性来设置上下左右四个方向，或者设置向前、向后两个方向的嵌套滚动模式，实现与父组件的滚动联动，同时也允许在过程中动态改变嵌套滚动的模式。

**完整代码**

1. // xxx.ets
2. import { webview } from '@kit.ArkWeb';

3. @Entry
4. @ComponentV2
5. struct NestedScroll {
6.   private scrollerForScroll: Scroller = new Scroller()
7.   private listScroller: Scroller = new Scroller()
8.   controller: webview.WebviewController = new webview.WebviewController();
9.   @Local arr: Array<number> = []

10.   aboutToAppear(): void {
11.     for (let i = 0; i < 10; i++) {
12.       this.arr.push(i)
13.     }
14.   }

15.   build() {
16.     Scroll(this.scrollerForScroll) {
17.       Column() {
18.         Web({ src: $rawfile("index.html"), controller: this.controller })
19.           .nestedScroll({
20.             scrollUp: NestedScrollMode.PARENT_FIRST,//向上滚动父组件优先
21.             scrollDown: NestedScrollMode.SELF_FIRST,//向下滚动子组件优先
22.           }).height("100%")
23.         Repeat<number>(this.arr)
24.           .each((item: RepeatItem<number>) => {
25.             Text("Scroll Area")
26.               .width("100%")
27.               .height("40%")
28.               .backgroundColor(0X330000FF)
29.               .fontSize(16)
30.               .textAlign(TextAlign.Center)
31.           })
32.       }
33.     }
34.   }
35. }

加载的html文件。

1. <!-- index.html -->
2. <!DOCTYPE html>
3. <html>
4. <head>
5.     <meta name="viewport" id="viewport" content="width=device-width, initial-scale=1.0">
6.     <style>
7.         .blue {
8.           background-color: lightblue;
9.         }
10.         .green {
11.           background-color: lightgreen;
12.         }
13.         .blue, .green {
14.          font-size:16px;
15.          height:200px;
16.          text-align: center;       /* 水平居中 */
17.          line-height: 200px;       /* 垂直居中（值等于容器高度） */
18.         }
19.     </style>
20. </head>
21. <body>
22. <div class="blue" >webArea</div>
23. <div class="green">webArea</div>
24. <div class="blue">webArea</div>
25. <div class="green">webArea</div>
26. <div class="blue">webArea</div>
27. <div class="green">webArea</div>
28. <div class="blue">webArea</div>
29. </body>
30. </html>

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163827.30306954501521552657679920908106:50001231000000:2800:22CF7F0F017E30BE2AB83AFF5D367271D1ED6CA31D5B8F1730B29FDE5B6CCE03.gif)

## 滚动偏移量由滚动父组件统一派发

**实现思路**

1. 手指向上滑动：
    
    (1) 如果Web页面没有滚动到底部，Scroll组件将滚动偏移量派发给Web，Scroll组件自身不滚动。
    
    (2) 如果Web页面滚动至底部，而Scroll组件尚未滚动至底部，则仅Scroll组件自身滚动，不向Web组件和List组件传递滚动位移。
    
    (3) 如果Scroll组件滚动到底部，则滚动偏移量派发给List组件，Scroll组件自身不滚动。
    
2. 手指向下滑动：
    
    (1) 如果List组件没有滚动到顶部，则Scroll组件将滚动偏移量派发给List组件，Scroll组件自身不滚动。
    
    (2) 当List组件滚动至顶部，而Scroll组件未到达顶部时，Scroll组件将自行滚动，滚动偏移量不会派发给List组件和Web组件。
    
    (3) 如果Scroll组件滚动到顶部，则滚动偏移量派发给Web，Scroll组件自身不滚动。
    

**关键实现**

1. 如何禁用Web组件滚动手势。
    
    (1) 首先调用Web组件滚动控制器方法，设置Web禁用触摸（[setScrollable](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#setscrollable12)）的滚动。
    
    1. this.webController.setScrollable(false, webview.ScrollType.EVENT);
    
    (2) 再使用[onGestureRecognizerJudgeBegin](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-gesture-blocking-enhancement#ongesturerecognizerjudgebegin13)方法，禁止Web组件自带的滑动手势触发。
    
    2. .onGestureRecognizerJudgeBegin((event: BaseGestureEvent, current: GestureRecognizer, otherArray<GestureRecognizer>) => {
    3.   if (current.isBuiltIn() && current.getType() == GestureControl.GestureType.PAN_GESTURE) {
    4.     return GestureJudgeResult.REJECT;
    5.   }
    6.   return GestureJudgeResult.CONTINUE;
    7. })
    
2. 如何禁止[List](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-list)组件的手势。
    
    1.   .enableScrollInteraction(false)
    
3. 如何检测List组件、Scroll组件是否滚动到边界。
    
    (1) 滚动到上边界：scroller.currentOffset().yOffset <= 0;
    
    (2) 滚动到下边界：scroller.isAtEnd() == true;
    
4. 如何检测Web组件是否滚动到边界。
    
    (1) 获取Web组件自身高度、内容高度和当前滚动偏移量来判定。
    
    (2) 判断Web组件是否滚动到顶部：webController.getPageOffset().y == 0;
    
    (3) 判断Web组件是否滚动到底部：webController.getPageOffset().y + this.webHeight >= webController.getPageHeight();
    
    (4) 获取Web组件自身高度：webController.[getPageHeight()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#getpageheight);
    
    (5) 获取Web组件窗口高度：webController?.[runJavaScriptExt](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#runjavascriptext10)('window. innerHeight');
    
    (6) 获取Web组件的滚动偏移量：webController.[getPageOffset()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#getpageoffset20);
    
5. 如何让Scroll组件不滚动。
    
    Scroll组件绑定[onScrollFrameBegin](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-scroll#onscrollframebegin9)事件，将剩余滚动偏移量返回0，scroll组件就不滚动，也不会停止惯性滚动动画。
    
6. 滚动偏移量如何派发给List。
    
    1.   this.listScroller.scrollBy(0, offset)
    
7. 滚动偏移量如何派发给Web。
    
    1.   this.webController.scrollBy(0, offset)
    
8. 设置Web组件[bypassVsyncCondition](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#bypassvsynccondition20)为WebBypassVsyncCondition.SCROLLBY_FROM_ZERO_OFFSET，加快Web组件首帧滚动绘制。
    
    1.   .bypassVsyncCondition(WebBypassVsyncCondition.SCROLLBY_FROM_ZERO_OFFSET)
    

**完整代码**

1. // xxx.ets
2. import { webview } from '@kit.ArkWeb';

3. @Entry
4. @ComponentV2
5. struct Index {
6.   private scroller:Scroller = new Scroller()
7.   private listScroller:Scroller = new Scroller()
8.   private webController: webview.WebviewController = new webview.WebviewController()
9.   private isWebAtEnd:boolean = false
10.   private webHeight:number = 0
11.   @Local arr: Array<number> = []

12.   aboutToAppear(): void {
13.     for (let i = 0; i < 10; i++) {
14.       this.arr.push(i)
15.     }
16.   }

17.   getWebHeight() {
18.     try {
19.       this.webController?.runJavaScriptExt('window.innerHeight',
20.         (error, result) => {
21.           if (error || !result) {
22.             return;
23.           }
24.           if (result.getType() === webview.JsMessageType.NUMBER) {
25.             this.webHeight = result.getNumber()
26.           }
27.         })
28.     } catch (error) {
29.     }
30.   }

31.   checkScrollBottom() {
32.       this.isWebAtEnd = false;
33.       if (this.webController.getPageOffset().y + this.webHeight >= this.webController.getPageHeight()) {
34.         this.isWebAtEnd = true;
35.       }
36.   }

37.   build() {
38.     Scroll(this.scroller) {
39.       Column() {
40.         Web({
41.           src: $rawfile("index.html"),
42.           controller: this.webController,
43.         }).height("100%")
44.           .bypassVsyncCondition(WebBypassVsyncCondition.SCROLLBY_FROM_ZERO_OFFSET)
45.           .onPageEnd(() => {
46.             this.webController.setScrollable(false, webview.ScrollType.EVENT);
47.             this.getWebHeight();
48.           })
49.             // 在识别器即将要成功时，根据当前组件状态，设置识别器使能状态
50.           .onGestureRecognizerJudgeBegin((event: BaseGestureEvent, current: GestureRecognizer, others: Array<GestureRecognizer>) => {
51.             if (current.isBuiltIn() && current.getType() == GestureControl.GestureType.PAN_GESTURE) {
52.               return GestureJudgeResult.REJECT;
53.             }
54.             return GestureJudgeResult.CONTINUE;
55.           })
56.         List({ scroller: this.listScroller }) {
57.           Repeat<number>(this.arr)
58.             .each((item: RepeatItem<number>) => {
59.               ListItem() {
60.                 Text("Scroll Area")
61.                   .width("100%")
62.                   .height("40%")
63.                   .backgroundColor(0X330000FF)
64.                   .fontSize(16)
65.                   .textAlign(TextAlign.Center)
66.               }
67.             })
68.         }.height("100%")
69.         .maintainVisibleContentPosition(true)
70.         .enableScrollInteraction(false)
71.       }
72.     }
73.     .onScrollFrameBegin((offset: number, state: ScrollState)=>{
74.       this.checkScrollBottom();
75.       if (offset > 0) {
76.         if (!this.isWebAtEnd) {
77.           this.webController.scrollBy(0, offset)
78.           return {offsetRemain:0}
79.         } else if (this.scroller.isAtEnd()) {
80.           this.listScroller.scrollBy(0, offset)
81.           return {offsetRemain:0}
82.         }
83.       } else if (offset < 0) {
84.         if (this.listScroller.currentOffset().yOffset > 0) {
85.           this.listScroller.scrollBy(0, offset)
86.           return {offsetRemain:0}
87.         } else if (this.scroller.currentOffset().yOffset <= 0) {
88.           this.webController.scrollBy(0, offset)
89.           return {offsetRemain:0}
90.         }
91.       }
92.       return {offsetRemain:offset}
93.     })
94.   }
95. }

加载的html文件。

1. <!-- index.html -->
2. <!DOCTYPE html>
3. <html>
4. <head>
5.     <meta name="viewport" id="viewport" content="width=device-width, initial-scale=1.0">
6.     <style>
7.         .blue {
8.           background-color: lightblue;
9.         }
10.         .green {
11.           background-color: lightgreen;
12.         }
13.         .blue, .green {
14.          font-size:16px;
15.          height:200px;
16.          text-align: center;       /* 水平居中 */
17.          line-height: 200px;       /* 垂直居中（值等于容器高度） */
18.         }
19.     </style>
20. </head>
21. <body>
22. <div class="blue" >webArea</div>
23. <div class="green">webArea</div>
24. <div class="blue">webArea</div>
25. <div class="green">webArea</div>
26. <div class="blue">webArea</div>
27. <div class="green">webArea</div>
28. <div class="blue">webArea</div>
29. </body>
30. </html>

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163827.33561163488343677995706375830943:50001231000000:2800:776BE430EFE52FFB1F2EA195DA35A92B9220B3612664BEB467E9B6F0A8920C8B.gif)

## 示例代码

- [Web组件嵌套滑动](https://gitcode.com/harmonyos_samples/web-scroller)

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-manage-page-interaction "管理网页交互")
