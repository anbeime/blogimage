# UI开发 (兼容JS的类Web开发范式)概述

更新时间: 2025-12-16 16:38

兼容JS的类Web开发范式的方舟开发框架，采用经典的[兼容JS的类Web开发范式API](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkui-js-full-comp)、CSS、JavaScript三段式开发方式。使用HML标签文件进行布局搭建，使用CSS文件进行样式描述，使用JavaScript文件进行逻辑处理。UI组件与数据之间通过单向数据绑定的方式建立关联，当数据发生变化时，UI界面自动触发更新。此种开发方式，更接近Web前端开发者的使用习惯，快速将已有的Web应用改造成方舟开发框架应用。主要适用于界面较为简单的中小型应用开发。

请参考[兼容JS的类Web开发范式API](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkui-js-full-comp)文档，全面地了解组件，更好地开发应用。

## 整体架构

兼容JS的类Web开发范式的方舟开发框架，包括应用层（Application）、前端框架层（Framework）、引擎层（Engine）和平台适配层（Porting Layer）。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163826.87161268712573647358554934765003:50001231000000:2800:DC6402049160CFB70761418585826AAC95814027928512EDF74C7AA40FE093B7.png)

- **Application**
    
    应用层表示开发者开发的FA应用，这里的FA应用特指JS FA应用。
    
- **Framework**
    
    前端框架层主要完成前端页面解析，并提供MVVM（Model-View-ViewModel）开发模式、页面路由机制和自定义组件等能力。
    
- **Engine**
    
    引擎层主要提供动画解析、DOM（Document Object Model）树构建、布局计算、渲染命令构建与绘制、事件管理等能力。
    
- **Porting Layer**
    
    适配层主要对平台层进行抽象，提供抽象接口，可以对接到系统平台。比如：事件对接、渲染管线对接和系统生命周期对接等。
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-js-dev "UI开发 (兼容JS的类Web开发范式)")
# 文件组织

更新时间: 2025-12-16 16:39

## 目录结构

JS FA应用的JS模块（entry/src/main/js/module）的典型开发目录结构如下：

**图1** 目录结构

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163901.94475806346348944175129890629900:50001231000000:2800:11650664C85C3E4C3DBDB7B042DE033B3F217BA41A174658D7CC7A5D17D37EDA.png)

**图2** [多实例](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/pageability-launch-type)资源共享目录结构

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163901.06718030243695942345091821639698:50001231000000:2800:B7CA2374809BEC973645AE3AF485B52F63B976E7F41B677CCC5DCC18DBC9E52E.png)

目录结构中文件分类如下：

- .hml结尾的HML模板文件，描述当前页面的文件布局结构。
    
- .css结尾的CSS样式文件，描述页面样式。
    
- .js结尾的JS文件，处理页面间的交互。
    

各个文件夹的作用：

- app.js文件用于全局JavaScript逻辑和应用生命周期管理，详见[app.js](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/js-framework-js-file)。
    
- pages目录用于存放所有组件页面。
    
- common目录用于存放公共资源文件，比如：媒体资源，自定义组件和JS文件。
    
- resources目录用于存放资源配置文件，比如：多分辨率加载等配置文件，详见[资源限定与访问](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/js-framework-resource-restriction)章节。
    
- share目录用于配置多个实例共享的资源内容，比如：share中的图片和JSON文件可被default1和default2实例共享。
    

说明

- i18n和resources文件夹不可重命名。
    
- 如果share目录中的资源和实例(default)中的资源文件同名且目录一致时，实例中资源的优先级高于share中资源的优先级。
    
- share目录当前不支持i18n。
    
- 在使用DevEco Studio进行应用开发时，目录结构中的可选文件夹需要开发者根据实际情况自行创建。
    

## 文件访问规则

应用资源可通过绝对路径或相对路径的方式进行访问，绝对路径以"/"开头，相对路径以"./"或"../"。具体访问规则如下：

- 引用代码文件，推荐使用相对路径，比如：../common/utils.js。
    
- 引用资源文件，推荐使用绝对路径。比如：/common/xxx.png。
    
- 公共代码文件和资源文件推荐放在common下，通过以上两条规则进行访问。
    
- CSS样式文件中通过url()函数创建<url>数据类型，如：url(/common/xxx.png)。
    

说明

当代码文件A需要引用代码文件B时：

- 如果代码文件A和文件B位于同一目录，则代码文件B引用资源文件时可使用相对路径，也可使用绝对路径。
    
- 如果代码文件A和文件B位于不同目录，则代码文件B引用资源文件时必须使用绝对路径。因为Webpack打包时，代码文件B的目录会发生变化。
    
- 在js文件中通过数据绑定的方式指定资源文件路径时，必须使用绝对路径。
    

## 媒体文件格式

**表1** 支持的图片格式

|格式|支持的文件类型|
|:--|:--|
|BMP|.bmp|
|GIF|.gif|
|JPEG|.jpg|
|PNG|.png|
|WebP|.webp|

**表2** 支持的视频格式

|格式|支持的文件类型|
|:--|:--|
|H.264 AVC|.3gp|
|Baseline Profile (BP)|.mp4|

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/js-framework-overview "框架说明")
# js标签配置

更新时间: 2025-12-16 16:39

js标签用于配置实例名称、页面路由和窗口样式信息。

|标签|类型|默认值|必填|描述|
|:--|:--|:--|:--|:--|
|name|string|default|是|标识JS实例的名字。|
|pages|Array|-|是|路由信息，详见“**[pages](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/js-framework-js-tag#pages)**”。|
|window|Object|-|否|窗口信息，详见“**[Window](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/js-framework-js-tag#window)**”。|

说明

name、pages和window等标签配置需在配置文件（config.json）中的“js”标签中完成设置。

## pages

定义每个页面的路由信息，每个页面由页面路径和页面名组成，页面的文件名即为页面名，例如：

1. {
2.     // ...
3.     "pages": [
4.         "pages/index/index",
5.         "pages/detail/detail"
6.     ]
7.     // ...
8. }

说明

- pages列表中第一个页面是应用的首页，即entry入口。
    
- 页面文件名不能使用组件名称，比如：text.hml、button.hml等。
    

## window

window用于定义与显示窗口相关的配置。屏幕适配问题可通过以下两种方式配置：

- 指定designWidth（屏幕逻辑宽度），所有与大小相关的样式（例如width、font-size）均以designWidth和实际屏幕宽度的比例进行缩放，例如在designWidth为720时，如果设置width为100px时，在实际宽度为1440物理像素的屏幕上，width实际渲染像素为200物理像素。
    
- 设置autoDesignWidth为true，此时designWidth字段将会被忽略，渲染组件和布局时按屏幕密度进行缩放。屏幕逻辑宽度由设备宽度和屏幕密度自动计算得出，在不同设备上可能不同，请使用相对布局来适配多种设备。例如：在466*466分辨率，320dpi的设备上，屏幕密度为2（以160dpi为基准），1px等于渲染出的2物理像素。
    
    说明
    
    1. 组件样式中<length>类型的默认值，基于屏幕密度进行计算和绘制。例如：在屏幕密度为2（以160dpi为基准）的设备上，默认<length>为1px时，设备上实际渲染出2物理像素。
        
    2. autoDesignWidth、designWidth的设置不影响默认值计算方式和绘制结果。
        
    

|属性|类型|必填|缺省值|描述|
|:--|:--|:--|:--|:--|
|designWidth|number|否|720|页面显示设计时的参考值，实际显示效果基于设备宽度与参考值之间的比例进行缩放。|
|autoDesignWidth|boolean|否|false|页面设计基准宽度是否自动计算。<br><br>true表示页面设计基准宽度自动计算，false表示页面设计基准宽度不自动计算。<br><br>当设为true时，designWidth将会被忽略，设计基准宽度由设备宽度与屏幕密度计算得出。|

示例如下：

1. {
2.     // ...
3.     "window": {
4.         "designWidth": 720,
5.         "autoDesignWidth": false
6.     }
7.     // ...
8. }

## 示例

1. {
2.   "app": {
3.     "bundleName": "com.example.player",
4.     "version": {
5.         "code": 1,
6.         "name": "1.0"
7.     },
8.     "vendor": "example"
9.   },
10.   "module": {
11.       // ...
12.       "js": [
13.       {
14.           "name": "default",
15.           "pages": [
16.               "pages/index/index",
17.               "pages/detail/detail"
18.           ],
19.           "window": {
20.               "designWidth": 720,
21.               "autoDesignWidth": false
22.           }
23.       }
24.       ],
25.       "abilities": [
26.       {
27.           // ...
28.       }
29.     ]
30.   }
31. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/js-framework-file "文件组织")
# app.js

更新时间: 2025-12-16 16:39

## 应用生命周期

每个应用可以在app.js自定义应用级[生命周期](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/js-framework-lifecycle)的实现逻辑，以下示例仅在生命周期函数中打印对应日志：

1. // app.js
2. export default {
3.     onCreate() {
4.         console.info('Application onCreate');
5.     },

6.     onDestroy() {
7.         console.info('Application onDestroy');
8.     },
9. }

## 应用对象6+

|属性|类型|描述|
|:--|:--|:--|
|getApp|Function|提供getApp()全局方法，可以在自定义js文件中获取app.js中暴露的对象。|

示例如下：

1. // app.js
2. export default {
3.     data: {
4.         test: "by getApp"
5.     },
6.     onCreate() {
7.         console.info('AceApplication onCreate');
8.     },
9.     onDestroy() {
10.         console.info('AceApplication onDestroy');
11.     },
12. }

13. // test.js 自定义逻辑代码
14. export var appData = getApp().data;

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/js-framework-js-tag "js标签配置")
# HML语法参考

更新时间: 2025-12-16 16:40

HML是一套类HTML的标记语言，通过组件，事件构建出页面的内容。页面具备数据绑定、事件绑定、列表渲染、条件渲染和逻辑控制等高级能力。

## 页面结构

1. <!-- xxx.hml -->
2. <div class="item-container">
3.   <text class="item-title">Image Show</text>
4.   <div class="item-content">
5.     <image src="/common/xxx.png" class="image"></image>
6.   </div>
7. </div>

## 数据绑定

1. <!-- xxx.hml -->
2. <div class="container" onclick="changeText">
3.   <text> {{content[1]}} </text>
4. </div>

5. /*xxx.css*/
6. .container{
7.     margin: 200px;
8. }

9. // xxx.js
10. export default {
11.   data: {
12.     content: ['Hello World!', 'Welcome to my world!']
13.   },
14.   changeText: function() {
15.     this.content.splice(1, 1, this.content[0]);
16.   }
17. }

说明

- 针对数组内的数据修改，请使用splice方法生效数据绑定变更。
    
- hml文件中的js表达式不支持ES6语法。
    

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216164014.87707978313311595713163891458635:50001231000000:2800:025E43B439769F0641121890099434212D4957A43534DF1129BC9BD3E4201A6F.png)

## 普通事件绑定

事件通过'on'或者'@'绑定在组件上，当组件触发事件时会执行JS文件中对应的事件处理函数。

事件支持的写法有：

- "funcName"：funcName为事件回调函数名（在JS文件中定义相应的函数实现）。
    
- "funcName(a,b)"：函数参数例如a，b可以是常量，或者是在JS文件中的data中定义的变量（前面不用写this.）。
    
- 示例
    
    1. <!-- xxx.hml -->
    2. <div class="container">
    3.     <text class="title">{{count}}</text>
    4.     <div class="box">
    5.         <input type="button" class="btn" value="increase" onclick="increase" />
    6.         <input type="button" class="btn" value="decrease" @click="decrease" />
    7.         <!-- 传递额外参数 -->
    8.         <input type="button" class="btn" value="double" @click="multiply(2)" />
    9.         <input type="button" class="btn" value="decuple" @click="multiply(10)" />
    10.         <input type="button" class="btn" value="square" @click="multiply(count)" />
    11.     </div>
    12. </div>
    
    13. // xxx.js
    14. export default {
    15.   data: {
    16.     count: 0
    17.   },
    18.   increase() {
    19.     this.count++;
    20.   },
    21.   decrease() {
    22.     this.count--;
    23.   },
    24.   multiply(multiplier) {
    25.     this.count = multiplier * this.count;
    26.   }
    27. };
    
    28. /* xxx.css */
    29. .container {
    30.     display: flex;
    31.     flex-direction: column;
    32.     justify-content: center;
    33.     align-items: center;
    34.     left: 0px;
    35.     top: 0px;
    36.     width: 454px;
    37.     height: 454px;
    38. }
    39. .title {
    40.     font-size: 30px;
    41.     text-align: center;
    42.     width: 200px;
    43.     height: 100px;
    44. }
    45. .box {
    46.     width: 454px;
    47.     height: 200px;
    48.     justify-content: center;
    49.     align-items: center;
    50.     flex-wrap: wrap;
    51. }
    52. .btn {
    53.     width: 200px;
    54.     border-radius: 0;
    55.     margin-top: 10px;
    56.     margin-left: 10px;
    57. }
    

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216164014.55851053259443584131176918244921:50001231000000:2800:9EE8BA0B3DBBDDE13515042203D861B406BD52E4A2BC5579E67F9AB162F995B6.gif)

## 冒泡事件绑定5+

冒泡事件绑定包括：

- 绑定冒泡事件：on:{event}.bubble。on:{event}等价于on:{event}.bubble。
    
- 绑定并阻止冒泡事件向上冒泡：grab:{event}.bubble。grab:{event}等价于grab:{event}.bubble。
    
    说明
    
    冒泡事件是指多个组件嵌套时，组件之间会有层次关系，当这些组件注册了相同的事件时，这个事件会首先运行在该元素上的处理程序，然后运行其父元素上的处理程序，一直向上到其他祖先上的处理程序。如果当一个组件触发了这个事件，它会首先触发该组件的回调函数，然后触发其父元素上的回调函数，然后触发其他祖先上的处理程序。
    
    详细冒泡事件说明参见[通用事件](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-components-common-events)章节。
    
- 示例
    
    1. <!-- xxx.hml -->
    2. <div>
    3.    <!-- 使用事件冒泡模式绑定事件回调函数。5+ -->;
    4.     <div on:touchstart.bubble="touchstartfunc" style="background-color: red; width: 10%; height: 100%"></div>
    5.     <div on:touchstart="touchstartfunc" style="background-color: orange; width: 10%; height: 100%"></div>
    6.     <!-- 绑定事件回调函数，但阻止事件向上传递。5+ -->
    7.     <div grab:touchstart.bubble="touchstartfunc" style="background-color: yellow; width: 10%; height: 100%"></div>
    8.     <div grab:touchstart="touchstartfunc" style="background-color: greenyellow; width: 10%; height: 100%"></div>
    9.     <!-- 使用事件冒泡模式绑定事件回调函数。6+ -->
    10.     <div on:click.bubble="clickfunc" style="background-color: lightskyblue; width: 10%; height: 100%"></div>
    11.     <div on:click="clickfunc" style="background-color: cornflowerblue; width: 10%; height: 100%"></div>
    12.     <!-- 绑定事件回调函数，但阻止事件向上传递。6+ -->
    13.     <div grab:click.bubble="clickfunc" style="background-color: mediumslateblue; width: 10%; height: 100%"></div>
    14.     <div grab:click="clickfunc" style="background-color: purple; width: 10%; height: 100%"></div>
    15. </div>
    
    16. // xxx.js
    17. export default {
    18.     clickfunc: function(e) {
    19.         console.info(e);
    20.     },
    21.     touchstartfunc: function(e) {
    22.         console.info(e);
    23.     },
    24. }
    

说明

采用旧写法(onclick)的事件绑定在最小API版本6以下时采用不冒泡处理，在最小API版本为6及6以上时采用冒泡处理。

## 捕获事件绑定5+

Touch触摸类事件支持捕获，捕获阶段位于冒泡阶段之前，捕获事件先到达父组件然后到达子组件。

捕获事件绑定包括：

- 绑定捕获事件：on:{event}.capture。
    
- 绑定并阻止事件向下传递：grab:{event}.capture。
    
- 示例
    
    1. <!-- xxx.hml -->
    2. <div>
    3.     <!-- 使用事件捕获模式绑定事件回调函数。5+ -->    
    4.     <div on:touchstart.capture="touchstartfunc"></div>
    5.     <!-- 绑定事件回调函数，但阻止事件向下传递。5+ -->
    6.     <div grab:touchstart.capture="touchstartfunc"></div>
    7. </div>
    
    8. // xxx.js
    9. export default {
    10.     touchstartfunc: function(e) {
    11.         console.info(e);
    12.     },
    13. }
    

## 列表渲染

1. <!-- xxx.hml -->
2. <div class="array-container" style="flex-direction: column;margin: 200px;">
3.   <!-- div列表渲染 -->
4.   <!-- 默认$item代表数组中的元素, $idx代表数组中的元素索引 -->
5.   <div for="{{array}}" tid="id" onclick="changeText">
6.     <text>{{$idx}}.{{$item.name}}</text>
7.   </div>
8.   <!-- 自定义元素变量名称 -->
9.   <div for="{{value in array}}" tid="id" onclick="changeText">    
10.     <text>{{$idx}}.{{value.name}}</text>
11.   </div>
12.   <!-- 自定义元素变量、索引名称 -->
13.   <div for="{{(index, value) in array}}" tid="id" onclick="changeText">    
14.     <text>{{index}}.{{value.name}}</text>
15.   </div>
16. </div>

17. // xxx.js
18. export default {
19.   data: {
20.     array: [
21.       {id: 1, name: 'jack', age: 18},
22.       {id: 2, name: 'tony', age: 18},
23.     ],
24.   },
25.   changeText: function() {
26.     if (this.array[1].name === "tony"){
27.       this.array.splice(1, 1, {id:2, name: 'Isabella', age: 18});
28.     } else {
29.       this.array.splice(2, 1, {id:3, name: 'Bary', age: 18});
30.     }
31.   },
32. }

tid属性主要用来加速for循环的重渲染，旨在列表中的数据有变更时，提高重新渲染的效率。tid属性是用来指定数组中每个元素的唯一标识，如果未指定，数组中每个元素的索引为该元素的唯一id。例如上述tid="id"表示数组中的每个元素的id属性为该元素的唯一标识。for循环支持的写法如下：

- for="array"：其中array为数组对象，array的元素变量默认为$item。
    
- for="v in array"：其中v为自定义的元素变量，元素索引默认为$idx。
    
- for="(i, v) in array"：其中元素索引为i，元素变量为v，遍历数组对象array。
    

说明

- 数组中的每个元素必须存在tid指定的数据属性，否则运行时可能会导致异常。
    
- 数组中被tid指定的属性要保证唯一性，如果不是则会造成性能损耗。比如，示例中只有id和name可以作为tid字段，因为它们属于唯一字段。
    
- tid不支持表达式。
    

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216164015.09247884081724128882056278175319:50001231000000:2800:6CB5B423378987B682ACACAEBD9E4ADDEDEBF3EA896A749E4CDCD524A085CA47.gif)

## 条件渲染

条件渲染分为2种：if/elif/else和show。两种写法的区别在于：第一种写法里if为false时，组件不会在vdom中构建，也不会渲染，而第二种写法里show为false时虽然也不渲染，但会在vdom中构建；另外，当使用if/elif/else写法时，节点必须是兄弟节点，否则编译无法通过。实例如下：

1. <!-- xxx.hml -->
2. <div class="container">
3.   <button class="btn" type="capsule" value="toggleShow" onclick="toggleShow"></button>
4.   <button class="btn" type="capsule" value="toggleDisplay" onclick="toggleDisplay"></button>
5.   <text if="{{visible}}"> Hello-world1 </text>
6.   <text elif="{{display}}"> Hello-world2 </text>
7.   <text else> Hello-World </text>
8. </div>

9. /* xxx.css */
10. .container{
11.   flex-direction: column;
12.   align-items: center;
13. }
14. .btn{
15.   width: 280px;
16.   font-size: 26px;
17.   margin: 10px 0;
18. }

19. // xxx.js
20. export default {
21.   data: {
22.     visible: false,
23.     display: true,
24.   },
25.   toggleShow: function() {
26.     this.visible = !this.visible;
27.   },
28.   toggleDisplay: function() {
29.     this.display = !this.display;
30.   }
31. }

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216164015.90642393373052759486416559731988:50001231000000:2800:BBF57F2A588E6E703C2B9402A1BE7D7C0C0E98F30ECAA829BFA4F019864A67F7.gif)

优化渲染：show方法。当show为true时，节点正常渲染；当为false时，仅仅设置display样式为none。

1. <!-- xxx.hml -->
2. <div class="container">
3.   <button class="btn" type="capsule" value="toggle" onclick="toggle"></button>
4.   <text show="{{visible}}" > Hello World </text>
5. </div>

6. /* xxx.css */
7. .container{
8.   flex-direction: column;
9.   align-items: center;
10. }
11. .btn{
12.   width: 280px;
13.   font-size: 26px;
14.   margin: 10px 0;
15. }

16. // xxx.js
17. export default {
18.   data: {
19.     visible: false,
20.   },
21.   toggle: function() {
22.     this.visible = !this.visible;
23.   },
24. }

说明

禁止在同一个元素上同时设置for和if属性。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216164015.69430340644158278009386947091106:50001231000000:2800:46170C1E967E3C7CB47B932127FBEDE266D8E40E215F6697DAE5DCAFDF9170FC.gif)

## 逻辑控制块

<block>控制块使得循环渲染和条件渲染变得更加灵活；block在构建时不会被当作真实的节点编译。注意block标签只支持for和if属性。

1. <!-- xxx.hml -->
2. <list>
3.   <block for="glasses">
4.     <list-item type="glasses">
5.       <text>{{$item.name}}</text>
6.     </list-item>
7.     <block for="$item.kinds">
8.       <list-item type="kind">
9.         <text>{{$item.color}}</text>
10.       </list-item>
11.     </block>
12.   </block>
13. </list>

14. // xxx.js
15. export default {
16.   data: {
17.     glasses: [
18.       {name:'sunglasses', kinds:[{name:'XXX',color:'XXX'},{name:'XXX',color:'XXX'}]},
19.       {name:'nearsightedness mirror', kinds:[{name:'XXX',color:'XXX'}]},
20.     ],
21.   },
22. }

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216164015.55201516495337621607607972613738:50001231000000:2800:6A2C3A4A7E4EC9A1931D0C7A27E939A8DDE4F8FF626740A799CAD1F3D8BC92FD.png)

## 模板引用

HML可以通过element引用模板文件，详细介绍可参考[自定义组件的基本用法](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-components-custom-basic-usage)章节。

1. <!-- template.hml -->
2. <div class="item"> 
3.   <text>Name: {{name}}</text>
4.   <text>Age: {{age}}</text>
5. </div>

6. <!-- index.hml -->
7. <element name='comp' src='../../common/template.hml'></element>
8. <div>
9.   <comp name="Tony" age="18"></comp>
10. </div>

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/js-framework-syntax "语法")
# CSS语法参考

更新时间: 2025-12-16 16:40

CSS是描述[HML](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/js-framework-syntax-hml)页面结构的样式语言。所有组件均存在系统默认样式，也可在页面CSS样式文件中对组件、页面自定义不同的样式。请参考[通用样式](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-components-common-styles)了解兼容JS的类Web开发范式支持的组件样式。

## 尺寸单位

- 逻辑像素px（文档中以<length>表示）：
    
    - 默认屏幕具有的逻辑宽度为720px（配置见[配置文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/js-framework-js-tag)中的window小节），实际显示时会将页面布局缩放至屏幕实际宽度，如100px在实际宽度为1440物理像素的屏幕上，实际渲染为200物理像素（从720px向1440物理像素，所有尺寸放大2倍）。
    - 额外配置autoDesignWidth为true时（配置见[配置文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/js-framework-js-tag)中的window小节），逻辑像素px将按照屏幕密度进行缩放，如100px在屏幕密度为3的设备上，实际渲染为300物理像素。应用需要适配多种设备时，建议采用此方法。
- 百分比（文档中以<percentage>表示）：表示该组件占父组件尺寸的百分比，如组件的width设置为50%，代表其宽度为父组件的50%。
    

## 样式导入

为了模块化管理和代码复用，CSS样式文件支持 @import 语句，导入css文件。

## 声明样式

每个页面目录下存在一个与布局hml文件同名的css文件，用来描述该hml页面中组件的样式，决定组件应该如何显示。

1. 内部样式，支持使用style、class属性来控制组件的样式。例如：
    
    1. <!-- index.hml -->
    2. <div class="container">
    3.   <text style="color: red">Hello World</text>
    4. </div>
    
    5. /* index.css */
    6. .container {
    7.   justify-content: center;
    8. }
    
2. 文件导入，合并外部样式文件。例如，在common目录中定义样式文件style.css，并在index.css文件首行中进行导入：
    
    1. /* style.css */
    2. .title {
    3.   font-size: 50px;
    4. }
    
    5. /* index.css */
    6. @import '../../common/style.css';
    7. .container {
    8.   justify-content: center;
    9. }
    

## 选择器

css选择器用于选择需要添加样式的元素，支持的选择器如下表所示：

|选择器|样例|样例描述|
|:--|:--|:--|
|.class|.container|用于选择class="container"的组件。|
|#id|#titleId|用于选择id="titleId"的组件。|
|tag|text|用于选择text组件。|
|,|.title, .content|用于选择class="title"和class="content"的组件。|
|#id .class tag|#containerId .content text|非严格父子关系的后代选择器，选择具有id="containerId"作为祖先元素，class="content"作为次级祖先元素的所有text组件。如需使用严格的父子关系，可以使用“>”代替空格，如：#containerId>.content。|

示例：

1. <!-- 页面布局xxx.hml -->
2. <div id="containerId" class="container">
3.   <text id="titleId" class="title">标题</text>
4.   <div class="content">
5.     <text id="contentId">内容</text>
6.   </div>
7. </div>

8. /* 页面样式xxx.css */
9. .container {
10.   width: 100%;
11.   height: 100%;
12.   justify-content: center;
13.   align-items: center;
14. }
15. /* 对所有div组件设置样式 */
16. div {
17.   flex-direction: column;
18. }
19. /* 对class="title"的组件设置样式 */
20. .title {
21.   font-size: 30px;
22. }
23. /* 对id="contentId"的组件设置样式 */
24. #contentId {
25.   font-size: 20px;
26. }
27. /* 对所有class="title"以及class="content"的组件都设置padding为5px */
28. .title, .content {
29.   padding: 5px;
30. }
31. /* 对class="container"的组件下的所有text设置样式 */
32. .container text {
33.   color: #007dff;
34. }
35. /* 对class="container"的组件下的直接后代text设置样式 */
36. .container > text {
37.   color: #fa2a2d;
38. }

以上样式运行效果如下：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216164028.29701661398704310378554283359212:50001231000000:2800:27B473F3BE800DAD6C0BE431EB04757EE66A5601F26C3B94175B24B56F826FB6.png)

其中“.container text”将“标题”和“内容”设置为蓝色，而“.container > text”直接后代选择器将“标题”设置为红色。2者优先级相同，但直接后代选择器声明顺序靠后，将前者样式覆盖（优先级计算见[选择器优先级](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/js-framework-syntax-css#%E9%80%89%E6%8B%A9%E5%99%A8%E4%BC%98%E5%85%88%E7%BA%A7)）。

## 选择器优先级

选择器的优先级计算规则与w3c规则保持一致（只支持：内联样式，id，class，tag，后代和直接后代），其中内联样式为在元素style属性中声明的样式。

当多条选择器声明匹配到同一元素时，各类选择器优先级由高到低顺序为：内联样式 > id > class > tag。

## 伪类

css伪类是选择器中的关键字，用于指定要选择元素的特殊状态。例如，:disabled状态可以用来设置元素的disabled属性变为true时的样式。

除了单个伪类之外，还支持伪类的组合，例如，:focus:checked状态可以用来设置元素的focus属性和checked属性同时为true时的样式。支持的单个伪类如下表所示，按照优先级降序排列：

|名称|支持组件|描述|
|:--|:--|:--|
|:disabled|支持disabled属性的组件|表示disabled属性变为true时的元素（不支持动画样式的设置）。|
|:active|支持click事件的组件|表示被用户激活的元素，如：被用户按下的按钮、被激活的tab-bar页签（不支持动画样式的设置）。|
|:waiting|button|表示waiting属性为true的元素（不支持动画样式的设置）。|
|:checked|input[type="checkbox"、type="radio"]、 switch|表示checked属性为true的元素（不支持动画样式的设置）。|

伪类示例如下，设置按钮的:active伪类可以控制被用户按下时的样式：

1. <!-- index.hml -->
2. <div class="container">
3.   <input type="button" class="button" value="Button"></input>
4. </div>

5. /* index.css */
6. .container {
7.   width: 100%;
8.   height: 100%;
9.   justify-content: center;
10.   align-items: center;
11. }

12. .button:active {
13.   background-color: #888888;/*按钮被激活时，背景颜色变为#888888 */
14. }

说明

针对弹窗类组件及其子元素不支持伪类效果，包括popup、dialog、menu、option、picker。

## 样式预编译

预编译提供了利用特有语法生成css的程序，可以提供变量、运算等功能，令开发者更便捷地定义组件样式，目前支持less、sass和scss的预编译。使用样式预编译时，需要将原css文件后缀改为less、sass或scss，如index.css改为index.less、index.sass或index.scss。

- 当前文件使用样式预编译，例如将原index.css改为index.less：
    
    1. /* index.less */
    2. /* 定义变量 */
    3. @colorBackground: #000000;
    4. .container {
    5.   background-color: @colorBackground; /* 使用当前less文件中定义的变量 */
    6. }
    
- 引用预编译文件，例如common中存在style.scss文件，将原index.css改为index.scss，并引入style.scss：
    
    1. /* style.scss */
    2. /* 定义变量 */
    3. $colorBackground: #000000;
    
    在index.scss中引用：
    
    4. /* index.scss */
    5. /* 引入外部scss文件 */
    6. @import '../../common/style.scss';
    7. .container {
    8.   background-color: $colorBackground; /* 使用style.scss中定义的变量 */
    9. }
    
    说明
    
    引用的预编译文件建议放在common目录进行管理。
    

## CSS样式继承6+

css样式继承提供了子节点继承父节点样式的能力，继承下来的样式在多选择器样式匹配的场景下，优先级排最低，当前支持以下样式的继承：

- font-family
    
- font-weight
    
- font-size
    
- font-style
    
- text-align
    
- line-height
    
- letter-spacing
    
- color
    
- visibility
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/js-framework-syntax-hml "HML语法参考")
# JS语法参考

更新时间: 2025-12-16 16:40

JS文件用来定义HML页面的业务逻辑，支持ECMA规范的JavaScript语言。基于JavaScript语言的动态化能力，可以使应用更加富有表现力，具备更加灵活的设计能力。下面讲述JS文件的编译和运行的支持情况。

## 语法

支持ES6语法。

- 模块声明
    
    使用import方法引入功能模块：
    
    1. import router from '@ohos.router';
    
- 代码引用
    
    使用import方法导入js代码：
    
    1. import utils from '../../common/utils.js';
    

## 对象

- 应用对象
    
    |属性|类型|描述|
    |:--|:--|:--|
    |$def|Object|使用this.$app.$def获取在app.js中暴露的对象。<br><br>**说明：**<br><br>应用对象不支持数据绑定，需主动触发UI更新。|
    
    示例代码
    
    1. // app.js
    2. export default {
    3.   onCreate() {
    4.     console.info('Application onCreate');
    5.   },
    6.   onDestroy() {
    7.     console.info('Application onDestroy');
    8.   },
    9.   globalData: {
    10.     appData: 'appData',
    11.     appVersion: '2.0',
    12.   },
    13.   globalMethod() {
    14.     console.info('This is a global method!');
    15.     this.globalData.appVersion = '3.0';
    16.   }
    17. };
    
    18. // index.js页面逻辑代码
    19. export default {
    20.   data: {
    21.     appData: 'localData',
    22.     appVersion:'1.0',
    23.   },
    24.   onInit() {
    25.     this.appData = this.$app.$def.globalData.appData;
    26.     this.appVersion = this.$app.$def.globalData.appVersion;
    27.   },
    28.   invokeGlobalMethod() {
    29.     this.$app.$def.globalMethod();
    30.   },
    31.   getAppVersion() {
    32.     this.appVersion = this.$app.$def.globalData.appVersion;
    33.   }
    34. }
    
- 页面对象
    
    |属性|类型|描述|
    |:--|:--|:--|
    |data|Object/Function|页面的数据模型，类型是对象或者函数，如果类型是函数，返回值必须是对象。属性名不能以$或_开头，不要使用保留字for, if, show, tid。<br><br>data字段不可与private/public字段同时使用。|
    |$refs|Object|持有注册过ref 属性的DOM元素或子组件实例的对象。示例见[获取DOM元素](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/js-framework-syntax-js#%E8%8E%B7%E5%8F%96dom%E5%85%83%E7%B4%A0)。|
    |private|Object|页面的数据模型，private下的数据属性只能由当前页面修改。|
    |public|Object|页面的数据模型，public下的数据属性的行为与data保持一致。|
    |props|Array/Object|props用于组件之间的通信，可以通过<tag xxxx='value'>方式传递给组件；props名称必须用小写，不能以$或_开头，不要使用保留字for, if, show, tid。目前props的数据类型不支持Function。示例见[Props](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-components-custom-props#props)。|
    |computed|Object|用于在读取或设置进行预先处理，计算属性的结果会被缓存。计算属性名不能以$或_开头，不要使用保留字。示例见[computed](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-components-custom-props#computed)。|
    

## 方法

- 数据方法
    
    |方法|参数|描述|
    |:--|:--|:--|
    |$set|key: string, value: any|添加新的数据属性或者修改已有数据属性。<br><br>用法：<br><br>this.$set('key',value)：添加数据属性。|
    |$delete|key: string|删除数据属性。<br><br>用法：<br><br>this.$delete('key')：删除数据属性。|
    
    示例代码
    
    1. // index.js
    2. export default {
    3.   data: {
    4.     keyMap: {
    5.       OS: 'OS',
    6.       Version: '2.0',
    7.     },
    8.   },
    9.   getAppVersion() {
    10.     this.$set('keyMap.Version', '3.0');
    11.     console.info("keyMap.Version = " + this.keyMap.Version); // keyMap.Version = 3.0
    
    12.     this.$delete('keyMap');
    13.     console.info("keyMap.Version = " + this.keyMap); // log print: keyMap.Version = undefined
    14.   }
    15. }
    
- 公共方法
    
    |方法|参数|描述|
    |:--|:--|:--|
    |$element|id: string|获得指定id的组件对象，如果无指定id，则返回根组件对象。示例见[获取DOM元素](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/js-framework-syntax-js#%E8%8E%B7%E5%8F%96dom%E5%85%83%E7%B4%A0)。<br><br>用法：<br><br><div id='xxx'></div><br><br>- this.$element('xxx')：获得id为xxx的组件对象。<br><br>- this.$element()：获得根组件对象。|
    |$rootElement|无|获取根组件对象。<br><br>用法：<br><br>this.$rootElement().scrollTo({ duration: 500, position: 300 }), 页面在500ms内滚动300px。|
    |$root|无|获得顶级ViewModel实例。[获取ViewModel](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/js-framework-syntax-js#%E8%8E%B7%E5%8F%96viewmodel)示例。|
    |$parent|无|获得父级ViewModel实例。[获取ViewModel](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/js-framework-syntax-js#%E8%8E%B7%E5%8F%96viewmodel)示例。|
    |$child|id: string|获得指定id的子级自定义组件的ViewModel实例。[获取ViewModel](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/js-framework-syntax-js#%E8%8E%B7%E5%8F%96viewmodel)示例。<br><br>用法：<br><br>this.$child('xxx') ：获取id为xxx的子级自定义组件的ViewModel实例。|
    
- 事件方法
    
    |方法|参数|描述|
    |:--|:--|:--|
    |$watch|data: string, callback: string \| Function|观察data中的属性变化，如果属性值改变，触发绑定的事件。示例见[$watch感知数据改变](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-components-custom-props#watch%E6%84%9F%E7%9F%A5%E6%95%B0%E6%8D%AE%E6%94%B9%E5%8F%98)。<br><br>用法：<br><br>this.$watch('key', callback)：通过监听key属性值的变化，触发callback事件。|
    
- 页面方法
    
    |方法|参数|描述|
    |:--|:--|:--|
    |scrollTo6+|scrollPageParam: ScrollPageParam|将页面滚动到目标位置，可以通过ID选择器指定或者滚动距离指定。|
    
    **表1** ScrollPageParam6+
    
    |名称|类型|默认值|描述|
    |:--|:--|:--|:--|
    |position|number|-|指定滚动位置。|
    |id|string|-|指定需要滚动到的元素id。|
    |duration|number|300|指定滚动时长，单位为毫秒。|
    |timingFunction|string|ease|指定滚动动画曲线，可选值参考<br><br>[动画样式animation-timing-function](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-components-common-animation)。|
    |complete|() => void|-|指定滚动完成后需要执行的回调函数。|
    
    示例：
    
    1. this.$rootElement().scrollTo({ position: 0 });
    2. this.$rootElement().scrollTo({ id: 'id', duration: 200, timingFunction: 'ease-in', complete: () => {
    3.     console.info('滚动已完成');
    4. } });
    

## 获取DOM元素

1. 通过$refs获取DOM元素
    
    1. <!-- index.hml -->
    2. <div class="container">
    3.   <image-animator class="image-player" ref="animator" images="{{images}}" duration="1s" onclick="handleClick"></image-animator>
    4. </div>
    
    5. // index.js
    6. export default {
    7.   data: {
    8.     images: [
    9.       { src: '/common/frame1.png' },
    10.       { src: '/common/frame2.png' },
    11.       { src: '/common/frame3.png' }
    12.     ]
    13.   },
    14.   handleClick() {
    15.     const animator = this.$refs.animator; // 获取ref属性为animator的DOM元素
    16.     const state = animator.getState();
    17.     if (state === 'Paused') {
    18.       animator.resume();
    19.     } else if (state === 'Stopped') {
    20.       animator.start();
    21.     } else {
    22.       animator.pause();
    23.     }
    24.   },
    25. };
    
2. 通过$element获取DOM元素
    
    1. <!-- index.hml -->
    2. <div class="container" style="width:500px;height: 700px; margin: 100px;">
    3.   <image-animator class="image-player" id="animator" images="{{images}}" duration="1s" onclick="handleClick"></image-animator>
    4. </div>
    
    5. // index.js
    6. export default {
    7.   data: {
    8.     images: [
    9.       { src: '/common/frame1.png' },
    10.       { src: '/common/frame2.png' },
    11.       { src: '/common/frame3.png' }
    12.     ]
    13.   },
    14.   handleClick() {
    15.     const animator = this.$element('animator'); // 获取id属性为animator的DOM元素
    16.     const state = animator.getState();
    17.     if (state === 'Paused') {
    18.       animator.resume();
    19.     } else if (state === 'Stopped') {
    20.       animator.start();
    21.     } else {
    22.       animator.pause();
    23.     }
    24.   },
    25. };
    

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216164041.94384284987403150792806572525872:50001231000000:2800:9F750D2654DE4F204105CF3E97F0B228F19E200329974B65406800FFD526AB72.gif)

## 获取ViewModel

根节点所在页面：

1. <!-- root.hml -->
2. <element name='parentComp' src='../../common/component/parent/parent.hml'></element>
3. <div class="container">
4.   <div class="container">
5.     <text>{{text}}</text>
6.     <parentComp></parentComp>
7.   </div>
8. </div>

9. // root.js
10. export default {
11.   data: {
12.     text: 'I am root!',
13.   },
14. }

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216164041.58064708634310118930401911506687:50001231000000:2800:C60B21C4D654B67DC33502C06CABBF7842AF2E4DE744DDFAEDEC12C42769E2A6.png)

自定义parent组件：

1. <!-- parent.hml -->
2. <element name='childComp' src='../child/child.hml'></element>
3. <div class="item" onclick="textClicked">
4.   <text class="text-style" onclick="parentClicked">parent component click</text>
5.   <text class="text-style" if="{{showValue}}">hello parent component!</text>
6.   <childComp id = "selfDefineChild"></childComp>
7. </div>

8. // parent.js
9. export default {
10.   data: {
11.     showValue: false,
12.     text: 'I am parent component!',
13.   },
14.   parentClicked () {
15.     this.showValue = !this.showValue;
16.     console.info('parent component get parent text');
17.     console.info(`${this.$parent().text}`);
18.     console.info("parent component get child function");
19.     console.info(`${this.$child('selfDefineChild').childClicked()}`);
20.   },
21. }

自定义child组件：

1. <!-- child.hml -->
2. <div class="item" onclick="textClicked">
3.   <text class="text-style" onclick="childClicked">child component clicked</text>
4.   <text class="text-style" if="{{isShow}}">hello child component</text>
5. </div>

6. // child.js
7. export default {
8.   data: {
9.     isShow: false,
10.     text: 'I am child component!',
11.   },
12.   childClicked () {
13.     this.isShow = !this.isShow;
14.     console.info('child component get parent text');
15.     console.info('${this.$parent().text}');
16.     console.info('child component get root text');
17.     console.info('${this.$root().text}');
18.   },
19. }

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216164041.48677453986601107654543493713144:50001231000000:2800:FA01367305ADAA6EC2425438C75EBAC81A47AF691CAAF643F056CE7F257794CF.gif)

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/js-framework-syntax-css "CSS语法参考")
# 生命周期

更新时间: 2025-12-16 16:39

## 应用生命周期

在app.js中可以定义如下应用生命周期函数：

|属性|类型|描述|触发时机|
|:--|:--|:--|:--|
|onCreate|() => void|应用创建|当应用创建时调用。|
|onShow6+|() => void|应用处于前台|当应用处于前台时触发。|
|onHide6+|() => void|应用处于后台|当应用处于后台时触发。|
|onDestroy|() => void|应用销毁|当应用退出时触发。|

## 页面生命周期

在页面JS文件中可以定义如下页面生命周期函数：

|属性|类型|描述|触发时机|
|:--|:--|:--|:--|
|onInit|() => void|页面初始化|页面数据初始化完成时触发，只触发一次。|
|onReady|() => void|页面创建完成|页面创建完成时触发，只触发一次。|
|onShow|() => void|页面显示|页面显示时触发。|
|onHide|() => void|页面消失|页面消失时触发。|
|onDestroy|() => void|页面销毁|页面销毁时触发。|
|onBackPress|() => boolean|返回按钮动作|当用户点击返回按钮时触发。<br><br>- 返回true表示页面自己处理返回逻辑。<br><br>- 返回false表示使用默认的返回逻辑。<br><br>- 不返回值会作为false处理。|
|onActive()5+|() => void|页面激活|页面激活时触发。|
|onInactive()5+|() => void|页面暂停|页面暂停时触发。|
|onNewRequest()5+|() => void|FA重新请求|FA已经启动时收到新的请求后触发。|

生命周期函数的一般调用顺序如下所示：

**图1** 生命周期函数调用顺序图示

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163958.45621901913269087258006232098146:50001231000000:2800:00B6DA49642DDFFA90EE5E23854EBE4BFB5224403617C57491D325A49846552D.png)

## 示例代码

通过以下示例，详细说明生命周期函数的调用顺序。首先创建两个页面，分别为pageA和pageB，并在config.json中配置页面路由信息：

1. {
2.     // ...
3.     "pages": [
4.         "pages/pageA/pageA",
5.         "pages/pageB/pageB"
6.     ],
7.     // ...
8. }

pageA实现代码如下：

1. <!-- pageA.hml -->
2. <div class="container">
3.   <text class="title">This is PageA</text>
4.   <input type="button" value="Go to the PageB" onclick="launch"></input>
5. </div>

6. /* pageA.css */
7. .container {
8.   flex-direction: column;
9.   align-items: center;
10.   width: 100%;
11.   height: 100%;
12. }
13. .title {
14.   font-size: 38px;
15.   text-align: center;
16.   width: 100%;
17.   height: 40%;
18. }

19. // pageA.js
20. import router from '@ohos.router';
21. export default {
22.   launch() {
23.     router.push ({
24.       url: 'pages/pageB/pageB'
25.     });
26.   },
27.   onInit() {
28.     console.info('PageA onInit');
29.   },
30.   onReady() {
31.     console.info('PageA onReady');
32.   },
33.   onShow() {
34.     console.info('PageA onShow');
35.   },
36.   onHide() {
37.     console.info('PageA onHide');
38.   },
39.   onDestroy() {
40.     console.info('PageA onDestroy');
41.   },
42.   onBackPress() {
43.     console.info('PageA onBackPress');
44.   },
45.   onActive() {
46.     console.info('PageA onActive');
47.   },
48.   onInactive() {
49.     console.info('PageA onInactive');
50.   },
51.   onNewRequest() {
52.     console.info('PageA onNewRequest');
53.   }
54. }

pageB实现代码如下：

1. <!-- pageB.hml -->
2. <div class="container">
3.   <text class="title">This is PageB</text>
4. </div>

5. /* pageB.css */
6. .container {
7.   flex-direction: column;
8.   align-items: center;
9.   width: 100%;
10.   height: 100%;
11. }
12. .title {
13.   font-size: 38px;
14.   text-align: center;
15.   width: 100%;
16.   height: 40%;
17. }

18. // pageB.js
19. export default {
20.   onInit() {
21.     console.info('PageB onInit');
22.   },
23.   onReady() {
24.     console.info('PageB onReady');
25.   },
26.   onShow() {
27.     console.info('PageB onShow');
28.   },
29.   onHide() {
30.     console.info('PageB onHide');
31.   },
32.   onDestroy() {
33.     console.info('PageB onDestroy');
34.   },
35.   onBackPress() {
36.     console.info('PageB onBackPress');
37.   },
38.   onActive() {
39.     console.info('PageB onActive');
40.   },
41.   onInactive() {
42.     console.info('PageB onInactive');
43.   },
44.   onNewRequest() {
45.     console.info('PageB onNewRequest');
46.   }
47. }

运行程序，通过日志观察生命周期函数的调用顺序。其中pageA的生命周期函数的调用顺序为：

- 打开应用进入页面A：onInit() -> onReady() -> onActive() -> onShow()
    
- 在页面A打开页面B：onHide()
    
- 从页面B返回页面A：onShow()
    
- 退出页面A：onBackPress() -> onInactive() -> onHide()
    
- 页面A隐藏到后台运行：onInactive() -> onHide()
    
- 页面A从后台运行恢复到前台：onNewRequest() -> onShow() -> onActive()
    

pageB的生命周期函数的调用顺序为：

- 在页面A打开页面B：onInit() -> onReady() -> onShow()
    
- 从页面B返回页面A：onBackPress() -> onHide() -> onDestroy()
    
- 页面B隐藏到后台运行：onInactive() -> onHide()
    
- 页面B从后台运行恢复到前台：onNewRequest() -> onShow() -> onActive()
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/js-framework-syntax-js "JS语法参考")
