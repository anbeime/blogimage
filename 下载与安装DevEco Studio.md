# 下载与安装DevEco Studio

更新时间: 2025-12-16 15:57

## 下载软件

请前往[下载中心](https://developer.huawei.com/consumer/cn/download/deveco-studio)，登录华为账号后下载DevEco Studio，并根据下载中心页面**工具完整性**指导进行完整性校验。

DevEco Studio支持Windows和macOS系统，下面将针对两种操作系统的软件安装方式分别进行介绍。

## Windows环境

### 运行环境要求

为保证DevEco Studio正常运行，建议电脑配置满足如下要求：

- 操作系统：Windows10 64位、Windows11 64位
- 内存：16GB及以上
- 硬盘：100GB及以上
- 分辨率：1280*800像素及以上

### 安装DevEco Studio

1. 下载完成后，双击下载的“deveco-studio-xxxx.exe”，进入DevEco Studio安装向导。在如下界面选择安装路径，默认安装于C:\Program Files路径下，也可以单击**浏览（B）...**指定其他安装路径，然后单击**下一步**。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155720.08899713960309919511675964000288:50001231000000:2800:F464ED060738E4B1EDC2F3CFFF7266D22E1E08822B69327B1489656C35F9032C.png)
    
2. 在如下安装选项界面勾选**DevEco Studio**后，单击**下一步**，直至安装完成。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155720.59137857013160308565079889668641:50001231000000:2800:3E9BD4EC260711BA5CE7DEAD7E98526F20307A51066C99B74439BC0D1B9D6A5F.png)
    
3. 安装完成后，单击**Finish**完成安装。安装完成后，如有需要请根据[配置代理](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-environment-config)，检查和配置开发环境。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155720.47266238744069313733381321750409:50001231000000:2800:B530A8E0F00CC03BBEAD3E420DCEAC3B2ECC84E0E7C5E30D5F00873E2F323F69.png)
    
    说明
    
    - DevEco Studio提供开箱即用的开发体验，将HarmonyOS SDK、Node.js、Hvigor、OHPM、模拟器平台等进行合一打包，简化DevEco Studio安装配置流程。
    - HarmonyOS SDK已嵌入DevEco Studio中，无需额外下载配置。HarmonyOS SDK可以在DevEco Studio安装位置下DevEco Studio\sdk目录中查看。如需进行OpenHarmony应用开发，可通过File > Settings > OpenHarmony SDK页签下载OpenHarmony SDK。
    

## macOS环境

### 运行环境要求

为保证DevEco Studio正常运行，建议电脑配置满足如下要求：

- 操作系统：macOS(X86) 11/12/13/14/15、 macOS(ARM) 12/13/14/15
- 内存：8GB及以上
- 硬盘：100GB及以上
- 分辨率：1280*800像素及以上

### 安装DevEco Studio

1. 在安装界面中，将“**DevEco-Studio.app**”拖拽到“**Applications**”中，等待安装完成。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155720.37926227343571168699467859990323:50001231000000:2800:8E0739B3DF0C130CB36AE7024B388053924019D3DAE35EA9EA83B8F2D8E68782.png "点击放大")
    
2. 安装完成后，如有需要请根据[配置代理](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-environment-config)，检查和配置开发环境。
    
    说明
    
    - DevEco Studio提供开箱即用的开发体验，将HarmonyOS SDK、Node.js、Hvigor、OHPM、模拟器平台等进行合一打包，简化DevEco Studio安装配置流程。
    - HarmonyOS SDK已嵌入DevEco Studio中，无需额外下载配置。HarmonyOS SDK可以在DevEco Studio安装位置下DevEco Studio\sdk目录中查看。如需进行OpenHarmony应用开发，可通过DevEco Studio > Preferences/Settings **>** OpenHarmony SDK页签下载OpenHarmony SDK。
    

## 诊断开发环境

为了您开发应用/元服务的良好体验，DevEco Studio提供了开发环境诊断的功能，帮助您识别开发环境是否完备。您可以在欢迎页面单击**Diagnose**进行诊断。如果您已经打开了工程开发界面，也可以在菜单栏单击**Help > Diagnostic Tools > Diagnose Development Environment**进行诊断。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155720.12762000587267149309845943336316:50001231000000:2800:53F7BE8CEDAD08635BADA11B109109F89F26CE54746E827416C752997F752249.png)

DevEco Studio开发环境诊断项包括电脑的配置、网络的连通情况、依赖的工具是否安装等。如果检测结果为未通过，请根据检查项的描述和修复建议进行处理。

## 启用中文化插件

说明

该功能仅支持中国境内（香港特别行政区、澳门特别行政区、中国台湾除外）。

- 从DevEco Studio 6.0.0 Beta1版本开始，中文化插件默认启用。如需切换为中文显示效果，在菜单栏进入**File > Settings...**（macOS为**DevEco Studio > Preferences/Settings** ） **> Appearance & Behavior > System Settings** > **Language**，语言选择**Chinese**并点击**Apply**，在弹窗中点击**Restart**重启即可完成语言切换。若语言选择时未找到Chinese，请按照[之前版本操作](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-software-install#li1956431816322)启用插件后，再选择。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155720.82344715650021387926980137618851:50001231000000:2800:701FB938A3752198420D403E89E78CE6A4933567BA1EC89985C971031BDE1863.png)
    

- 若使用DevEco Studio 6.0.0 Beta1之前版本，请在菜单栏进入**File > Settings** （macOS为**DevEco Studio > Preferences** ）**> Plugins**，选择**Installed**页签，在搜索框输入“Chinese”，搜索结果里将出现**Chinese(Simplified)**，在右侧单击**Enable**，点击**OK**，在弹窗中单击**Restart**，重启DevEco Studio后即可生效。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155721.67237622539504458868220309338273:50001231000000:2800:735D53C16912FEDB4727EC853F7CD0322128BCDCDD4220C5EE8F645A2F8E4582.png)
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-tools-overview "工具概述")
# 使用新UI

更新时间: 2025-12-16 15:57

DevEco Studio 6.0.0 Beta1版本适配IntelliJ 2024.3.3底座升级，同时提供全新的用户界面（User Interface，简称UI），简化工具布局，优化图标、窗口等显示效果，带来更简洁的外观及开发体验。

## 开启或关闭新UI

启动DevEco Studio 6.0.0 Beta1版本时，将有弹窗提示是否启用新用户界面。点击**Enable and Restart**，将重启DevEco Studio开始体验新UI。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155721.84544320888809327659322510011367:50001231000000:2800:C4D9FC7FC1B5DEA4F8F82A38078699AB5115166E1F72D4093A1B4CAE4C62CC6C.png)

此外，可以在菜单栏进入**File > Settings...**（macOS系统为**DevEco Studio > Preferences/Settings...**）**> Appearance & Behavior > New UI**，勾选**Enable new UI**，点击**Apply**，在弹窗中点击**Restart**重启完成后体验新UI。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155721.51449835235535993506766223136895:50001231000000:2800:D8AE8527BF47CFDD655A99A808D4D37D829E31DC52AB5B5B32B8E9419359D297.png)

如需切换回原有的经典UI，在界面左上角点击![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155721.36620405639346416944156411919907:50001231000000:2800:3D4CCB189EEB85DFE03A29A49563A0079D17EF0589B8535E6C25F68AF9F7FF03.png)图标，进入**File > Settings...** （macOS系统为**DevEco Studio > Preferences/Settings...**）**> Appearance & Behavior > New UI**，取消勾选**Enable new UI**，点击**Apply**，在弹窗中点击**Restart**重启即可完成切换。

## 菜单栏体验变化

原有固定于界面上方的菜单栏，在新UI中收起到页面左上角工具栏中Main Menu主菜单![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155721.99057764037581955084581451702765:50001231000000:2800:D192941B4D6DABC711CD8F3B940C4928D06CBF69EEEAFBCA6D965DA3E23104C0.png)图标内。点击图标即可展开菜单，继续选择需要执行的功能或操作。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155721.15654531270869400821486042132272:50001231000000:2800:2DBA2394451618A19A045A0B0933B81C22EAF30747C49796BFE633B0E9CE6E77.png)

如需将菜单栏展开并固定在主界面，可以在菜单栏进入**File > Settings... > Appearance & Behavior > Appearance** > **UI Options**中，勾选**Show main menu in a separate toolbar**，点击**Apply**在主界面固定显示菜单栏。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155721.71677989331504415737501864123111:50001231000000:2800:7AA8AFE47E22E7E8A29308724064EB98429051CA215CD294447B595C263A5486.png)

## 工具窗口优化

主窗口两侧的工具窗口提供更丰富的功能选择。与经典UI相比，ArkUI Inspector、Services、Terminal、Problems、Version Control等功能图标在左侧工具窗口中呈现。点击工具窗口中Project![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155721.01620344790495678380627665858104:50001231000000:2800:42B1F9E907E3B08CCD1686B236D6C57D14BF411110049AAF02561AAF316EE7D9.png)图标，显示当前工程目录。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155721.66458829920607467435855931144089:50001231000000:2800:2C4C79731733614878BB3DBF73DFFA5FDEC22459F14DE9C698BF6B37B2360B25.png)

在菜单栏进入**File > Settings... > Appearance & Behavior > Appearance** > **Tool Windows，**勾选**Show tool window names**后点击**Apply**，或将鼠标放置于工具窗口区域右键选择**Show Tool Window Names**，选择在界面中展示各功能图标的名称。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155721.31838107708525274450741901133898:50001231000000:2800:738F426DB8AF028E99BBC33980A575055316FD7CF1AB6D15FDA81D4333498BDB.png)

## 文件路径展示位置变化

在新UI中，当前编辑的文件所在的工程路径将展示在页面左下方。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155721.50653844873823982112931154187140:50001231000000:2800:54971B55487D171E8566CE39CFA466B32239E70324F0551E21BC3A8F88AF7B4A.png "点击放大")

说明

更多新用户界面变化详情，请参见[new UI](https://www.jetbrains.com.cn/en-us/help/idea/2024.3/new-ui.html)。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-software-install "下载与安装DevEco Studio")
# 工程介绍

更新时间: 2025-12-16 15:57

## 应用程序包基础知识

开发应用前，请先了解应用程序包相关基础知识，具体请参考[应用程序包概述](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/application-package-overview)。

## 切换工程视图

DevEco Studio工程目录结构提供工程视图和Ohos视图。工程视图（Project）展示工程中实际的文件结构，Ohos视图会隐藏一些编码中不常用到的文件，并将常用到的文件进行重组展示，方便开发者查询或定位所需编辑的模块或文件。

工程创建或打开后，默认显示工程视图，如果要切换到Ohos视图，在左上角单击**Project** > **Ohos**进行切换**。**

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155722.80293489663028796317413532183697:50001231000000:2800:1AF6D9029A7A250017D35767680AD1C1D3C9FBBA16342630FE4FB9369E4219E1.png)

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-project "工程创建")
# 工程目录结构

更新时间: 2025-12-16 15:57

## ArkTS工程目录结构（Stage模型）

ArkTS Stage模型支持API Version 10及以上版本，其工程目录结构如下图所示：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155722.99592238482924915337565247591747:50001231000000:2800:FBC8D6D84F5779B09CBC24B4A93A34F71E7DC068F482C9A739C8A51A926E5726.png)

- **AppScope > app.json5**：应用的全局配置信息。
- **entry：**应用/元服务模块，编译构建生成一个HAP。
    - **src > main > ets**：用于存放ArkTS源码。
    - **src > main > ets > entryability**：应用/元服务的入口。
    - **src > main > ets > entrybackupability**：用于提供扩展备份恢复能力。
    - **src > main > ets > pages**：应用/元服务包含的页面。
    - **src > main > resources：**用于存放应用/元服务模块所用到的资源文件，如图形、多媒体、字符串、布局文件等。关于资源文件的详细说明请参考[资源分类与访问](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/resource-categories-and-access)。
        
        |资源目录|资源文件说明|
        |:--|:--|
        |base>element|包括字符串、整型数、颜色、样式等资源的json文件。每个资源均由json格式进行定义，例如：<br><br>- boolean.json：布尔型<br>- color.json：颜色<br>- float.json：浮点型<br>- intarray.json：整型数组<br>- integer.json：整型<br>- pattern.json：样式<br>- plural.json：复数形式<br>- strarray.json：字符串数组<br>- string.json：字符串值|
        |base>media|多媒体文件，如图形、视频、音频等文件，支持的文件格式包括：**.png**、**.gif**、**.mp3**、**.mp4**等。|
        |rawfile|用于存储任意格式的原始资源文件。rawfile不会根据设备的状态去匹配不同的资源，需要指定文件路径和文件名进行引用。|
        
    - **src > main > module.json5**：Stage模型模块配置文件，主要包含HAP的配置信息、应用在具体设备上的配置信息以及应用的全局配置信息。具体请参考[module.json5配置文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file)。
    - **src > main >** **mock****：**配置测试框架的Mock能力。具体请参考[Mock能力](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-test-mock)。
    - **src > main >** **ohosTest：**存放Instrument Test测试类。具体请参考[Instrument Test](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-instrument-test)。
    - **src > main >** **test：**存放Local Test创建测试类。具体请参考[Local Test](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-local-test)。
    - **build-profile.json5：**当前的模块信息、编译信息配置项，包括buildOption、targets配置等。
    - **hvigorfile.ts**：模块级编译构建任务脚本。
    - **obfuscation-rules.txt**：混淆规则文件。混淆开启后，在使用Release模式进行编译时，会对代码进行编译、混淆及压缩处理，保护代码资产。详见[混淆加固](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-build-obfuscation)。
    - **oh-package.json5**：描述三方包的包名、版本、入口文件（类型声明文件）和依赖项等信息。
- **oh_modules**：用于存放三方库依赖信息，包含应用/元服务所依赖的第三方库文件。
- **build-profile.json5：**应用级配置信息，包括签名、产品配置等。
- **code-linter.json5：**配置代码检查规则，包括代码检查范围、生效的规则等。
- **hvigorfile.ts：**应用级编译构建任务脚本。
- **oh-package.json5：**描述全局配置，如：依赖覆盖（overrides）、依赖关系重写（overrideDependencyMap）和参数化配置（parameterFile）等。
- **oh-package-lock.json5：**用于锁定应用级依赖的版本，以及缓存依赖的元数据信息。

## C++工程目录结构（Stage模型）

C++ Stage模型支持API Version 10以上版本，支持使用ArkTS和C++进行开发，其工程目录结构如下图所示。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155722.82712482445929085152979814786937:50001231000000:2800:013FDC1E7F42095C8DE64D2CC0C94F1EE1EC63722FFC11DD6A1FEC597E2FF84C.png)

- **entry**：应用模块，编译构建生成一个HAP。
    - **src > main > cpp > types**：用于存放C++的API接口描述文件
    - **src > main > cpp > types** **> libentry > index.d.ts**：描述C++ API接口行为，如接口名、入参、返回参数等。
    - **src > main > cpp > types** **> libentry> oh-package.json5**：配置.so三方包声明文件的入口及包名。
    - **src > main > cpp > CMakeLists.txt**：CMake配置文件，提供CMake构建脚本。
    - **src > main > cpp > napi_init.cpp：**定义C++ API接口的文件**。**
    - **src > main > ets：**用于存放ArkTS源码。
    - **src > main > resources：**用于存放应用所用到的资源文件，如图形、多媒体、字符串、布局文件等。关于资源文件的详细说明请参考[资源分类与访问](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/resource-categories-and-access)。
        
        |资源目录|资源文件说明|
        |:--|:--|
        |base>element|包括字符串、整型数、颜色、样式等资源的json文件。每个资源均由json格式进行定义，例如：<br><br>- boolean.json：布尔型<br>- color.json：颜色<br>- float.json：浮点型<br>- intarray.json：整型数组<br>- integer.json：整型<br>- pattern.json：样式<br>- plural.json：复数形式<br>- strarray.json：字符串数组<br>- string.json：字符串值。|
        |base>media|多媒体文件，如图形、视频、音频等文件，支持的文件格式包括：**.png**、**.gif**、**.mp3**、**.mp4**等。|
        |rawfile|用于存储任意格式的原始资源文件。rawfile不会根据设备的状态去匹配不同的资源，需要指定文件路径和文件名进行引用。|
        
    - **src > main > module.json5：**Stage模块配置文件，主要包含HAP的配置信息、应用在具体设备上的配置信息以及应用的全局配置信息。具体请参考[module.json5配置文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file)。
    - **build-profile.json5：**当前的模块信息、编译信息配置项，包括buildOption、targets配置等。
    - **hvigorfile.ts：**模块级编译构建任务脚本。
    - **obfuscation-rules.txt**：混淆规则文件。混淆开启后，在使用Release模式进行编译时，会对代码进行编译、混淆及压缩处理，保护代码资产。详见[混淆加固](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-build-obfuscation)。
    - **oh-package.json5**：描述三方包的包名、版本、入口文件（类型声明文件）和依赖项等信息。
    - **oh-package-lock.json5：**用于锁定当前模块依赖的版本，以及缓存依赖的元数据信息。
- **oh_modules**：用于存放三方库依赖信息，包含应用/元服务所依赖的第三方库文件。
- **hvigorfile.ts**：应用级编译构建任务脚本。
- **build-profile.json5：**应用级配置信息，包括签名、产品配置等。
- **code-linter.json5：**配置代码检查规则，包括代码检查范围、生效的规则等。
- **hvigorfile.ts：**应用级编译构建任务脚本。
- **oh-package.json5：**描述全局配置，如：依赖覆盖（overrides）、依赖关系重写（overrideDependencyMap）和参数化配置（parameterFile）等。
- **oh-package-lock.json5：**用于锁定应用级依赖的版本，以及缓存依赖的元数据信息。

## JS工程目录结构（FA模型）

JS工程只支持FA模型，其工程目录结构如下图所示：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155722.46590681877019045670641291632684:50001231000000:2800:C050584D57E60CEDD39A76B2F9F9F6390A0EE4AF1069AF73A83B5D30E23AB9F0.png)

- **entry：**应用/元服务模块，编译构建生成一个HAP。
    - **src > main > js**：用于存放js源码。
    - **src > main > js > MainAbility**：应用/元服务的入口。
    - **src > main > js > MainAbility > i18n**：用于配置不同语言场景资源内容，比如应用文本词条、图片路径等资源。
    - **src > main > js > MainAbility > pages**：MainAbility包含的页面。
    - **src > main > js > MainAbility > app.js**：承载Ability生命周期。
    - **src > main > resources：**用于存放应用/元服务所用到的资源文件，如图形、多媒体、字符串、布局文件等。关于资源文件的详细说明请参考[资源分类与访问](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/resource-categories-and-access)。
        
        |资源目录|资源文件说明|
        |:--|:--|
        |base>element|包括字符串、整型数、颜色、样式等资源的json文件。每个资源均由json格式进行定义，例如：<br><br>- boolean.json：布尔型<br>- color.json：颜色<br>- float.json：浮点型<br>- intarray.json：整型数组<br>- integer.json：整型<br>- pattern.json：样式<br>- plural.json：复数形式<br>- strarray.json：字符串数组<br>- string.json：字符串值|
        |base>media|多媒体文件，如图形、视频、音频等文件，支持的文件格式包括：**.png**、**.gif**、**.mp3**、**.mp4**等。|
        |rawfile|用于存储任意格式的原始资源文件。rawfile不会根据设备的状态去匹配不同的资源，需要指定文件路径和文件名进行引用。|
        
    - **src > main > config.json**：模块配置文件，主要包含HAP的配置信息、应用在具体设备上的配置信息以及应用的全局配置信息。
    - **build-profile.json5：**当前的模块信息、编译信息配置项，包括buildOption、targets配置等。
    - **hvigorfile.ts**：模块级编译构建任务脚本。
    - **oh-package.json5**：配置三方包声明文件的入口及包名。
- **build-profile.json5：**应用级配置信息，包括签名、产品配置等。
- **hvigorfile.ts：**应用级编译构建任务脚本。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-project-overview "工程介绍")
# 工程模板介绍

更新时间: 2025-12-16 15:57

DevEco Studio支持多种品类的应用/元服务开发，预置丰富的工程模板，可以根据工程向导轻松创建适应于各类设备的工程，并自动生成对应的代码和资源模板。同时，DevEco Studio还提供了多种编程语言供开发者进行应用/元服务开发，包括ArkTS、JS和C/C++。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155722.53633840390243232091130445478893:50001231000000:2800:39A2566EE3E628BBF2045367A2ED9D462AF8E959BB759E2FE4BE73BF24221594.png)

工程模板支持的开发语言及模板说明如下表所示：

|模板名称|说明|
|:--|:--|
|Empty Ability|用于Phone、Tablet、2in1、Car、Wearable、TV设备的模板，展示基础的Hello World功能。|
|Native C++|用于Phone、Tablet、2in1、Car、Wearable、TV设备的模板，作为应用调用C++代码的示例工程，界面显示“Hello World”。|
|[CloudDev]Empty Ability|端云一体化开发通用模板。更多信息请参见[端云一体化开发](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddevguide)。<br><br>**约束与限制**：该功能仅支持中国境内（香港特别行政区、澳门特别行政区、中国台湾除外）。|
|[Lite]Empty Ability|用于Lite Wearable设备的模板，展示了基础的Hello World功能。可基于此模板，修改设备类型及RuntimeOS，进行小型嵌入式设备开发。|
|Flexible Layout Ability|用于创建跨设备应用开发的三层工程结构模板。三层工程结构包含common（公共能力层）、features（基础特性层）、products（产品定制层）。|
|Embeddable Ability|用于开发支持被其他应用嵌入式运行的元服务的工程模板。|
|[ArkUI-X]Empty Ability|创建一个展示基础的Hello World功能的模板，构建基于HarmonyOS应用的跨平台应用包。更多信息请参见[ArkUI-X概览](https://gitcode.com/arkui-x/docs/blob/master/zh-cn/ArkUI-X-Overview-zh.md#arkui-x%E6%A6%82%E8%A7%88)。|
|[ArkUI-X]Library|用于基于HarmonyOS应用构建跨平台应用的依赖包。依赖包支持添加到已有的应用中。更多信息请参见[ArkUI-X概览](https://gitcode.com/arkui-x/docs/blob/master/zh-cn/ArkUI-X-Overview-zh.md#arkui-x%E6%A6%82%E8%A7%88)。|
|[ArkUI-X]Native C++|创建一个调用C++代码的示例工程，构建基于HarmonyOS应用的跨平台应用包。更多信息请参见[ArkUI-X概览](https://gitcode.com/arkui-x/docs/blob/master/zh-cn/ArkUI-X-Overview-zh.md#arkui-x%E6%A6%82%E8%A7%88)。|

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-project-structure "工程目录结构")
# 创建一个新的工程

更新时间: 2025-12-16 15:57

当您开始开发一个应用/元服务时，首先需要根据工程创建向导，创建一个新的工程，工具会自动生成对应的代码和资源模板。

说明

在运行DevEco Studio工程时，建议每一个运行窗口有2GB以上的可用内存空间。

## 创建和配置新工程

DevEco Studio提供了基础的工程模板资源，不同模板支持的设备类型、API Version可能不同，在创建新工程前，请提前了解各模板的相关信息，具体请参考[工程模板介绍](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-template)。

从DevEco Studio 6.0.1 Beta1开始，创建Native C++工程时支持选择C++版本。

### 创建HarmonyOS工程

1. 通过如下两种方式，打开工程创建向导界面。
    
    - 如果当前未打开任何工程，可以在DevEco Studio的欢迎页，选择**Create Project**开始创建一个新工程。
    - 如果已经打开了工程，可以在菜单栏选择**File > New > Create Project**来创建一个新工程。
    
2. 根据工程创建向导，选择创建Application或[Atomic Service](https://developer.huawei.com/consumer/cn/doc/atomic-guides/atomic-service-create-project)。再选择需要的Ability工程模板，然后单击**Next**。
    
    说明
    
    - 从API 11版本开始支持Atomic Service元服务工程开发。
    - Atomic Service元服务工程暂不支持Native开发。
    - [CloudDev]Empty Ability模板：该功能仅支持中国境内（香港特别行政区、澳门特别行政区、中国台湾除外）。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155722.23195093282326869386588000404613:50001231000000:2800:7281A522D0BB69243E7914B2D6C589164D609D3CB088B31B03F8A13D7CAAF53E.png)
    
3. 在工程配置页面，需要根据向导配置工程的基本信息。
    
    - **Project name**：工程的名称，可以自定义，由大小写字母、数字和下划线组成，必须由大小写字母开头，长度为1~200个字符。
    - **Bundle name**：标识应用的包名，用于标识应用的唯一性。
        
        说明
        
        应用包名要求：
        
        - 必须为以点号（.）分隔的字符串，且至少包含三段，每段中仅允许使用英文字母、数字、下划线（_），如“com.example.myapplication ”。
        - 首段以英文字母开头，非首段以数字或英文字母开头，每一段以数字或者英文字母结尾，如“com.01example.myapplication”。
        - 不允许多个点号（.）连续出现，如“com.example..myapplication ”。
        - 长度为7~128个字符。
        
    - **Save location**：工程文件本地存储路径，由大小写字母、数字和下划线等组成，不能包含中文字符。
    - **Compatible SDK**：兼容的最低API Version。
    - **Module name**： 模块的名称。
    - **Device type：**该工程模板支持的设备类型。设备类型说明请参考[deviceTypes标签](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#devicetypes%E6%A0%87%E7%AD%BE)。
    - **C++ Standard：**C++标准库，取值包括：Toolchain Default、C++11、C++14。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155722.42531458612307277013659704246221:50001231000000:2800:284E0F87FE7F52B64F2B62E4F941672FFAD3EE584908C20A8E32925120CE22DC.png)
    
4. 单击**Finish**，工具会自动生成示例代码和相关资源，等待工程创建完成。

### （可选）创建OpenHarmony工程

如需创建OpenHarmony工程进行应用开发，请按照以下步骤操作。

1. 在完成[创建HarmonyOS工程](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-create-new-project#section11644183711342)后，根据如下操作修改工程级build-profile.json5文件中相关字段：
    
    1. 在工程级build-profile.json5文件添加**compileSdkVersion**字段。
    2. 将**compatibleSdkVersion**、**compileSdkVersion**、**targetSdkVersion**（若有）字段赋值为数值类型。
    3. 将runtimeOS从"HarmonyOS"修改为**"OpenHarmony"**。
    
    4. "products": [
    5.   {
    6.     "name": "default",
    7.     "signingConfig": "default", 
    8.     "compileSdkVersion": 20,    //指定OpenHarmony应用编译时的版本，当前以API 20为例
    9.     "targetSdkVersion": 20,     //指定OpenHarmony应用运行所需的目标SDK版本，当前以API 20为例
    10.     "compatibleSdkVersion": 20, //指定OpenHarmony应用兼容的最低版本，当前以API 20为例
    11.     "runtimeOS": "OpenHarmony",
    12.   }
    13. ],
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155722.98614772796232544224335863209671:50001231000000:2800:BAA4D665489F09825EC8979D0013275DD9C329AEF3C85BECCF424D0F9667FC70.png)
    
2. 单击Sync Now进行同步。在Sync Check弹窗中点击**Yes**，同意将module.json5/config.json文件中的phone切换为OpenHarmony支持的default类型，并删除在OpenHarmony不适用的其他设备类型，同步成功无其他报错则工程创建完成。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155722.88995959674805879823068836774831:50001231000000:2800:20C6C809C880FEA490E97D43AE34363B22789074325569A968009C0EA3540207.png)
    

说明

若选择Native C++模板创建OpenHarmony应用，且应用需要在RK开发板上运行，则需在对应Native模块的build-profile.json5文件buildOption/externalNativeOptions字段下，新增abiFilters字段并赋值为"armeabi-v7a"。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-template "工程模板介绍")
# 生成单层图标

更新时间: 2025-12-16 15:57

DevEco Studio支持Image Asset功能，帮助开发者生成适应不同设备、不同屏幕密度的图标，并展示图标在目录中的具体位置。

说明

当前Image Asset功能支持为Phone、Tablet、2in1应用生成单层图标。

Image Asset支持生成以下两种类型图标：

- icon：应用图标（设备桌面及设置>应用中出现的应用图标）。
- start window icon：启动页图标。

1. 在工程中选中模块或文件，右键单击**New > Image Asset**，进入图标配置页面。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155723.43882226126480418311201579433825:50001231000000:2800:9389A3A420E565D715C5B0F1A8BF159577AFB82262F2084A87C9FB49C932A061.png "点击放大")
    
    说明
    
    若在模块级目录（Entry或其他模块）下新建Image Asset，将创建Icon and start window icon类型图标，用于在module.json5文件中配置icon及startWindowIcon字段；在工程级目录（AppScope或其他目录）下新建Image Asset，将创建Icon类型图标，用于在app.json5文件中配置icon字段。
    
2. 需要根据向导配置图标样式、大小等基本信息。
    
    - **Device**：选择当前配置的图标生效的设备类型。
    - **Icon Type**：展示当前图标的类型。
    - **Name**：配置图标名称。命名支持使用字母、数字、下划线，长度最多128个字符，不支持中文命名。
    - **Foreground Layer**：分层图标资源前景层。可配置下列字段信息：
        - **Path**：选择前景Image存放路径。推荐使用的图标尺寸为1024px*1024px，保证图标整体的清晰性。
        - **Trim**：选择Yes，将调整图标图形与边框之间的距离，同时会去除图片周围多余的透明空间。
        - **Resize**：拖动滑块，设置图形的缩放比例。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155723.32046031362665436336848369114478:50001231000000:2800:0FB97DF60C6C2D2C7CEF6B21CCDBF96EDA2F4323F6491657C99C419327ED5D83.png)
    
    - **Background Layer**：分层图标资源背景层。请配置下列字段信息：
        - **Asset Type**：设置图标背景类型。可以选择颜色（**Color**）或图像（**Image**）。
        - **Color**：点击色块区域，选择适当的背景色。
        - **Path**：选择背景Image路径。推荐使用的图标尺寸为1024px*1024px，保证图标整体的清晰性。
        - **Trim**：选择Yes，将调整图标图形与边框之间的距离，同时会去除图片周围多余的透明空间。
        - **Resize**：拖动滑块，设置图形的缩放比例。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155723.87182526803356028548042096833799:50001231000000:2800:456D4FAD89E511563F954C487BFADBEF5F28E1B7F090A17061727928787E44EE.png)
    
3. 点击**Next**，确认图标相应的尺寸信息，点击**Finish**完成图标生成，图标将默认存放在**resources** 目录下。
    
    icon.png为桌面图标，icon_start window.png为启动页图标，Size为图标的尺寸信息，不同尺寸对照关系如下：
    
    - sdpi：表示小规模的屏幕密度（Small-scale Dots Per Inch），适用于dpi取值为(0, 120]的设备。
    - mdpi：表示中规模的屏幕密度（Medium-scale Dots Per Inch），适用于dpi取值为(120, 160]的设备。
    - ldpi：表示大规模的屏幕密度（Large-scale Dots Per Inch），适用于dpi取值为(160, 240]的设备。
    - xldpi：表示特大规模的屏幕密度（Extra Large-scale Dots Per Inch），适用于dpi取值为(240, 320]的设备。
    - xxldpi：表示超大规模的屏幕密度（Extra Extra Large-scale Dots Per Inch），适用于dpi取值为(320, 480]的设备。
    - xxxldpi：表示超特大规模的屏幕密度（Extra Extra Extra Large-scale Dots Per Inch），适用于dpi取值为(480, 640]的设备。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155723.30533306650590655748533798046818:50001231000000:2800:ED76343DA2EA74C1842E6A41E52E1B9E9F828E0D4ADA29EE85912CA0B0257645.png)
    
4. 如需配置桌面或设置页面出现的应用图标，可将module.json5文件中icon字段修改为新生成的图标名称；如需修改启动页的icon图标，可将module.json5文件中startWindowIcon字段修改为新生成的图标名称。
    
    说明
    
    - 当上述字段配置了新生成的图标名称后，系统会根据当前设备状态优先从相匹配的限定词目录，即步骤[3](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-apply-generated-icon#zh-cn_topic_0000002166648820_li094548151616)生成的不同尺寸的图标文件中寻找资源。具体请参考[资源匹配](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/resource-categories-and-access)。
    - 若module.json5文件中未配置icon字段，系统将使用app.json5中icon字段配置的图标。
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-create-new-project "创建一个新的工程")
# 添加/删除模块

更新时间: 2025-12-16 15:57

模块（Module）是应用/元服务的基本功能单元，包含了源代码、资源文件、第三方库及应用/元服务配置文件。一个应用/元服务通常会包含一个或多个模块，因此，可以在工程中创建多个模块。模块支持entry、feature（仅应用工程支持创建）、har、shared四种类型，具体请参考[module.json5配置文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6%E6%A0%87%E7%AD%BE)。

从DevEco Studio 6.0.1 Beta1开始，创建Native C++模块或Library模板时支持选择C++版本。

## 创建新的模块

1. 通过如下三种方法，在工程中添加新的模块。
    
    - 方法1：鼠标移到工程目录顶部，单击鼠标右键，选择**New > Module**...，开始创建新的Module，此时该模块将创建在工程根目录下。
    - 方法2：选中工程目录中任意文件，然后在菜单栏选择**File > New > Module**...，开始创建新的Module，此时该模块将创建在工程根目录下。
    - 方法3：在工程根目录下创建一个新的Directory，可在该目录下单击鼠标右键，选择**New > Module**...，创建新的模块，此时模块将创建在该文件目录下，方便开发者对模块进行分类管理。
        
        说明
        
        当前暂不支持在AppScope、hvigor、oh_modules、build、以点开头的目录（如：.hvigor、.idea）下通过单击鼠标右键创建模块。
        
    
2. 在**New Project Module**界面中，选择需要创建的模板，单击**Next**。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155723.65766727333323316386109862372930:50001231000000:2800:47355C87D856BAF3F6222041647B896BF2F426AB245461113B55FF88D9DE05B5.png)
    
3. 在模块配置页面，设置新增模块的基本信息，然后单击**Next**。从DevEco Studio 6.0.1 Beta1开始，支持选择C++版本。
    
    - **Module name**：新增模块的名称，**Module name**不可与工程名称/工程中其他模块名称相同。
    - **Module type**：仅在Ability模板存在该字段，可以选择Feature和Entry类型。
        
        说明
        
        - 同一工程通过新增模块仅支持创建一个Entry模块。如需构建Entry类型模块，可在module.json5文件中修改相应module下的type字段。
        - 如果同一类型的设备已经存在Entry模块，出现新的Entry模块后，还需要[配置分发策略](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#distributionfilter%E6%A0%87%E7%AD%BE)。
        
    - **Device type**：选择模块的设备类型，如果新建模块的Module type为feature，则只能选择该工程原有的设备类型；如果Module type为entry，可以选择该模块支持的其他设备类型。
    - **Enable native**：仅Library模板存在，将创建一个可以调用C/C++的共享包。
    - **C++ Standard：**C++标准库，取值包括：Toolchain Default、C++11、C++14。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155723.36582182613463809921591451403535:50001231000000:2800:9ED0B6693E8605BFD2E33B21903CFF36775A9C6ECD3F17F878F7662F5050C99C.png)
    
4. 若该模块的模板类型为Ability，还需要设置新增Ability的**Ability name**和****E****xported****参数，**E****xported**参数表示该Ability是否可以被其它应用/元服务所调用（FA模型下为Visible参数)。
    
    - 勾选（true）：可以被其它应用/元服务调用。
    - 不勾选（false）：不能被其它应用/元服务调用。
    
5. 单击**Finish**，等待创建完成后，可以在工程目录中查看和编辑新增的模块。工程中所包含模块的信息可以在[build-profile.json5](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile-app)中modules字段进行配置。

## 导入/引用模块

DevEco Studio支持通过以下两种方式导入其他工程下的模块：

1. 通过[Import Module](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-add-new-module#section13771399184)功能，将其它HarmonyOS模块的功能代码复制到当前工程中；当前仅支持FA模型的模块导入到FA模型，Stage模型的模块导入到Stage模型。不支持FA模型的模块导入到Stage模型，或Stage模型的模块导入到FA模型。
2. 通过在[srcPath字段下配置相对路径](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-add-new-module#section12961144312265)的方式引用其他工程下的模块，该方式仅引用模块相关信息，不会将模块代码完全复制至本地。当前支持引用其他工程下的HAR和HSP模块。

### Import Module

1. 在菜单栏单击**File > New > Import... > Import Module。**
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155723.66260707689037492787774962457508:50001231000000:2800:AAF201C095334B219E32674F7712296BFC25A6EA91BCEFCCBF440651049B7CEC.png)
    
2. 选择导入的模块。
    
    在指定路径下，选择导入的模块，单击**OK**。导入的模块可以为文件夹，也可以为zip格式。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155723.95650501753510399377621798914722:50001231000000:2800:94569BA101E2C703655E62025CB11A96881E1FEC91F0DA88C7690708776D2C84.png)
    

### srcPath方式引用模块

在工程级build-profile.json5文件中，如下图所示在modules > srcPath字段下配置工程外模块的相对路径，即可引用模块相关信息，不会将模块代码完全复制至本工程中。当前支持引用其他工程下的HAR和HSP模块。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155723.21542642706618316402339547717156:50001231000000:2800:0ADF876F5B3DED0A03BBAB7EC68C52E24D4CC113A066481A36E3FD02FC19623B.png)

## 删除Module

在工程目录中选中要删除的模块，单击鼠标右键，选中**Delete**，并在弹出的对话框中单击**Delete**。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-module-management "模块管理")
# 开发静态共享包

更新时间: 2025-12-16 15:57

HAR（Harmony Archive）是静态共享包，可以包含代码、C++库、资源和配置文件。通过HAR可以实现多个模块或多个工程共享ArkUI组件、资源等相关代码。HAR不同于HAP，不能独立安装运行在设备上，只能作为应用模块的依赖项被引用。

本文将介绍如何创建HAR模块、如何编译共享包。接下来，将简单介绍HAR模块的工程结构，如下图所示：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155726.53888491125538640728525782698248:50001231000000:2800:27EE252E1969E5C0387CDE863A5A0B2675CCA54DE37938A4D998755C464588F3.png)

相关字段的描述如下，其余字段与Entry或Feature模块相关字段相同，可参考[工程介绍](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-project-overview)。

- **libs**：用于存放.so文件。
- **src > main > cpp > types**：用于存放C++ API描述文件，子目录按照so维度进行划分。
- **src > main > cpp > types** **> liblibrary > Index.d.ts**：描述C++接口的方法名、入参、返回参数等信息。
- **src > main > cpp > types** **> liblibrary > oh-package.json5**：描述so三方包声明文件入口和so包名信息。
- **src > main > cpp >** **CMakeLists.txt**：CMake配置文件，提供CMake构建脚本。
- **src > main > cpp > napi_init.cpp**：共享包C++代码源文件。
- **Index.ets**：共享包导出声明的入口。

从DevEco Studio 6.0.1 Beta1开始，创建HAR模块时支持选择C++版本。

## 创建HAR模块

1. 鼠标移到工程目录顶部，单击右键，选择**New > Module**，在工程中添加模块。
2. 在**Choose Your Ability Template**界面中，选择**Static Library**，并单击**Next**。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155726.43888626788809884100727705803022:50001231000000:2800:6417E7AA3971D363F8C3E0FB84C51E67FB8EB1A99E01C26E605377A0DB89F3A2.png)
    
3. 在**Configure New Module**界面中，设置新添加的模块信息，设置完成后，单击**Finish**完成创建。从DevEco Studio 6.0.1 Beta1开始，支持选择C++版本。
    
    - **Module name**：新增模块的名称。
    - **Device type**：支持的设备类型。
    - **Enable native**：创建用于调用C++代码的模块。
    - **C++ Standard：**C++标准库，取值包括：Toolchain Default、C++11、C++14。仅打开Enable native时需要配置。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155726.63661826272151944743839091254914:50001231000000:2800:6C19C16436E30D3F4027584C20833D87F9CF55B0FC4076B08D7666AC20E7DB8A.png)
    
    创建完成后，会在工程目录中生成HAR模块及相关文件。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155726.86916347498466778587959822185190:50001231000000:2800:0B14CE2E64C89FEC08C7C2305CEE4A74A0A431B53224EC595BCE87CB3126F313.png)
    

## 编译HAR模块

开发完HAR模块后，选中模块名，然后通过DevEco Studio菜单栏的**Build > Make Module ${libraryName}**进行编译构建，生成HAR。HAR可供工程其他模块引用，或将HAR上传至ohpm仓库，供其他开发者下载使用。若部分源码文件不需要打包至HAR中，可通过[创建.ohpmignore文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-har#li5533646204511)，配置打包时要忽略的文件/文件夹。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155727.30102334398676007025061604641539:50001231000000:2800:9AD7FB68092F1F5CBD00C0988BF844FF6D4A13379AF4DD40C851DBB0FBE21911.png)

编译构建的HAR可在模块下的build目录下获取，包格式为*.har。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155727.77942613638863701612370468769143:50001231000000:2800:FE4FD91ABB561A3AD5C8FEE7470C992106368D12F38D5DFECB083AE265C4E22F.png)

在编译构建HAR时，请注意以下事项：

- 编译构建HAR的过程中，不会将模块中的C++代码直接打包进.har文件中，而是将C++代码编译成动态依赖库.so文件放置在.har文件中的libs目录下。
- 在编译构建HAR的过程中，会生成资源文件ResourceTable.txt，以便编辑器可以对HAR中的资源文件进行联想。因此，如果不使用DevEco Studio对HAR进行构建，则DevEco Studio的编辑器会无法联想HAR中的资源。
- 如果使用的Hvigor为2.5.0-s及以上版本，在编译构建HAR的过程中，会将dependencies内处于本模块路径下的本地依赖也打包进.har文件中；如果在打包后发现缺少部分本地依赖（如cpp/types目录），请参见[FAQ](https://developer.huawei.com/consumer/cn/doc/harmonyos-faqs/faqs-compiling-and-building-23)。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-creating-har-api9 "开发及发布共享包")
# 开发动态共享包

更新时间: 2025-12-16 15:57

DevEco Studio支持开发动态共享包[HSP（Harmony Shared Package）](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/in-app-hsp)。在应用/元服务开发过程中部分功能按需动态下载，或开发元服务场景时需要分包加载，可使用HSP实现相应功能。当有多个安装包需要资源共享时，也可利用HSP减少公共资源和代码重复打包。

说明

- 应用内HSP：在编译过程中与应用包名（bundleName）强耦合，只能给某个特定的应用使用。
- 集成态HSP：构建、发布过程中，不与特定的应用包名耦合；使用时，工具链支持自动将集成态HSP的包名替换成宿主应用包名。

## 使用约束

- HSP及其使用方都必须是API 10及以上版本Stage模型。
- HSP及其使用方都必须使用[模块化编译](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-esmodule-compile)模式。
- 从DevEco Studio 6.0.1 Beta1开始，创建HSP模块时支持选择C++版本。

## 开发动态共享包

### 创建HSP模块

1. 通过如下两种方法，在工程中添加新的Module。
    
    - 方法1：鼠标移到工程目录顶部，单击鼠标右键，选择**New > Module**，开始创建新的Module。
    - 方法2：选中工程目录中任意文件，然后在菜单栏选择**File > New > Module**，开始创建新的Module。
    
2. 模板类型选择**Shared Library**，点击**Next**。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155727.29321331877466557204107286596835:50001231000000:2800:9D112F9A528FB74CE4BAC8D5747F969831EA4E79A0ED996988FD72845D2FF3AB.png)
    
3. 在**Configure New Module**界面中，设置新添加的模块信息，设置完成后，单击**Finish**完成创建。从DevEco Studio 6.0.1 Beta1开始，支持选择C++版本。
    
    - **Module name**：新增模块的名称，如设置为sharedlibrary。
    - **Device type**：支持的设备类型。
    - **Enable native**：是否创建一个用于调用C++代码的模块。
    - **C++ Standard：**C++标准库，取值包括：Toolchain Default、C++11、C++14。仅打开Enable native时需要配置。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155727.52030045350055057453634883662523:50001231000000:2800:26A1CB098B96E55BB54464F250976C66195F218DE111BC5F35BCA0731867AB35.png)
    
    创建完成后，会在工程目录中生成HSP模块及相关文件。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155727.94275457622746112118157284797225:50001231000000:2800:0E226E720CCE80FE5B826CD981CDA19659B3321DC7CE37DFAD8C60C16C3F954E.png)
    

### 编译HSP模块

说明

如果HSP未开启[混淆](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-build-obfuscation)，则后续HSP被集成使用时，将不会再对HSP包进行混淆。

参考[应用内HSP开发指导](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/in-app-hsp)开发完HSP模块后，选中模块名，然后通过DevEco Studio菜单栏的**Build > Make Module ${libraryName}**进行编译构建，生成HSP。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155727.76460645051038157106127146513114:50001231000000:2800:6E90487529D0B3B0344919A78B17E3BE8C11FB1051649F732998C4113C5FEC10.png)

打包HSP时，会同时默认打包出HAR，在模块下build目录下可以看到*.har和*.hsp。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155728.41401473999412650142586532944341:50001231000000:2800:3D3CE74F1D3EAD518030589CBCAA7E93B0716D974834F1F9B702A7579C47B0AD.png)

如需在应用内共享HSP，请将HSP共享包上传至私仓（请参考[将三方库发布到 ohpm-repo](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-quickstart#zh-cn_topic_0000001792256157_%E4%BB%8Eohpm-repo%E8%8E%B7%E5%8F%96%E4%B8%89%E6%96%B9%E5%BA%93)），请先按以下操作编译生成*.tgz包。

1. 点击工具栏![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155728.64336966592429501619052292234065:50001231000000:2800:D6BE0D373F373E2FF8B89E320E48767A49A04AD5671B6CDE23B5417D02091823.png)图标将编译模式切换成release模式。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155728.11160360516092993950132194960675:50001231000000:2800:5E51FE52806C93336054FA1AA2A3E666734828FC150E901D54FD12074436187F.png)
    
2. 选中HSP模块的根目录，点击**Build > Make Module ${libraryName}**启动构建。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155728.78052071422035256789695438163247:50001231000000:2800:2E319C7D75EC0958102A7FC05B48B296EF08C8A8D4C0F0AE579F342B85A89E67.png)
    
    构建完成后，build目录下生成HSP包产物，其中.tgz用来上传至私仓。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155728.05260775554890008204272618191502:50001231000000:2800:7147196AA827EEA7D269615C5ECCFD7A3F1F51786AD7DB5D4ACE3BE55B4DBF19.png)
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-har "开发静态共享包")
# 发布共享包

更新时间: 2025-12-16 15:57

发布打包的HAR，可供其他开发者安装和引用。接下来将介绍如何发布HAR共享包。

说明

OpenHarmony三方库中心仓仅支持HAR共享包发布，不支持HSP共享包发布。如需在应用内共享HSP，可将HSP共享包发布至私仓使用，请参考[ohpm私仓搭建工具](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-overview)。

1. 在HAR模块中（与src文件夹同一级目录下），添加如下文件：
    
    - 新建README.md文件：在README.md文件中必须包含包的介绍和引用方式，还可以根据包的内容添加更详细介绍。
    - 新建CHANGELOG.md文件：填写HAR的版本更新记录。
    - 添加LICENSE文件：LICENSE许可文件。
    
2. 重新[编译HAR模块](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-har#section7892044183814)，生成*.har文件。
    
    说明
    
    若修改了HAR包模块级oh-package.json5文件中version字段信息，请先执行Build > Clean Project指令，再重新进行Build全量构建。
    
3. 利用工具ssh-keygen生成公、私钥，可执行以下命令：
    
    1. ssh-keygen -m PEM -t RSA -b 4096 -f ~/.ssh_ohpm/mykey 
    
    说明
    
    2. ~/.ssh_ohpm/mykey 为私钥文件 mykey 的文件路径，按照实际情况指定。指定的私钥存储目录必须存在。
    3. 追加了.pub后缀的相应公钥文件会存放在和私钥相同的目录下。
    4. OHPM包管理器只支持加密密钥认证，请在生成公私钥时输入密码。
    
4. 登录[OpenHarmony三方库中心仓](https://ohpm.openharmony.cn/#/cn/home)官网，单击主页右上角的**个人中心，** 新增OHPM公钥，将公钥文件（mykey.pub）的内容粘贴到公钥输入框中。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155729.27883857508334860303298343255009:50001231000000:2800:1AF99267E905A663AE3A8974AFC78F7C0036EBFCFF1E438DDC74870F81FA1B52.png)
    
5. 打开命令行工具，将对应私钥文件路径配置到 .ohpmrc 文件中 key_path 字段上，可执行以下命令进行配置：
    
    1. ohpm config set key_path  ~/.ssh_ohpm/mykey
    
6. 登录[OpenHarmony三方库中心仓](https://ohpm.openharmony.cn/)官网，单击主页右上角的**个人中心**，复制发布码，获取发布码并配置到 .ohpmrc 文件中，可执行如下命令：
    
    1. ohpm config set publish_id your_publish_id
    
7. 执行如下命令发布HAR，<HAR路径>需指定为.har文件的具体路径。
    
    1. ohpm publish <HAR路径>  
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hsp "开发动态共享包")
# 引用及管理共享包

更新时间: 2025-12-16 15:57

引用三方HAR，包括从仓库进行安装、从本地文件夹和本地压缩包中进行安装三种方式。

- 引用ohpm仓中的HAR，首先需要设置三方HAR的仓库信息，DevEco Studio默认仓库地址为OpenHarmony三方库中心仓，如果您想设置自定义仓库，请在DevEco Studio的**Terminal**窗口执行如下命令进行设置（执行命令前，请确保已[将ohpm配置到环境变量中](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-environment-config#zh-cn_topic_0000001056725590_li1012418311835)，第一次配置环境变量后，需重启DevEco Studio）：
    
    1. ohpm config set registry your_registry1,your_registry2
    
    说明：ohpm支持多个仓库地址，采用英文逗号分隔。
    
    支持通过如下方式配置三方包依赖信息：
    
    - 方式一：在菜单栏点击**Tools >** **OHPM Index**，进入DevEco Studio内置的OpenHarmony开源中心仓，选择需要的三方包，详情请参考[使用OpenHarmony开源中心仓管理三方包](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-har-import#section1579838153916)。
        
        说明
        
        方式一仅支持中国境内（香港特别行政区、澳门特别行政区、中国台湾除外）。
        
    - 方式二：在**Terminal**窗口中，切换到需要引入三方包的模块，如entry模块，执行如下命令安装三方包，DevEco Studio会自动在该模块的oh-package.json5中自动添加三方包依赖。
        
        1. cd path/to/your/project/entry
        2. ohpm install @ohos/lottie
        
    - 方式三：在需要引入三方包的模块的oh-package.json5中设置三方包依赖，配置示例如下：
        
        1. "dependencies": {
        2.   "@ohos/lottie": "^2.0.0"
        3. }
        
        依赖设置完成后，需要执行**ohpm install**命令安装依赖包，依赖包会安装到该模块的oh_modules目录下。
        
        4. ohpm install
        
    
- 引用本地模块源码（该本地模块必须与宿主模块归属于同一个工程），如entry模块需要依赖foo模块的源码，有如下两种方式：
    - 方式一：在**Terminal**窗口中，切换到需要引入本地模块源码的模块，即entry模块下，执行如下命令进行安装，并会在该模块下的oh-package.json5中自动添加依赖。
        
        1. cd path/to/your/project/entry
        2. ohpm install path/to/foo
        
    - 方式二：在需要引入本地模块源码的模块的oh-package.json5中设置源码依赖项，即entry模块的oh-package.json5中，添加如下配置：
        
        1. "dependencies": {
        2.   "foo": "file:path/to/foo"  // 此处也可以是以当前oh-package.json5所在目录为起点的相对路径
        3. }
        
        依赖设置完成后，需要执行**ohpm install**命令安装依赖包，模块foo的源码会安装在entry模块的oh_modules目录下。
        
        4. ohpm install
        

- 引用本地HAR/HSP包，有如下两种方式：
    - 方式一：在**Terminal**窗口中，切换到需要引入本地HAR/HSP包的模块，如entry模块，执行如下命令进行安装，并会在oh-package.json5中自动添加依赖。以HAR/HSP包在工程根目录下为例，配置示例如下（实际配置时请以HAR/HSP包实际目录为准）：
        - 引用HAR：
            
            1. cd path/to/your/project/entry
            2. ohpm install path/to/package.har
            
        - 引用HSP（*.tgz包通过HSP模块在release模式下[编译](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hsp#section67683213597)生成）：
            
            1. cd path/to/your/project/entry
            2. ohpm install path/to/package.tgz
            
    - 方式二：在需要引入三方包的模块的oh-package.json5中设置本地HAR/HSP包。以HAR/HSP包在工程根目录下为例，配置示例如下（实际配置时请以HAR/HSP包实际目录为准）：
        
        - 引用HAR：
            
            1. "dependencies": {
            2.   "package": "file:path/to/package.har" // 此处也可以是以当前oh-package.json5所在目录为起点的相对路径。 
            3. }                                       
            
            说明
            
            代码片段中package.har为三方包文件名；"package"为引用该三方包所使用的依赖名称，建议与三方包包名，即三方包的oh-package.json5文件中的name字段保持一致。
            
        
        - 引用HSP：
            
            1. "dependencies": {
            2.   "package": "file:path/to/package.tgz" // 此处也可以是以当前oh-package.json5所在目录为起点的相对路径
            3. }
            
        
        依赖设置完成后，需要执行**ohpm install**命令安装依赖包，依赖包会安装在该模块的oh_modules目录下。
        
        1. ohpm install
        

另外，在安装或卸载共享包时，可在模块或工程的oh-package.json5文件中增加钩子设置，以管理install、uninstall命令的生命周期，配置示例如下：

1.  "hooks": {
2.     "preInstall": "echo 00 preInstall", // install命令执行之前
3.     "postInstall": "echo 00 postInstall", // install命令执行之后
4.     "preUninstall": "echo 00 preUninstall", // uninstall命令执行之前
5.     "postUninstall": "echo 00 postUninstall"  // uninstall命令执行之后
6.   }

说明

- 目前只支持执行当前模块或工程的oh-package.json5文件中hooks，不支持执行依赖中hooks。
- 在引用共享包时，请注意当前只支持在模块和工程下的oh-package.json5文件中声明dependencies依赖，才会被当做依赖使用，并在编译构建过程中进行相应的处理。

## 使用OpenHarmony开源中心仓管理三方包

说明

该功能仅支持中国境内（香港特别行政区、澳门特别行政区、中国台湾除外）。

从DevEco Studio 6.0.0 Beta5版本开始，新增OHPM Index入口，提供OHPM开源中心仓的高效筛选和管理能力，提升开发者选型开发效率，消减因软件信息不对称导致的选型使用风险，快速选择与定位所需的开源三方库。

1. 在菜单栏点击**Tools >** **OHPM Index**，进入OpenHarmony开源中心仓。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155724.96158870428592002736788671940440:50001231000000:2800:F00B2EC96B194DA04179EDE0ED83B6A743D4E9470F31447E19BCB054A605164A.png)
    
2. 在左侧搜索框可查询三方包名称，或点击目录树，根据分类查看不同分类下推荐的依赖包信息。选定所需要安装的三方包，点击右上角蓝色按钮**Install**进行安装。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155724.00264262641773983074414697268819:50001231000000:2800:66717839EA42F894029B4F5B54D2094C7D75B0A957300123BC0E7D44B311B5B6.png)
    
3. 安装过程中，如出现下方弹窗，点击**Add**按钮，将OpenHarmony中心仓地址添加到.ohpmrc文件中。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155724.00750492006311236153150700743102:50001231000000:2800:EFBBBAD07303D5AD3A05D1D6D001BC5655AE54CA1C312DA156E26E1E20445319.png)
    
4. 三方包安装完成后，在工程级oh-package.json5文件中可以看到已安装的三方包名称及版本信息，oh_modules中将同时添加该三方包。
5. 点击页面左上角![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155724.18995227090500129426534846495101:50001231000000:2800:E4A02DB855B5AC0AD9A2C726956B2F1CF5D00BBEEC83E904C7612E5267411E0D.png)图标，展示当前已安装的三方包信息。若当前三方包非最新版本，可以点击右上角**Update**按钮，更新至最新版本；点击**Delete**按钮，可以删除当前已安装的三方包。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155724.01244474986786530676248197887189:50001231000000:2800:8F88149E7CFD999C63FA8B99484013ED53296E1C0D8DD112DBEBD3C61D948488.png)
    
6. 若对于已使用的三方包依赖存在推荐的同类三方包，可点击编辑界面中黄色灯泡图标，在弹框中选择**Replace selected with recommended library**，将当前依赖替换为推荐的三方包依赖；或选择**Replace all with recommended libraries**，一键替换当前文件中所有同类推荐三方包。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155724.70550109990468813309011030061990:50001231000000:2800:7C791A4A71AD9B1D805D86D96CEACE9007C8229BDA3B9F3F425BF4E4D0B2CB7D.png)
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-har-publish "发布共享包")
# 概述

更新时间: 2025-12-16 15:57

ohpm-repo是一个搭建轻量级的ohpm私仓服务的工具。它与ohpm包管理器兼容，并按需缓存所有依赖项，加速私有网络中的安装。

## 私有性

所发的三方库都是私有的，只能根据配置进行访问。

## 缓存

ohpm-repo根据需要缓存所有依赖项，加快私有网络的安装速度。

## 部署

ohpm-repo支持单点部署和多实例部署。

说明

- 单点部署：ohpm-repo仅部署在一台机器上使用。
- 多实例部署：ohpm-repo会部署到多台机器中，具有相同的配置内容，并且共享数据存储空间。
- 单点部署的数据如果需要迁移至多实例部署，请参考[数据迁移指导](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-data-migration)。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo "ohpm-repo私仓搭建工具")
# 快速开始

更新时间: 2025-12-16 15:57

说明

ohpm-repo私仓不允许在Linux或macOS系统中使用root用户启动，请使用普通用户安装运行。

## 如何安装

### ohpm-repo

1. ohpm-repo依赖于Node运行，支持Node.js18.x及以上版本，请提前安装Nodejs，并完成环境变量的配置。Node.js安装请参考[Node.js官方网站](https://nodejs.org/download/release/latest/)。
    
2. 下载ohpm-repo私仓工具包。请在[下载中心](https://developer.huawei.com/consumer/cn/download/ohpm-repo)获取最新的ohpm-repo，并根据下载中心页面**工具完整性**指导进行完整性校验。
    
3. 解压ohpm-repo私仓工具包。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155728.26953948755514565847554434430571:50001231000000:2800:397F3C62BC6D38C7DCE6E6C08564715A98345AF1C629D13E9C39949F9FCFC696.png)
    
4. 请将ohpm-repo工具包解压目录中bin目录的路径配置到[系统环境变量](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-faq#section24117279211)path中，执行如下查询命令:
    
    1. ohpm-repo -v
    
    终端输出版本号（如：2.0.0），则表示安装包解压无问题。如有报错，请参考[常见问题FAQ](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-faq)解决。
    
    注意
    
    针对Linux和Mac系统，建议使用bash或zsh作为命令行界面。如果使用其他类型shell，写入ohpm-repo部署根目录[deploy_root](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#zh-cn_topic_0000001745376470_deploy_root)的环境变量时，默认写入.bashrc文件中。
    
5. 在启动ohpm-repo前，需要先按照如下方式完成配置修改：进入ohpm-repo解压目录的conf目录内，打开config.yaml[配置文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration)。
    
    说明
    
    **ohpm-repo成功启动后修改配置文件方法**：
    
    - 首次启动ohpm-repo时执行**install**命令已指定配置文件：找到指定的配置文件进行文件内容修改，然后重新执行install指定修改后的配置文件，再执行start启动ohpm-repo。
    - 首次启动ohpm-repo时执行**install**命令未指定配置文件：默认使用ohpm-repo压缩包解压路径下conf目录中的配置文件，修改该文件内容，然后重新执行install和start操作。
    
6. 检查[listen](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#zh-cn_topic_0000001745376470_listen)配置，默认配置为localhost:8088，表示仅支持监听本机地址；如果希望其他机器通过ip/域名访问，则建议修改listen配置为ohpm-repo部署机器的ip：
    
    1. listen: <部署ohpm-repo机器的ip>:8088
    
7. 检查[deploy_root](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#zh-cn_topic_0000001745376470_deploy_root)配置：如果不配置，会存储在默认地址中。该路径不允许配置为ohpm-repo解压根目录。
8. 检查[db](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#zh-cn_topic_0000001745376470_db)和[store](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#zh-cn_topic_0000001745376470_store)配置，db是元数据存储的配置项，store是文件存储的配置项。db支持fileDB本地存储和mysql数据库存储，store支持file storage本地存储，sftp storage存储和custom storage自定义插件存储。db和store不能随意搭配，需要符合表1的匹配规范。配置文件默认db使用fileDB本地存储，store使用file storage本地存储。
    
    **表1** db配置项与store配置项的搭配选择
    |db：元数据存储|与db所适配的store类型|
    |:--|:--|
    |fileDB|file storage|
    |mysql|file storage，sftp storage， custom storage|
    
9. 检查是否配置了[store.config.server](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#zh-cn_topic_0000001745376470_store)，用于指定ohpm-repo仓库内容的下载地址、不配置取默认值，详情见：[server: 仓库内容的下载地址](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#zh-cn_topic_0000001745376470_li922300957171146)。如果[listen](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#zh-cn_topic_0000001745376470_listen)的host为0.0.0.0，且本机存在多个网络接口，那么该值必须配置，建议手动修改host为本机指定的ip/域名，例如listen为0.0.0.0:8088，故server需配置为http://<指定部署机器的ip/域名>:8088。
    
    说明
    
    - 如果为ohpm-repo服务配置了反向代理服务器，则该地址需要填写为反向代理服务器的地址。
    - 如果ohpm-repo以多实例方式启动，必须配置反向代理服务器，多个实例之间需要统一的下载地址。
    - config.yaml中各项配置的详细描述请见：[配置文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration)。
    
10. 进入ohpm-repo工具包解压目录中的bin目录下，执行安装命令:
    
    1. ohpm-repo install
    
    结果实例：
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155728.09761820138153434835407729510598:50001231000000:2800:75B03BBD6D59C450EAB2052042A47077E8D7C72A06CAFC037D20D46FA3E23FC7.png "点击放大")
    
11. 安装成功后，**必须**根据给出的提示信息刷新部署目录的环境变量，针对Windows系统和Linux/Mac系统，有不同处理方式：
    
    - Windows系统：关闭当前窗口，重新开启一个窗口。
    - Linux/Mac系统：在命令行中执行刷新命令：当shell为bash时执行_source ~/.bashrc_或者. _~/.bashrc_；当shell为zsh时执行_source ~/.zshrc_或者. _~/.zshrc_。
    

## 如何启动

ohpm-repo安装成功后，进入ohpm-repo工具包解压目录下的bin目录下，执行如下命令，启动ohpm-repo：

1. ohpm-repo start

启动成功，将会出现以下日志信息：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155728.23256220499120318108885047551030:50001231000000:2800:A56E5370C658F380F27C47495D1E448B62FE2196E3FECACB6ADF751FBD55E912.png "点击放大")

说明

ohpm-repo首次启动时，默认创建一个管理员账号，账号名称：_**admin**_，密码：_**12345Qq!**_。该账号在首次登录时，需要修改其密码，请修改密码后，重新登录该账号。

## 从ohpm-repo获取三方库

可以为所有项目配置该私有仓，例如执行以下命令：

1. ohpm config set registry <配置的ohpm-repo私仓服务地址>/repos/ohpm
2. ohpm install

或者在命令行中配置参数--registry使用，例如以下命令：

1. ohpm install @ohos/lottie --registry <配置的ohpm-repo私仓服务地址>/repos/ohpm

说明

<配置的ohpm-repo私仓服务地址>：配置文件中[store.config.server](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#zh-cn_topic_0000001745376470_store)的地址信息，例如：_[store.config.server](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#zh-cn_topic_0000001745376470_store):为http://127.0.0.1:8088_，故registry为：_http://127.0.0.1:8088/repos/ohpm。_如果[store.config.server](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#zh-cn_topic_0000001745376470_store)没有配置，取默认值。

## 将三方库发布到ohpm-repo

三方库包含静态共享包HAR包和动态共享包HSP包，可以通过ohpm命令行工具和使用Web页面两种方式发布。

说明

从ohpm命令行工具1.3.0版本和ohpm-repo私仓1.1.0版本开始，支持动态共享包HSP包以.tgz文件形式发布到ohpm-repo，之前版本仅支持发布以.har文件形式的静态共享包。

### 使用命令行工具发布

1. 利用工具ssh-keygen生成公、私钥，可执行以下命令：
    
    1. ssh-keygen -m PEM -t RSA -b 4096 -f <your_key_path>
    
    说明
    
    - <your_key_path>：配置公钥和私钥的名称和存放路径，仅包含名称时，以当前命令行工作路径为存储目录。
    - OHPM包管理器只支持加密密钥认证，请在生成公私钥时输入密码。
    
    示例：
    
    1. ssh-keygen -m PEM -t RSA -b 4096 -f D:\path\my_key_path
    
    说明
    
    公钥和私钥存储在D盘的path目录下，公钥和私钥名称分别为my_key_path.pub和my_key_path。
    

2. 登录ohpm-repo私仓管理地址，单击主页右上角的个人中心 > 认证管理，新增公钥，将公钥文件（<your_key_path>.pub）的内容粘贴到公钥输入框中。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155729.86139986513094915514745675469529:50001231000000:2800:4E60B8574B776151C02F433BA95A4AAB663EF2435CDE539262847BD8EBF02AB5.png "点击放大")
    

3. 打开命令行工具，执行如下命令设置私钥路径。
    
    1. ohpm config set key_path <your_key_path>
    

4. 登录ohpm-repo私仓管理地址，单击主页右上角的个人中心，复制发布码。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155729.04770257570213834202218770973228:50001231000000:2800:63F82E297B5FE13E85810D2C1B63398CC917CE8621EF1B719A3C19DAD7AB997D.png "点击放大")
    

5. 将发布码配置到.ohpmrc文件中，可执行如下命令：
    
    1. ohpm config set publish_id <your_publish_id>
    

6. 三方库包含静态共享包HAR包和动态共享包HSP包，发布方式存在不同。
    
    - 静态共享包HAR包
        
        执行 ''ohpm publish <HAR包路径>'' 命令发布HAR包，<HAR包路径> 指向的文件后缀需为.har文件的具体路径。例如执行以下命令：
        
        1. ohpm config set publish_registry <ohpm-repo私仓管理地址>/repos/ohpm
        2. ohpm publish demo.har
        
        或在命令行中配置参数--publish_registry使用，例如以下命令：
        
        1. ohpm publish demo.har --publish_registry <ohpm-repo私仓管理地址>/repos/ohpm
        
    
    - 动态共享包HSP包
        
        动态共享包HSP包不能直接发布在ohpm-repo内，需要先转化为.tgz包，转换方法见：[编译HSP模块](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hsp#section67683213597)。TGZ包的发布流程同HAR一致。
        
        执行 ''ohpm publish <TGZ包路径>'' 命令发布TGZ包，< TGZ 包路径> 指向的文件后缀需为.tgz文件的具体路径。例如执行以下命令：
        
        1. ohpm config set publish_registry <ohpm-repo私仓管理地址>/repos/ohpm
        2. ohpm publish demo.tgz
        
        或在命令行中配置参数--publish_registry使用，例如以下命令：
        
        1. ohpm publish demo.tgz --publish_registry <ohpm-repo私仓管理地址>/repos/ohpm
        
    
    说明
    
    - 开发HAR包和HSP包，HSP生成.tgz包和.tgz格式共享包转换为.har格式等更详细内容请参考：[开发及引用共享包](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-creating-har-api9)。
    - 发布时ohpm-repo私仓管理地址填写规则如下：
        - listen的host不为0.0.0.0时， 管理地址使用[listen](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#zh-cn_topic_0000001745376470_listen)的完整格式，例如：当listen：localhost:8088，此处ohpm-repo私仓管理地址应填写：http://localhost:8088。
        - listen的host为0.0.0.0时，host需更改为ohpm-repo私仓部署机器的ip/域名，例如：当listen：0.0.0.0:8088，此处ohpm-repo私仓管理地址应填写：http://<ohpm-repo私仓部署机器的ip/域名>:8088。
    

### 使用Web页面发布

在Web页面用管理员账号登录ohpm-repo私仓管理地址，在个人中心 > 仓库管理中，点击管理三方包 > 上传三方包，包的后缀名必须为.har或者.tgz。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155729.70907301552523824327609617495094:50001231000000:2800:81E8BDFDC22A9A67CA215F760752EB759CA2481D4F324136F96CB11E4B4C3C46.png "点击放大")

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155729.99059356379224716837500933380524:50001231000000:2800:39606E0F346DBED7585EA95458438D7580C764D6F1FF778BC0D7033F13276DBA.png "点击放大")

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-overview "概述")
# 配置文件

更新时间: 2025-12-16 15:57

config.yaml是ohpm-repo的重要文件，可以在其中修改默认参数配置，启动插件和扩展功能。ohpm-repo私仓解压目录中的conf目录下带有一个默认配置文件config.yaml，ohpm-repo执行install命令时默认读取该文件。

说明

**ohpm-repo成功启动后修改配置文件方法**：

- 首次启动ohpm-repo时执行**install**命令时已指定配置文件：找到指定的配置文件进行文件内容修改，然后重新执行install指定修改后的配置文件，再执行start启动ohpm-repo。
- 首次启动ohpm-repo时执行**install**命令未指定配置文件：默认使用ohpm-repo压缩包解压路径下conf目录中的配置文件，修改该文件内容，然后重新执行install和start操作。

## 默认配置

1. ##### server configuration section #####
2. listen: localhost:8088        # 建议修改为具体的ip/域名
3. # listen:
4. # - localhost:8088            # 监听本机环回地址
5. # - http://localhost:8088     # 监听本机环回地址
6. # - 0.0.0.0:8088              # 监听本机所有地址 (INADDR_ANY)
7. # 协议可配置 http 或者 https，默认为 http
8. # port: 1-65535(Windows系统)/ 1024-65535(Linux或Mac系统）

9. # 可选 (listen 为 https 协议时必须配置)
10. https_key: ''                 # https 服务使用的 key 的路径  (不配置默认为'')
11. https_cert: ''                # https 服务使用的 crt 的路径  (不配置默认为'')

12. ##### server deploy root section #####
13. deploy_root: ''                # 安装根目录，只支持绝对路径，且目录必须存在

14. ##### server numeric limit section #####
15. max_package_size: 500          # 上传包大小限制，单位是MB (0, 500]，不配置或配置为0默认为 500
16. max_extract_size: 800          # 压缩包解压后大小限制，单位是MB ，不配置或配置为0默认为 800
17. max_extract_file_num: 30000    # 压缩包解压后文件个数限制，不配置或配置为0默认为30000个
18. user_rate_limit: 100           # 用户访问频率控制，单位是次/小时 (0, 10000]，不配置或配置为0默认为 100
19. fetch_timeout: 60              # 请求/响应的超时时间，单位是秒 (0, 3600]，不配置或配置为0默认为 60
20. keep_alive_timeout: 60         # TCP 保持连接的超时时间，单位是秒 (0, 3600]，不配置或配置为0默认为 60
21. api_timeout: 60                # api超时时间，单位是秒(0, 3600]，不配置或配置为0默认为 60
22. upload_api_timeout: 300        # 上传三方包api超时时间，单位是秒(0, 3600]，不配置或配置为0默认为 300
23. upload_lock_hour: 24           # 下架某一三方包所有版本后，限时禁止同名三方包上传，单位是小时 (0, 168]，不配置或配置为0默认为 24
24. upload_max_times: 100          # 单用户24小时内上传次数限制 (0, 100000]，不配置或配置为0默认为 100
25. operation_log_retention: 100   # 数据库中操作日志保留时间，单位是天，不配置或配置为0默认为 100

26. ##### metadata storage section #####
27. ## 数据存储类型 filedb 和 mysql 二选一，不可都配置
28. db:                         # 必须用 yaml 数组形式写法
29.   type: filedb
30.   config:                   # 如果想修改存储路径且保留旧的数据，则需要把旧路径下的数据文件迁移至新路径
31.     path: ./db              # 本地数据存储路径，不配置默认为<deploy_root>/db;

32. #db:                        # 必须用yaml数组形式写法
33. #  type: mysql
34. #  config:
35. #    host: "localhost"      # 数据库主机地址
36. #    port: 3306             # 数据库端口 (0,65535]
37. #    username: tctAdmin         # 数据库的用户名
38. #    password: "password"   # 数据库的用户密码（请配置明文, 最终在部署目录中会转换为密文）
39. #    database: "repo"       # 数据库名

40. ##### storage section #####
41. ## 文件存储类型fs,sftp 和 custom 三选一，不可多选。

42. store:                               # 必须用 yaml 数组形式写法
43.   type: fs
44.   config:                            # 上传资源后如若要修改存储路径，则需要把旧路径下的数据迁移至新路径中
45.     path: ./storage                  # 已上架三方库存储路径，不配置默认为 <deploy_root>/storage;
46.     #server: http://localhost:8088   # 仓库下载链接地址，不配置取默认值

47. # 文件存储类型为 sftp 时，最多配置三个 sftp
48. #store:                               # 必须用 yaml 数组形式写法
49. #  type: sftp                         # 当且仅当 db 的类型为 mysql 时，store 的类型才能为 sftp
50. #  config:
51. #    location:
52. #      -
53. #        name: test_one_sftp          # 主机名字不能与其他sftp配置重复
54. #        host: "localhost"            # 主机地址
55. #        port: 22                     # 主机端口 (0,65535]
56. #        read_username: "read"        # 主机有读权限的用户名字
57. #        read_password: "password"    # 主机有读权限的用户密码（请配置明文, 最终在部署目录中会转换为密文）
58. #        write_username: "write"      # 主机有写权限的用户名字
59. #        write_password: "password"   # 主机有写权限的用户密码（请配置明文, 最终在部署目录中会转换为密文）
60. #        path: /source22              # 相对 sftp 根目录的文件路径，仅限/开头，且路径文件夹必须存在
61. #      -
62. #        name: test_two_sftp
63. #        host: "localhost"
64. #        port: 24
65. #        read_username: "read"
66. #        read_password: "password"
67. #        write_username: "write"
68. #        write_password: "password"
69. #        path: /source24
70. #    #server: http://localhost:8088   # 仓库下载链接地址，不配置取默认值

71. #store:
72. #  type: custom                                            # custom是自定义存储插件类型，自定义存储插件开发流程见[指导文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-storageplugin)
73. #  config:
74. #    export_name: CustomStorage                            # 插件export的类名
75. #    plugin_path: plugins/CustomStorage.js                 # 插件的绝对路径或者相对于ohpm-repo软件包的路径，建议将插件放在软件包的plugins目录下
76. #    custom_field: "test"                                  # 自定义字段，通过引入libs/common/getStorageConfigInfo.js的getStorageConfigInfo方法获取自定义字段的值
77. #    #server: http://localhost:8088                        # 仓库下载链接地址，不配置取默认值

78. ##### 是否使用反向代理 #####
79. # 可选项:true,false, 默认：false。如果使用反向代理，需要配置为true，客户端IP地址将从请求头中的x-forwarded-for字段获取
80. use_reverse_proxy: false

81. ##### uplink section #####
82. uplink_cache_path: ./uplink      # 缓存路径，不配置默认为 <deploy_root>/uplink
83. uplink_cache_time: 168           # 远程包 metadata 缓存时间，单位为小时，默认 168 小时，取值范围为 (0, 8760]

84. ##### log section #####
85. logs_path: ./logs                # 日志路径，不配置默认为 <deploy_root>/logs

86. ##### log level section #####
87. # 日志级别: 级别由低到高分别是 all、trace、debug、info、warn、error、fatal、mark、off
88. # run，operate 和 access 不配置或者配置错误，默认为 info
89. loglevel_run: info
90. loglevel_operate: info
91. loglevel_access: info

92. ##### auth plugin section #####
93. # 可选项，自定义认证插件配置
94. #auth_plugin:
95. #  name: CustomAuth              # 认证插件的名字
96. #  path: plugins/CustomAuth.js   # 插件的绝对路径或者相对于ohpm-repo软件包的路径，建议将插件放在软件包的plugins目录下

97. ##### fieldCheck plugin section #####
98. # 可选项，自定义元数据规则检验插件配置
99. #field_check_plugin:
100. #  config_file_path:  plugins/fieldCheckPlugin/CustomExtensionValidationConfig.json  # 字段校验配置文件的绝对路径或者相对于ohpm-repo软件包的路径，建议将文件放在软件包的plugins/fieldCheckPlugin目录下
101. #  check_func_dir: plugins/fieldCheckPlugin                                          # 字段校验函数文件所在目录的绝对路径或者相对于ohpm-repo软件包的路径，建议将目录设置为plugins/fieldCheckPlugin文件夹

102. ##### content check plugin #####
103. # 可选项，包内容规则检测插件配置
104. #content_check_plugin:
105.   # 该校验要求环境变量中有ark_disasm可执行文件、tar命令行工具
106.   # 检查范围：上架的字节码har、hsp
107. #  name: 'OHMUrlCheck'

108. ##### compatibleSdkVersion等兼容性字段检测日志等级 #####
109. # 可选值：close、info、warn、error，默认：warn
110. compability_log_level: warn

111. ##### 是否允许下架被其他组件依赖的包 #####
112. # 可选项:true,false, 默认：false
113. allow_remove_depended_packages: false

## 配置项说明

### listen

格式为三段式，即<proto>://<host>:<port>，其中<proto>可以不填，默认为http，如：

- 监听本机回环地址（默认）：
    
    1. listen: localhost:8088
    2. # 或 listen: http://localhost:8088
    
- 监听具体地址（建议）：
    
    1. listen: https://<ohpm-repo部署机器ip>:8088
    
- 监听所有地址（当选择监听所有地址时，配置项[store](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#zh-cn_topic_0000001745376470_store)中server值必须配置）：
    
    1. listen: 0.0.0.0:8088
    2. # 或 listen: http://0.0.0.0:8088
    

注意

listen值建议监听具体的地址。proto支持http和https协议，支持缺省，缺省时默认为http。为了确保ohpm-repo链接的安全，建议选择使用https协议，如果配置为https协议，则需要完善[https](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#zh-cn_topic_0000001745376470_https)相关配置。

### https

当配置[listen](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#zh-cn_topic_0000001745376470_listen)时选择使用https协议，则需要配置https_key和https_cert：

- https_key：ssl证书私钥文件。
- https_cert：ssl证书文件。

参考配置如下：

1. https_key: ./ssl/server.key
2. https_cert: ./ssl/server.crt

说明

生产环境必须使用受信任CA颁发的证书，避免因使用自签名证书导致浏览器安全警告。

### deploy_root

ohpm-repo的部署目录，存储运行时生成的文件数据。

- 如果<deploy_root>字段为空，则默认路径为：
    
    windows系统: ~/AppData/Roaming/Huawei/ohpm-repo
    
    其他操作系统：~/ohpm-repo
    
- 如果<deploy_root>字段不为空，则路径必须为**绝对路径**，且路径所指向文件夹**必须存在**。
    
- 该路径不允许配置为ohpm-repo安装包解压根目录。

参考配置如下：

1. deploy_root: ''

### server

服务相关配置，具体为：

- **max_package_size**: 上传包大小限制，单位为MB， 不配置或配置为0取默认值500MB，取值范围为 (0, 500] 。
- **max_extract_size**: 压缩包解压后大小限制，单位为MB，不配置或配置为0取默认值800MB。
- **max_extract_file_num**: 压缩包解压后文件个数限制，不配置或配置为0取默认值30000个。
- **user_rate_limit**: 用户访问频率控制，单位为次/秒，不配置或配置为0取默认值100 次/秒，取值范围为 (0, 10000]。
- **fetch_timeout**: 当使用[uplink](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#zh-cn_topic_0000001745376470_uplink)时，请求uplink数据的请求/响应超时时间，单位为秒，不配置或配置为0取默认值60秒，取值范围为 (0, 3600]。
- **keep_alive_timeout**: TCP 保持连接的超时时间，单位为秒，不配置或配置为0取默认值60秒，取值范围为 (0, 3600]。
- **api_timeout**: 接口请求与响应超时时间，单位为秒，不配置或配置为0取默认值60秒，取值范围(0, 3600]。
- **upload_api_timeout**: 上传三方包接口请求与响应超时时间，单位为秒，不配置或配置为0取默认值300秒，取值范围(0, 3600]。
- **upload_lock_hour**: 下架某个三方包所有版本后，限时禁止同名三方包上传，单位为小时，不配置或配置为0取默认值24小时，取值范围为 (0, 168]。
- **upload_max_times**: 单用户24小时内上传次数限制，不配置或配置为0取默认值100次，取值范围为 (0, 100000]。
- **operation_log_retention**：数据库中操作日志保留时间，单位是天，不配置或配置为0取默认值100天。

参考配置如下：

1. max_package_size: 500
2. max_extract_size: 800
3. max_extract_file_num: 30000
4. user_rate_limit: 100
5. fetch_timeout: 60
6. keep_alive_timeout: 60
7. api_timeout: 60
8. upload_api_timeout: 300
9. upload_lock_hour: 24
10. upload_max_times: 100
11. operation_log_retention: 100   

注意

db是元数据存储的配置项，store是文件存储的配置项。db支持fileDB本地存储和mysql数据库存储；store支持file storage存储，sftp存储和custom storage 自定义插件存储。db和store不能随意搭配，需要符合表1的匹配规范：

**表1** db配置项与store配置项的搭配选择
|db：元数据存储|**与db所适配的store：三方包文件存储**|
|:--|:--|
|filedb|file storage|
|mysql(ohpm-repo 1.1.0开始支持）|file storage，sftp storage(ohpm-repo 1.1.0开始支持），custom storage(ohpm-repo 2.2.0开始支持）|

### db

ohpm-repo运行过程产生的用户信息，运行状态等元数据存储配置，支持本地磁盘存储filedb和mysql数据库存储。

**本地磁盘存储**

默认使用本地磁盘存储，配置如下：

- type: 存储插件名称，为filedb。
- config: 插件配置，具体为：
    - path: 数据库文件存储地址，默认值为./db，支持相对和绝对路径配置，当配置为相对路径时，则以[deploy_root](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#zh-cn_topic_0000001745376470_%E5%85%B3%E4%BA%8E-deploy_root)为根目录。

说明

如果想修改数据库文件存储路径同时保留旧的数据，则需要把旧路径下的数据文件迁移至新路径。

参考配置如下：

1. db:                
2.   type: filedb     
3.   config:
4.     path: ./db     

**Mysql存储**

- type: 插件名称，配置为mysql。
- config: 插件配置，具体为：
    - host: 数据库主机地址。
    - port: 数据库端口。
    - username: 数据库的用户名。
    - password: 数据库的用户密码（请配置明文, 最终在部署目录中会转换为密文）。
    - database: 数据库名。

参考配置如下：

1. db:                         
2.   type: mysql
3.   config:
4.     host: "localhost"
5.     port: 3306
6.     username: "tctAdmin"
7.     password: "password"
8.     database: "repo"

注意

为了避免潜在的安全风险，建议使用非最高权限的数据库账户进行连接。

### store

三方库及其元数据等资源文件存储配置，支持本地磁盘存储，sftp存储和自定义插件存储。

**本地磁盘存储**

默认使用本地磁盘存储文件，具体配置为：

- type: 插件名称，为fs。
- config: 插件配置，具体为：
    - path: 存储根目录路径，默认为./storage，支持相对和绝对路径配置，当配置为相对路径时，则以[deploy_root](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#zh-cn_topic_0000001745376470_%E5%85%B3%E4%BA%8E-deploy_root)为根目录。
    - server: 仓库内容的下载地址，当[listen](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#zh-cn_topic_0000001745376470_listen)的host为0.0.0.0且本机存在多个网络接口时，**必须配置**。
        - server的格式如下：<[listen](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#zh-cn_topic_0000001745376470_listen)的proto>://<host>:<[listen](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#zh-cn_topic_0000001745376470_listen)的port>；
        - 当配置项[listen](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#zh-cn_topic_0000001745376470_listen)的host不为0.0.0.0时，则server**默认**取listen的完整格式，例如listen为127.0.0.1:8088，故server默认值为http://127.0.0.1:8088；
        - 当配置项[listen](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#zh-cn_topic_0000001745376470_listen)的host为0.0.0.0时，如果本机仅存在一个网络接口，则server中的host默认为本机网络接口的ipv4地址；如果本机存在多个网络接口，则server中的host默认为本机获取到的第一个网络接口的ipv4地址，建议手动修改host为指定的本机ip/域名，例如listen为0.0.0.0:8088，故server需配置为http://<本机ip/域名>:8088；
        - 如果需要通过反向代理来访问ohpm-repo服务，则该字段须配置为反向代理服务器的域名地址，且需要配置[use_reverse_proxy](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#section1074004784011)值为true。

注意

上传资源后如若要修改存储路径，则需要把旧路径下的数据迁移至新路径中。

参考配置如下：

1. store:
2.   type: fs
3.   config:
4.     path: ./storage
5.     #server: http://localhost:8088

**sftp 存储**

支持使用sftp存储文件，仅当数据存储为mysql存储时才能使用sftp存储，具体配置为：

- type: 插件名称，其名称为sftp。
- config: 插件配置。
    - location: 支持配置最多3个sftp服务，必须用yaml的数组形式写法，详细配置如下；
        - name: sftp服务名，名字不能与其他sftp配置重复。
        - host: sftp服务主机地址。
        - port：sftp服务端口。
        - read_username：有读权限的用户名。
        - read_password：有读权限的用户密码（请配置明文, 最终在部署目录中会转换为密文)。
        - write_username：有写权限的用户名。
        - write_password：有写权限的用户密码（请配置明文, 最终在部署目录中会转换为密文)。
        - path：相对 sftp 根目录的文件路径，仅限/开头，且路径所指向的文件夹必须存在。
    - server: 仓库内容的下载地址，当[listen](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#zh-cn_topic_0000001745376470_listen)的host为0.0.0.0且本机存在多个网络接口时，**必须配置**。
        - server的格式如下：<[listen](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#zh-cn_topic_0000001745376470_listen)的proto>://<host>:<[listen](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#zh-cn_topic_0000001745376470_listen)的port>
        - 当配置项[listen](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#zh-cn_topic_0000001745376470_listen)的host不为0.0.0.0时，则server**默认**取listen的完整格式，例如listen为127.0.0.1:8088，故server默认值为 http://127.0.0.1:8088；
        - 当配置项[listen](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#zh-cn_topic_0000001745376470_listen)的host为0.0.0.0时，如果本机仅存在一个网络接口，则server中的host默认为本机网络接口的ipv4地址；如果本机存在多个网络接口，则server中的host默认为本机获取到的第一个网络接口的ipv4地址，建议手动修改host为指定的本机ip/域名，例如listen为0.0.0.0:8088，故server需配置为http://<本机ip/域名>:8088；
        - 如果需要通过反向代理来访问ohpm-repo服务，则该字段须配置为反向代理服务器的域名地址，且需要配置[use_reverse_proxy](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#section1074004784011)值为true。

参考配置如下：

1. store:                               
2.   type: sftp                         
3.   config:
4.     location:
5.       - 
6.         name: test_one_sftp          
7.         host: "localhost"           
8.         port: 22                     
9.         read_username: "read"   
10.         read_password: "password" 
11.         write_username: "write"   
12.         write_password: "password" 
13.         path: /source22
14.       -
15.         name: test_two_sftp
16.         host: "localhost"
17.         port: 24
18.         read_username: "read"
19.         read_password: "password"
20.         write_username: "write"
21.         write_password: "password"
22.         path: /source24
23.     #server: http://localhost:8088

**custom存储**

使用自定义插件存储，具体配置为：

- type: 插件名称，为custom。custom是自定义存储插件类型，自定义存储插件[开发流程见官方文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-storageplugin)。
- config: 插件配置，具体为：
    - export_name：待书写插件export的类名。
    - plugin_path：插件的绝对路径或者相对于ohpm-repo软件包的路径，建议将插件放在软件包的plugins目录下。
    - custom_field：自定义字段，通过引入ohpm-repo解压包中libs/common/getStorageConfigInfo.js的getStorageConfigInfo方法获取自定义字段的值。
    - server: 本地仓库下载地址：
        - 当配置项[listen](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#zh-cn_topic_0000001745376470_listen)的host不为0.0.0.0时，则**默认**取listen的完整格式，例如listen为127.0.0.1:8088，故server默认值为http://127.0.0.1:8088；
        - 如果配置项[listen](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#zh-cn_topic_0000001745376470_listen)的host为0.0.0.0，则server中的host默认为localhost，如http://localhost:8088。建议手动修改host为本机的ip/域名，例如listen为 0.0.0.0:8088，故server需配置为http://<本机ip/域名>:8088；
        - 如果需要通过反向代理来访问ohpm-repo服务，则该字段须配置为反向代理服务器的域名地址。多实例部署ohpm-repo时必须配置反向代理服务器，且需要配置[use_reverse_proxy](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#section1074004784011)值为true。

参考配置如下：

1. store:
2.   type: custom                                            
3.   config:
4.     export_name: "MyStorage"                              
5.     plugin_path: "plugins/storagePlugin/MyStorage.js"        
6.     custom_field: "test"                                  
7.     #server: http://localhost:8088

### use_reverse_proxy

- use_reverse_proxy: 是否使用反向代理选项。可选项：true/false， 默认：false。如果使用反向代理，必须配置为true，客户端IP地址将从请求头中的x-forwarded-for字段获取。

1. use_reverse_proxy: false

注意

当use_reverse_proxy配置为true时，必须在反向代理配置时刷新x-forwarded-for值（如果存在多级代理，只需要在最外层代理配置刷新），如果不刷新将存在x-forwarded-for数据被篡改风险，反向代理配置刷新x-forwarded-for命令如下：

1. proxy_set_header x-forwarded-for $remote_addr

### uplink

- uplink_cache_path：远程包缓存路径，默认路径为./uplink，支持相对和绝对路径配置，当配置为相对路径时，则以[deploy_root](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#zh-cn_topic_0000001745376470_%E5%85%B3%E4%BA%8E-deploy_root)为基准目录。
- uplink_cache_time：远程包metadata缓存时间，单位为小时，默认168小时，取值范围为(0, 8760]。

参考配置如下：

1. uplink_cache_path: ./uplink
2. uplink_cache_time: 168

### logs

- logs_path: 日志存储，默认路径为./logs，支持相对路径和绝对路径配置，当配置为相对路径时，以[deploy_root](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#zh-cn_topic_0000001745376470_%E5%85%B3%E4%BA%8E-deploy_root)为基准目录。

参考配置如下：

1. logs_path: ./logs 

### loglevel

loglevel自定义配置，具体配置为：

- loglevel_run：run日志文件的存储级别，默认级别为info，输出的日志信息级别高于设定的日志级别才会存储到run日志文件中。
- loglevel_operate：operate日志文件的存储级别，默认级别为info，输出的日志信息级别高于设定的日志级别才会存储到operate日志文件中。
- loglevel_access：access日志文件的存储级别，默认级别为info，输出的日志信息级别高于设定的日志级别才会存储到access日志文件中。

说明

- 日志级别由低到高分别是all、trace、debug、info、warn、error、fatal、mark 和 off。
- run、operate和access，日志级别不配置或者配置错误，默认为info。

参考配置如下：

1. loglevel_run: info
2. loglevel_operate: info
3. loglevel_access: info

### auth_plugin

ohpm-repo从2.3.0版本开始支持自定义认证插件（需配套使用1.8.0及以上版本ohpm命令行工具），允许您开发定制化的认证插件来对接您自己的用户信息系统。自定义认证插件开发流程见[认证插件说明文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-custom-auth-plugin)。

参数说明：

- name: 插件名称，自定义插件文件CustomAuth.js中定义的实现类名称，如果实现类为CustomAuth，故此处值为：CustomAuth 。
- path: 编译后插件文件CustomAuth.js的存储位置。支持绝对路径和相对路径，相对路径的基准为ohpm-repo解压根目录。

参考配置如下（默认不开启）：

1. #auth_plugin:
2. #  name: CustomAuth              
3. #  path: plugins/CustomAuth.js   

### field_check_plugin

ohpm-repo从5.1.3版本开始支持自定义元数据规则校验，可以对oh-package.json5中部分字段开发定制化的校验规则。自定义元数据规则校验插件开发流程见[自定义元数据规则校验插件说明文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-custom-metadata-rule-validation-config)。

参数说明：

- config_file_path：字段校验配置文件路径，支持绝对路径和相对路径，相对路径的基准为ohpm-repo解压根目录，建议将文件存放在软件包的plugins/fieldCheckPlugin目录下，默认值为plugins/fieldCheckPlugin/CustomExtensionValidationConfig.json。
- check_func_dir：字段校验函数文件所在目录路径，支持绝对路径和相对路径，相对路径的基准为ohpm-repo解压根目录，建议将目录设置为plugins/fieldCheckPlugin文件夹，默认值为plugins/fieldCheckPlugin。

参考配置如下（默认不开启）：

1. #field_check_plugin:
2. #  config_file_path:  plugins/fieldCheckPlugin/CustomExtensionValidationConfig.json   
3. #  check_func_dir: plugins/fieldCheckPlugin                                           

### content_check_plugin

ohpm-repo从5.2.0版本开始支持三方库字节码文件的OHMUrl版本一致性校验，可以对字节码har文件中module.abc文件中的OHMUrl的版本号与har文件中实际的版本号进行一致性校验，阻止不一致包的上传，以防止运行时崩溃。

注意

一致性检查将用到ark_disasm工具及系统自带的tar解压工具。ark_disasm工具位于命令行工具中，用于反编译module.abc文件，请先下载[命令行工具](https://developer.huawei.com/consumer/cn/download/command-line-tools-for-hmos)，并将ark_disasm工具所在路径（默认路径为command-line-tools/sdk/default/openharmony/toolchains）及tar解压工具的所在路径添加到系统环境变量中（对于Linux/macOS系统，请将bsdtar解压工具所在路径添加到系统环境变量中）。如在上传三方库过程中发现ark_disasm导致报错，请联系管理员，确保您使用的DevEco Studio与ark_disasm工具配套。

参数说明：

- name：固定为"OHMUrlCheck"

参考配置如下（默认不开启）：

1. #content_check_plugin:
2. #  name: 'OHMUrlCheck'     

### compability_log_level

- compability_log_level: compatibleSdkVersion等兼容性字段检测日志等级，可选值：close、info、warn、error，默认为warn，参考配置如下：

1. compability_log_level: warn

### allow_remove_depended_packages

- allow_remove_depended_packages: 是否允许下架被其他组件依赖的包，可选项：true，false，默认为false，参考配置如下：

1. allow_remove_depended_packages: false

## 关于 deploy_root

deploy_root为ohpm-repo的部署目录，通过配置文件中字段<[deploy_root](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#zh-cn_topic_0000001745376470_deploy_root)>可进行配置。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-quickstart "快速开始")
# 日志

更新时间: 2025-12-16 15:57

与任何web应用程序相同，ohpm-repo有一个内置的日志记录器，其定义了四种日志类型。

## 访问日志 - access.log

访问日志中主要包含操作时间、服务器ip、操作源、操作结果以及请求接口或者请求静态资源，其文件保存个数最多为180个。

## 操作日志 - operate.log

操作日志中主要包含操作时间、日志级别、操作人id(userId)、终端 ip(ip)、操作资源（resource）、操作方法名（event）以及操作结果（result），其文件保存个数最多为180个。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155730.30170832545881200844300880730911:50001231000000:2800:F24083DE962E220B06BC79612A3601F061DCCC148570DD048939F230A0631BD0.png "点击放大")

说明

**操作方法名(event)**： 当在ohpm-repo管理界面执行一系列操作时，会在operate.log文件生成一条条操作数据，操作方法名即表示当前操作涉及到的方法名字，例如login即表示登录操作，analyzePackage即表示上传包时对包的解析操作。

**表1** 常用操作方法说明
|序号|Event描述|说明|
|:--|:--|:--|
|1|generateAccessToken / deleteAccessToken|生成 / 删除AccessToken|
|2|login / logout|登入 / 登出|
|3|publish / unPublish/batchUnPublish|上架资源包/ 下架资源包/批量下架资源包|
|4|addGroup / deleteGroup|添加/删除组织|
|5|updateGroup|更新组织|
|6|addMember/deleteMember|添加 / 删除组织成员|
|7|addAdminMember/deleteAdminMember|添加/删除组织管理员|
|8|addPublicKey / delPublicKeyById|添加 / 删除发布公钥|
|9|addRepo/updateRepo/deleteRepo|新增仓库/更新仓库/删除仓库|
|10|analyzePackage|解析上传的包文件|
|11|uploadPackage|上传包文件|
|12|getPackageSizeLimit|获取包的大小限制|
|13|addUplink / deleteUplink|添加 / 删除uplink|
|14|updateUplink|更新uplink|
|15|updateUplinkProxy|更新Uplink代理|
|16|addUser / delUserByUserId|添加/删除用户|
|17|changePassWord|改变用户账户密码|
|18|resetPassWord|重置用户账户密码|
|19|changeRole|修改用户角色(管理员和非管理员)|
|20|register|注册账户|
|21|resetKey|重置系统密钥|
|22|addPackagePermissionOwner/deletePackagePermissionOwner/transferPackagePermissionOwner|新增/删除/转移包所有者|
|23|addPackagePermissionMaintainer/deletePackagePermissionMaintainer|新增/删除包维护者|
|24|addPackagePermissionVisitor/deletePackagePermissionVisitor|新增/删除包白名单用户|
|25|editPackageReadPolicy|编辑包可见性|

## 运行日志 - run.log

运行日志中主要包含操作时间、日志级别以及日志信息，其文件保存个数最多为30个。运行日志定义了日志级别：all，trace，debug，info，warn，error，fatal，mark和off。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155730.94829438043169180468312748481339:50001231000000:2800:FBD594AB2E8E32A5542F89B17ED6350FF525906696F4656695A47E57FC58D0A9.png "点击放大")

## 运行错误日志 - repoError.log

当ohpm-repo在运行过程中，所有run.log中生成的error日志都会打印到repoError.log中，是error日志的集合，日志打印级别与run.log日志保持一致。

## 下载错误日志

当从仓库中下载某个包失败时，仓库会生成一条错误日志记录在数据库中的downloadfailure 表中，当为ohpm-repo配置了sftp存储服务时，从任意一个sftp服务中下载失败时，都会生成一条错误日志并保存。每条日志都有handled标识，handled为0时表示已处理，handled为1时表示未处理。

## 日志存储路径

日志存储的默认路径为./logs，相对路径基准为ohpm-repo部署根目录[deploy_root](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#zh-cn_topic_0000001745376470_%E5%85%B3%E4%BA%8E-deploy_root)。

## 日志打印级别

在配置文件中可以设置访问、操作、运行日志的打印级别，日志将会只打印不低于设置级别的日志，日志级别由低到高为：all，trace，debug，info，warn，error，fatal，mark和off。

1. loglevel_run: info
2. loglevel_operate: info
3. loglevel_access: info

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration "配置文件")
# 单点部署

更新时间: 2025-12-16 15:57

说明

ohpm-repo私仓不允许在Linux或macOS系统中使用root用户启动，请使用普通用户安装运行。

## 安装ohpm-repo工具

1. ohpm-repo依赖于Node运行，支持Node.js 18.x及以上版本，请提前安装Nodejs，并完成环境变量的配置。Node.js安装请参考[Node.js官方网站](https://nodejs.org/download/release/latest/)。
    
2. 下载ohpm-repo工具包，[点击链接获取](https://developer.huawei.com/consumer/cn/download/ohpm-repo)**。**
    
3. 解压ohpm-repo私仓工具包。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155733.54164763087581820782279345443324:50001231000000:2800:7B50FA61311BAA26CAFA40FEB5B26C30549090E688DB68659B8D61CAC21D75D9.png)
    

4. 请将ohpm-repo工具包解压目录中bin目录的路径配置到[系统环境变量](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-faq#section24117279211)path中，执行如下查询命令:
    
    1. ohpm-repo -v
    
    终端输出版本号（如：2.0.0），则表示安装包解压无问题。如有报错，请参考[FAQ](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-faq#section82-%E6%89%A7%E8%A1%8C%E5%91%BD%E4%BB%A4-ohpm-repo-command%E6%8A%A5%E9%94%99-ohpm-repo-%E4%B8%8D%E5%AD%98%E5%9C%A8%E6%88%96%E8%80%85-command-%E5%91%BD%E4%BB%A4%E4%B8%8D%E5%AD%98%E5%9C%A8)解决。
    
    注意
    
    针对Linux和Mac系统，建议使用bash作为命令行界面。
    
5. 进入ohpm-repo解压目录的conf目录中，修改配置文件config.yaml：
    - 检查[listen](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#zh-cn_topic_0000001745376470_listen)配置，默认配置为localhost:8088 ，表示仅支持监听本机地址；如果希望其他机器通过ip/域名访问，则建议修改listen配置为ohpm-repo部署机器的ip：
        
        1. listen: <部署ohpm-repo机器的ip>:8088
        
    - 检查[deploy_root](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#zh-cn_topic_0000001745376470_deploy_root)配置：如果选择不配置，会存储在默认地址中。禁止该路径配置为ohpm-repo解压根目录。
    - 数据存储db模块使用filedb：
        
        1. db:
        2.   type: filedb
        3.   config:
        4.     path: ./db
        
    - 文件存储store模块使用fs：
        
        1. store:
        2.   type: fs
        3.   config:
        4.     path: ./storage
        5.     #server: http://localhost:8088
        
    - 检查是否配置了[store.config.server](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#zh-cn_topic_0000001745376470_store)，用于指定ohpm-repo仓库内容的下载地址，不配置取默认值，具体请参考[server: 仓库内容的下载地址](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#zh-cn_topic_0000001745376470_li922300957171146)。如果[listen](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#zh-cn_topic_0000001745376470_listen)的host为0.0.0.0，且本机存在多个网络接口，那么该值必须配置，建议手动修改server的host为本机指定的ip/域名，例如listen为0.0.0.0:8088，故server需配置为http://<指定部署机器的ip/域名>:8088。
        
        说明
        
        - 如果为ohpm-repo服务配置了反向代理服务器，则[store.config.server](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#zh-cn_topic_0000001745376470_store)必须填写为反向代理服务器的ip/域名地址，且需要配置[use_reverse_proxy](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#section1074004784011)值为true。
        - config.yaml中各项配置的详细描述请见：[配置文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration)。
        
6. 进入ohpm-repo解压目录的bin目录下，执行安装命令:
    
    1. ohpm-repo install 
    
    说明
    
    不配置参数--config，默认使用ohpm-repo根目录中conf目录内自带的配置文件config.yaml。
    
    启动成功日志信息如下：
    
    2. PS D:\> ohpm-repo install
    3. [2025-08-26T14:29:15.153] [WARN] default - "listen" protocol is set to 'http' in "config.yaml" file, which is insecure, advise to use the more secure 'https' protocol instead.
    4. [2025-08-26T14:29:15.178] [INFO] default - initialize encryption component successfully.
    5. [2025-08-26T14:29:15.179] [INFO] default - initialize "file database" successfully.
    6. [2025-08-26T14:29:15.184] [INFO] default - initialize "file storage" successfully.
    7. 。。。
    8. [2025-08-26T14:29:15.194] [INFO] console - install successfully.
    9. [2025-08-26T14:29:15.195] [INFO] default - "deploy_root" environment variables: "OHPM_REPO_DEPLOY_ROOT = C:\Users\xxx\AppData\Roaming\Huawei\ohpm-repo".
    
7. 安装成功后，必须根据给出的提示信息及时刷新环境变量，针对Windows系统和Linux/Mac系统，有不同处理方式：
    
    说明
    
    - Windows系统： 关闭当前窗口，重新开启一个窗口。
    - Linux系统或Mac系统： 在命令行中执行刷新命令：当shell为bash时执行_**source ~/.bashrc**_ 或者 . **_~/.bashrc_** ；当shell为zsh时，执行_source ~/.zshrc_ 或者 . _~/.zshrc_ 。
    

## 启动ohpm-repo

执行start命令启动ohpm-repo。

1. ohpm-repo start 

启动成功日志信息如下：

1. PS D:\> ohpm-repo start
2. [2025-08-26T14:31:22.209] [WARN] default - "listen" protocol is set to 'http' in "config.yaml" file, which is insecure, advise to use the more secure 'https' protocol instead.
3. [2025-08-26T14:31:22.211] [INFO] default - config file path: "C:\Users\xxx\AppData\Roaming\Huawei\ohpm-repo\conf\config.yaml".
4. [2025-08-26T14:31:22.216] [INFO] default - initialize "file database" successfully.
5. [2025-08-26T14:31:22.217] [INFO] default - initialize "file storage" successfully.
6. [2025-08-26T14:31:22.237] [INFO] console - http address - localhost:8088 - ohpm-repo/5.1.5.

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-deploy-guide "部署指导")
# 多实例部署

更新时间: 2025-12-16 15:57

说明

- ohpm-repo私仓不允许在Linux或macOS系统中使用root用户启动，请使用普通用户安装运行。
- 只有db存储为mysql且store存储为sftp或者custom时，才支持多实例方式部署。本章节多实例部署以db存储为mysql，store存储为sftp为例。

## 环境准备

1. 准备mysql数据库服务；
2. 准备至少一个sftp存储服务，ohpm-repo最大支持连接3个sftp服务；
3. 安装Node.js18.x及以上版本。

说明

- 确保sftp服务端口能够被外部机器访问。
- sftp服务的读写用户应该指定相同的存储根目录。

## 安装ohpm-repo工具

1. 解压ohpm-repo工具包
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155735.54463571741923025075604999129090:50001231000000:2800:2EA6DD10EC0831DB580711BCD852879A41B7F5AB772702DD21B0F0D2CF9D0B44.png)
    
2. 请将ohpm-repo工具包解压目录中bin目录的路径配置到[系统环境变量](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-faq#section24117279211)path中，执行如下查询命令:
    
    1. ohpm-repo -v
    
    终端输出版本号（如：2.0.0），则表示安装包解压无问题。如有报错，请参考[FAQ](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-faq#section82-%E6%89%A7%E8%A1%8C%E5%91%BD%E4%BB%A4-ohpm-repo-command%E6%8A%A5%E9%94%99-ohpm-repo-%E4%B8%8D%E5%AD%98%E5%9C%A8%E6%88%96%E8%80%85-command-%E5%91%BD%E4%BB%A4%E4%B8%8D%E5%AD%98%E5%9C%A8)解决。
    
    注意
    
    针对Linux和Mac系统，建议使用bash作为命令行界面。
    
3. 进入ohpm-repo解压目录的conf目录中，修改配置文件config.yaml：
    - 检查[listen](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#zh-cn_topic_0000001745376470_listen)配置，默认配置为localhost:8088 ，表示仅支持监听本机地址；如果希望其他机器通过ip/域名访问，则建议修改listen配置为ohpm-repo部署机器的ip地址：
        
        1. listen: <部署ohpm-repo机器的ip>:8088
        
    - 检查[deploy_root](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#zh-cn_topic_0000001745376470_deploy_root)配置：如果选择不配置，会存储在默认地址中。禁止配置该路径配置为ohpm-repo解压根目录。
    - 数据存储db模块使用mysql：
        
        1. db:                         
        2.   type: mysql
        3.   config:
        4.     host: "localhost"
        5.     port: 3306
        6.     username: "tctAdmin"
        7.     password: "password"
        8.     database: "repo"
        
    - 文件存储store模块使用sftp，sftp配置最多只能设置3个：
        
        1. store:                               
        2.   type: sftp                         
        3.   config:
        4.     location:
        5.       -      
        6.         name: test_one_sftp          
        7.         host: "localhost"           
        8.         port: 22                     
        9.         read_username: "read"   
        10.         read_password: "password" 
        11.         write_username: "write"   
        12.         write_password: "password" 
        13.         path: /source22 
        14.       -  
        15.         name: test_two_sftp
        16.         host: "localhost"
        17.         port: 24
        18.         read_username: "read"
        19.         read_password: "password"
        20.         write_username: "write"
        21.         write_password: "password"
        22.         path: /source24
        23.     #server: http://localhost:8088
        
        注意
        
        1、ohpm-repo文件的存储路径为： <sftp服务器配置的存储根目录> +<store配置的[path](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#zh-cn_topic_0000001745376470_li1275312401171146)路径>，其中path只支持相对路径，必须以/开头。例如sftp服务器存储根目录为/user/sftp/data，store中[path](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#zh-cn_topic_0000001745376470_li1275312401171146)配置的路径为/source，故最终ohpm-repo文件存储路径为/user/sftp/data/source。
        
        2、多实例部署ohpm-repo时，必须配置反向代理服务器，转发客户端请求到部署的多个ohpm-repo实例服务器中，故[store.config.server](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#zh-cn_topic_0000001745376470_store)必须手动配置为反向代理服务器的域名/ip地址，且需要配置[use_reverse_proxy](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-configuration#section1074004784011)值为true。
        

4. 进入ohpm-repo解压目录的bin目录下，执行安装命令:
    
    1. ohpm-repo install 
    
    说明
    
    不配置参数--config，则默认使用ohpm-repo解压目录中conf目录内自带的配置文件config.yaml。
    
    安装成功日志信息如下：
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155735.67449947767883164404962491991226:50001231000000:2800:735E9574828A02BC49FDF21EA6F276E00B5E988B0949A969FDF68872FD3DBDE1.png "点击放大")
    
5. 安装成功后，必须根据给出的提示信息刷新环境变量，针对Windows系统和Linux/Mac系统，有不同处理方式：
    
    说明
    
    - Windows系统： 关闭当前窗口，重新开启一个窗口。
    - Linux系统或Mac系统： 在命令行中执行刷新命令：当shell为bash时执行_source ~/.bashrc_ 或者 . _~/.bashrc_ ；当shell为zsh时，执行_source ~/.zshrc_ 或者 . _~/.zshrc_ 。
    

## 部署首个节点

进入ohpm-repo解压目录的bin目录中，命令行启动ohpm-repo。

1. ohpm-repo start 

启动成功日志信息如下：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155735.63186911601241611065768982095122:50001231000000:2800:575DF1CE831A2A7EDDE766519CCC43507676AE76B1892DCC06D92DA88BF5FC19.png "点击放大")

## 打包和部署

为帮助更方便地完成多实例部署，已提供打包和部署命令。

### 打包

在完成了多实例配置并首次启动过ohpm-repo服务实例的机器上，执行ohpm-repo pack <deploy_root>。

1. ohpm-repo pack D:\ohpm-repo

说明

该命令用来打包备份ohpm-repo的<deploy_root>/conf，<deploy_root>/meta目录，并在命令行工作目录下生成压缩包。

打包成功日志信息如下：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155735.92188108768855022625393754288554:50001231000000:2800:45E7E34DE1731F45553D1679FEECF8C89255B56635C98F75FAF27A60EF61239F.png "点击放大")

### 部署

将pack命令的产物拷贝到其他机器中。在解压ohpm-repo压缩包后，使用ohpm-repo deploy <file_path>命令部署新的实例。

1. ohpm-repo deploy D:\ohpm-repo\bin\pack_1695805599689.zip --deploy_root D:\new-ohpm-repo\ohpm-repo-deploy

说明

- <file_path>： 参数指定备份压缩包地址。
- --deploy_root： 指定部署根目录，用于存储ohpm-repo启动时生成的文件，默认使用 <现有用户home目录>/ohpm-repo。

部署成功日志信息如下：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155735.91767962816868892173601205338260:50001231000000:2800:835CD690D0174D80417B05B10833CC33C69826E239E083A190003C460FCE9689.png "点击放大")

部署成功后可执行ohpm-repo start启动ohpm-repo。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155735.58858309358905961247866221576817:50001231000000:2800:049301635BE6EDFF30CDAA14CCA33D8923EA13CA84FFF797D30E9E801DF8D79A.png "点击放大")

## 配置自动重启（可选）

为ohpm-repo实例配置系统重启时自动重启的功能。

说明

在进行该配置前需要将ohpm-repo工具bin目录配置到[系统环境变量](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-faq#section24117279211)path中。

### Linux

1. 在ohpm-repo工具的bin目录下创建自动运行脚本run-repo.sh：
    
    1. touch run-repo.sh
    
2. 写入下面内容，保存并关闭文件：
    
    说明
    
    当mysql或sftp服务与ohpm-repo部署在同一服务器上时，请将mysql和sftp的启动命令放在ohpm-repo start命令之前。
    
    1. #!/bin/bash
    2. ohpm-repo start
    
3. 将该脚本设置为可执行文件：
    
    1. chmod +x run-repo.sh
    
4. 使用linux的定时任务工具crontab重启自动执行脚本。编辑当前用户的crontab配置：
    
    1. crontab -e
    
5. 当前用户的crontab配置写入下面内容，保存并关闭文件：
    
    1. @reboot /bin/sh run-repo.sh >/dev/null 2>&1
    

其中run-repo.sh表示要执行的脚本路径；>/dev/null 2>&1表示将输出重定向到空设备，即不输出任何信息。

现在，每次系统启动时，都会自动执行run-repo.sh脚本中的命令。

### Windows

1. 新建run-repo.bat文件，写入下面内容：
    
    说明
    
    当mysql或sftp服务与ohpm-repo部署在同一服务器上时，请将mysql和sftp的启动命令放在ohpm-repo start命令之前。
    
    1. @echo off
    2. call ohpm-repo start
    3. exit
    
2. 按下win+R，输入shell:startup，回车：弹出启动文件框；将run-repo.bat文件剪切到启动文件夹下即可。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155736.07487797604045365124258516091099:50001231000000:2800:3B10926558813F2911FD8E27384CDC608E96173DEF23901F940682344C5222B7.png "点击放大")
    

现在，每次系统启动时，都会自动执行run-repo.bat脚本中的命令。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-deploy-single-instance "单点部署")
# 在模块中添加Ability

更新时间: 2025-12-16 15:57

Ability是应用/元服务所具备的能力的抽象，应用的一个Module可以包含一个或多个Ability，元服务仅包含一个Ability。应用/元服务先后提供了两种应用模型：

- FA（Feature Ability）模型： API 7开始支持的模型，已经不再主推。
- Stage模型：HarmonyOS 3.1 Developer Preview版本开始新增的模型，是目前主推且会长期演进的模型。在该模型中，由于提供了AbilityStage、WindowStage等类作为应用组件和Windows窗口的“舞台”，因此称这种应用模型为Stage模型。
    
    Stage模型包含两种Ability组件类型：
    
    - UIAbility组件：包含UI界面，提供展示UI的能力，主要用于和用户交互。详细介绍请参见[UIAbility组件概述](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/uiability-overview)。
    - ExtensionAbility组件：提供特定场景的扩展能力，满足更多的使用场景。详细介绍请参见[ExtensionAbility概述](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/extensionability-overview)。元服务暂不支持使用ExtensionAbility组件。

## Stage模型添加Ability

### 在模块中添加UIAbility

1. 选中对应的模块，单击鼠标右键，选择**New > Ability**。
2. 设置Ability名称，选择是否在设备主屏幕上显示该功能的启动图标，单击Finish完成Ability创建。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155724.93846847532218884989227254091387:50001231000000:2800:D2245EF416B2006B97055D3EAC95E9E2A6EB27D099D566BD1166968A62E0405C.png)
    

### 在模块中添加Extension Ability

1. 在工程中选中对应的模块，单击鼠标右键，选择**New > Extension Ability**，选择不同的场景类型 。当前仅Application工程支持创建Extension Ability。
    
    - 若创建的模块类型为entry或feature，支持创建以下五种Extension Ability：
        - **EmbeddedUIExtensionAbility**：用于提供[跨进程界面嵌入](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/embeddeduiextensionability)的能力。
        - **Backup****Ability**：用于提供[备份及恢复应用数据](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-file-backup-overview)的能力。
        - **WorkScheduler**：用于提供[延迟任务](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/work-scheduler)的相关能力。
        - **RemoteNotificationAbility**：用于提供获取场景化消息数据和生命周期销毁的回调的通知能力。
        - **Driver**：用于提供[驱动相关扩展框架](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/driverextensionability)。仅在当前工程的设备类型只含有2in1设备时，支持创建该类型。
    - 若创建的模块类型为HAR或HSP，支持创建以下两种Extension Ability：
        - **EmbeddedUIExtensionAbility**：用于提供[跨进程界面嵌入](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/embeddeduiextensionability)的能力。
        - **WorkScheduler**：用于提供[延迟任务](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/work-scheduler)的相关能力。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155724.49842738246989101511143584420369:50001231000000:2800:E614B56A7BD7B894330905903C851A073348200A48CB71E8D637CF1B5130AA79.png)
    
2. 设置Ability名称，单击Finish完成Extension Ability创建。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155724.41738365717439615718963176324754:50001231000000:2800:1235D21ACEF999157D9FD28C0776DE5060E529E94F70450E2094943C75CFA194.png)
    

## FA模型添加Ability

ArkTS工程与JS工程在FA模型中添加Ability的操作方式一致，本节内容以ArkTS工程为例介绍在模块中添加Ability。

### 创建Particle Ability

1. 选中对应的模块，单击鼠标右键，选择**New > Ability** ，然后选择对应的Data Ability/Service Ability模板。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155724.67620966478069682345558224380351:50001231000000:2800:F718783307507C6E23625E05FC25AE766A81ECF11E19BDF7C297F48F417BD98C.png)
    
2. 根据选择的Ability模板，设置Ability的基本信息。
    
    - **Ability name**：Ability类名称，由大小写字母、数字和下划线组成。
    - **Language**：该Ability使用的开发语言。
    
3. 单击**Finish**完成Ability的创建，可以在工程目录对应的模块中查看和编辑Ability。

### 创建Feature Ability

1. 选中对应的模块，单击鼠标右键，选择**New > Ability** ，然后选择对应的Page Ability模板。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155724.18840219801761584670492251659824:50001231000000:2800:03C321E2B4B38364B98F7E6DE71286744BD1BCBF155519507C3A2C2F1E540C2D.png)
    
2. 根据选择的Ability模板，设置Ability的基本信息。
    
    - **Ability name**：Ability类名称，由大小写字母、数字和下划线组成。
    - **Launcher ability**：表示该Ability在终端桌面上是否有启动图标，一个HAP可以有多个启动图标，来启动不同的FA。
    - **Language**：该Ability使用的开发语言。
    
3. 单击**Finish**完成Ability的创建，可以在工程目录对应的模块中查看和编辑Ability。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-rule-verification-template-file "模板文件")
# 创建服务卡片

更新时间: 2025-12-16 15:57

## 概述

[服务卡片（简称“卡片”）](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/formkit-overview)可将元服务/应用的重要信息以卡片的形式展示在桌面，用户可通过快捷手势使用卡片，通过轻量交互行为实现服务直达、减少层级跳转的目的。

卡片类型分静态卡片和动态卡片两种。静态卡片内存占用较小，有助实现整机内存优化，可实现静态信息展示、刷新和点击跳转；动态卡片支持自定义交互、动效、滑动等功能，功能丰富但内存占用较大。

从编译产物角度，卡片包产物分为共包和独立包两种类型，详情请参考[创建ArkTS卡片](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-ui-widget-creation)。

|创建方式|卡片类型|
|:--|:--|
|共包|静态卡片（Static Widget）|
|动态卡片（Dynamic Widget）|
|独立包|独立静态卡片（Static Widget(Standalone)）|
|独立动态卡片（Dynamic Widget(Standalone)）|

创建卡片后可选择不同卡片模板以满足业务需求，具体卡片模板和详细描述如下。

|模板名称|支持的设备|支持的开发语言|模板描述|
|:--|:--|:--|:--|
|Hello World|Phone、Tablet、2in1、Wearable、Car、TV|ArkTS、JS|HelloWorld卡片，用于高效直观地构建UI。当前Hello World卡片模板支持使用6*4尺寸。|
|Image With Information（图文卡片模板）|Phone、Tablet、2in1、Wearable、Car|ArkTS、JS|图文卡片模板主要在于展现图片和一定数量文本的搭配，在这种布局下，图片和文本属于同等重要的信息。在不同尺寸下，图片大小和文本数量会发生一定变化，用于凸显关键信息。|
|Immersive Information（沉浸图文卡片模板）|Phone、Tablet、2in1、Wearable、Car|ArkTS、JS|沉浸式卡片的装饰性较强，能够较好的提升卡片品质感并起到装饰桌面的作用，合理的去布局信息与背景图片之间的空间比例，可以提升用户的个性化使用体验。|
|List|Phone、Tablet、2in1、Car|ArkTS|提供基本的列表功能。当前仅动态卡片支持在API 11及以上工程创建List卡片模板。|
|Control Button|Phone、Tablet、2in1、Car|ArkTS|操控类型的卡片，展示文本信息与按钮操作，点击按钮响应事件。当前仅静态卡片支持API 11及以上工程创建Control Button卡片模板。|
|Control Search|Phone、Tablet、2in1、Car|ArkTS|操控类型的卡片，适用于搜索场景。当前仅静态卡片支持API 11及以上工程创建Control Search卡片模板。|

## 使用约束

- 卡片不支持调试。
- 仅应用的Hello World、Image With Information、Immersive Information的动态卡片和独立动态卡片支持JS语言，元服务不支持JS语言。
- 从DevEco Studio 5.0.4 Release开始，支持在API 16及以上工程创建Wearable设备可用的卡片。
- 从DevEco Studio 6.0.0 Beta3开始，支持在API 20及以上工程创建Car设备可用的卡片。
- 从DevEco Studio 6.0.0 Beta3开始，支持Phone设备创建独立静态/动态卡片。
- DevEco Studio 5.1.1 Release（Build Version:5.1.1.850）版本、DevEco Studio 6.0.0 Release（Build Version:6.0.0.868）及以上版本，支持工程创建TV设备可用的卡片。
- 一个工程模块内，仅支持创建共包类型卡片或独立包类型卡片。
- 每个模块最多可以配置16张卡片。

## 创建服务卡片

[创建一个工程](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-create-new-project)后，可以通过如下方法进行创建卡片。

1. 创建卡片包括如下两种方式：
    
    - 选择模块（如entry模块）下的任意文件，单击菜单栏**File > New > Service Widget**，[按需选择卡片](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-service-widget#section6353219163116)。
    - 选择模块（如entry模块）下的任意文件，单击**右键 > New > Service Widget**，[按需选择卡片](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-service-widget#section6353219163116)。
    
    说明
    
    - API 11 Stage模型及以上，创建元服务工程或在元服务工程中创建模块时，不再默认创建卡片和EntryCard。
    
2. 在**Choose a Template for Your Service Widget**界面中，选择卡片模板，单击**Next**。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155725.92724805757218177950828966990057:50001231000000:2800:6AF6F9353D526CF0C1DC4F3D8C63F69F8A90C5DC5F5770DDF6E5F1245BBC6A0F.png)
    
3. 在**Configure Your Service Widget**界面中，配置卡片的基本信息，包括：
    
    - **Service widget name**：卡片的名称，在同一个应用/元服务中，卡片名称不能重复，且只能包含大小写字母、数字和下划线。
    - **Display name**：卡片预览面板上显示的卡片名称。仅API 11 及以上Stage工程支持配置该字段。
    - **Description**：卡片的描述信息。
    - **Language：**界面开发语言，可选择创建ArkTS/JS卡片。
    - **Support dimension**：选择卡片的规格。部分卡片支持同时设置多种规格。首次创建卡片时，将默认生成一个EntryCard目录，用于存放卡片快照。
    - **Default dimension**：在下拉框中可选择默认的卡片。
    - **Ability name：**选择一个挂靠卡片的Form Ability，或者创建一个新的Form Ability。
    - **Module name：**卡片所属的模块。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155725.19184888172375033502626385276631:50001231000000:2800:9C3B749409F2590824F4A2BB42141C1383614B7FBF7B829E86E7CDD768B06FAC.png)
    
4. 单击**Finish**完成卡片的创建。创建完成后，工具会自动创建出卡片的布局文件，并在form_config.json文件中写入服务卡片的属性字段，关于各字段的说明请参考[配置文件说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-ui-widget-configuration)。
5. 卡片创建完成后，请根据开发指导，完成卡片的开发，详情请参考[服务卡片开发指南](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-ui-widget)。

## 预览服务卡片

在开发卡片过程中，支持对卡片进行实时预览。卡片通过ArkTS文件进行布局设计，在开发过程中，可以对布局文件进行实时预览，只要在布局文件中保存了修改的源代码，在预览器中就可以实时查看布局效果。在Phone和Tablet卡片的预览效果中，每个尺寸的卡片提供3种场景的预览效果，分别为极窄（Minimum）、默认（Default）、极宽(Maximum)，开发者应确保三种尺寸的显示效果均正常，以便适应不同屏幕尺寸的设备。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155725.03196906111669397724568461998436:50001231000000:2800:CE944F0C380585DAC409BD2CF9880E2B5514CFF83CE8A045E38A79BD423E30B4.png)

关于预览器的使用详细说明请参考[界面预览](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-previewer-01)。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-add-new-ability "在模块中添加Ability")
# 添加Page

更新时间: 2025-12-16 15:57

在ArkTS语言的工程中，支持添加Page。Page是表示应用/元服务的一个页面。应用/元服务可以设计为多个功能页面，每个页面进行单独的文件管理，并通过路由API实现页面的调度管理，以实现应用内功能的解耦。ArkTS语言的工程添加Page后，会在pages文件夹下生成一个新的ets文件。

1. 在Stage工程中选中ets文件夹下的pages，单击鼠标右键，选择**New > Page**，当前提供如下Page类型：
    
    - Empty Page：创建一个普通页面，展示基础的Hello World功能；
    - Map Page：创建一个地图页面，展示地图视图功能，当前仅支持在Phone设备中使用；
    - Payment Page：创建一个支付页面，可以实现点击按钮调起支付弹窗，当前仅支持在Phone设备中使用；
    - Iap Page：IAP Kit场景化模板，支持快速创建应用内支付购买虚拟数字商品相关代码。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155725.49382668994428618117082322716229:50001231000000:2800:17E2AB53FD21E59611E17336F718B7874448FBD72054F514D0530FD0BA9ACEEB.png)
    
    说明
    
    API 10工程中仅支持创建Page，展示基础的Hello World功能；如需使用场景化Page模板，请将工程切换为API 11及以上后进行开发。
    
2. 输入Page name（由大小写字母、数字和下划线组成），单击**Finish**完成添加。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155725.46442292332562793895285737461490:50001231000000:2800:45DFEF277CB36FAFCD2D01DE2B8D49537C6C87134DED0326C68E9A020C03BC4E.png "点击放大")
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-service-widget "创建服务卡片")
# 业务介绍

更新时间: 2025-12-16 15:57

## 什么是端云一体化开发

为丰富HarmonyOS对云端开发的支持、实现端云联动，DevEco Studio以[Cloud Foundation Kit（云开发服务）](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-introduction)为底座、在传统的“端开发”基础上新增“云开发”能力：开发者选择云开发工程模板，可创建一个同时包含端侧工程与云侧工程的端云一体化工程。之后，开发者在云侧工程对云函数或者云数据库等服务进行开发、调试和部署，而后在端侧工程通过Cloud Foundation Kit调用部署的云端服务。

DevEco Studio中提供的端云一体化开发体验，支持开发者基于统一的技术栈进行端、云代码协同开发，前端开发人员轻松转换为全栈工程师，极大提高了构建HarmonyOS应用和元服务的效率、降低开发成本。

## 什么是云开发工程模板

云开发工程模板是为端云一体化开发工程构建的场景化模板，提供了常见场景的代码实现。使用云开发工程模板，您可根据工程向导轻松创建端云一体化开发工程，工程将自动加载模板内预置的代码和资源文件。

DevEco Studio目前预置了通用云开发模板，该模板当前使用[Cloud Foundation Kit（云开发服务）](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-introduction)搭建了基础的演示项目，不含业务属性。您可参考模板学习如何进行基础的端云工程开发，后续开发时可删除预置的页面代码。

[点击此处](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-emptyability)了解通用云开发模板的更多信息。

## 端云一体化开发特性

端云一体化开发特性主要包含了如下功能。

|主要功能|说明|
|:--|:--|
|端云一体化开发|您不仅可以在DevEco Studio中开发和调试应用端侧的业务代码，还可以开发和调试应用云侧的服务代码、并在开发完成后将云侧工程一键部署至AGC云端。|
|Cloud Foundation Kit|云侧工程接入Cloud Foundation Kit，按需为应用提供云函数、云数据库、云存储等云端服务，借助Cloud Foundation Kit开箱即用、一键部署、自动弹性伸缩、免运维等特点助力开发者降本增效。|

## 端云一体化开发的优势

相比于传统开发模式，端云一体化开发模式具备成本低、效率高、门槛低等优势，具体区别见下表。

|区别点|传统开发模式|端云一体化开发模式|
|:--|:--|:--|
|开发工具|端侧与云侧各需一套开发工具，云侧需自建服务器，工具成本高。|DevEco Studio一套开发工具即可支撑端侧与云侧同时开发，无需搭建服务器，工具成本低。|
|开发人员|- 端侧与云侧要求不同的开发语言，技能要求高。<br>- 需多人投入，且开发人员之间需持续、准确沟通，人力与沟通成本高、效率低。|- 依托Cloud Foundation Kit开放的接口，端侧开发人员也能轻松开发云侧代码，大大降低开发门槛。<br>- 开发人员数量少，降低人力成本，提高沟通效率。|
|运维|需自行构建运营与运维能力，成本高、负担重。|直接接入Cloud Foundation Kit，具有开箱即用、一键部署、自动弹性伸缩、免运维等特点，开发者可聚焦业务逻辑本身，实现降本增效。|

## 工作原理

DevEco Studio支持开发者在本地完成云侧服务资源的开发与部署，并可在端侧工程中调用您开发的云侧代码，真正实现端云一体化开发。

1. 选择云开发工程模板，根据工程向导[创建端云一体化开发工程](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-devproject)。
2. 分别为Cloud Foundation Kit提供的各个服务完成端云代码的开发、调试和部署。
    
    说明
    
    云侧与端侧工程的代码可并行开发，一般无先后顺序。但若需在端侧代码中调用云侧代码，云侧代码必须先部署到AGC云端，因此建议您先完成云侧代码的开发、调试与部署，再进行端侧代码开发与调试。
    
    1. 开发云侧工程：在云侧工程开发Cloud Foundation Kit提供的服务，目前包括云函数、云对象和云数据库。
        - [开发云函数](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-cloudfunctions)：在云侧工程下创建并配置函数、开发函数代码、调试函数、部署函数到AGC云端。
        - [开发云对象](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-cloudobj)：在云侧工程下创建云对象、开发云对象代码、调试云对象、部署云对象到AGC云端。
        - [开发云数据库](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-clouddb)：在云侧工程下中创建对象类型、在对象类型中添加数据条目、部署云数据库到AGC云端。
    2. [部署云侧工程](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-deploy)：云侧工程代码开发调试完毕后，一键部署云侧工程到AGC云端。
    3. [开发端侧工程](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-appdevelop)：在端侧工程下通过Cloud Foundation Kit调用部署的云侧代码，包括调用云函数、调用云对象、访问云数据库、调用云存储。
    
3. 端云两侧工程代码全部开发完成后，将端云一体化工程打包成APP，提交至AGC申请上架。

## 约束与限制

### 支持的设备

仅支持手机。

### 支持的国家/地区

当前仅在中国境内（香港特别行政区、澳门特别行政区、中国台湾除外）提供服务。

### 支持的签名方式

当前自动签名仅支持“[关联注册应用进行签名](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section20943184413328)”方式。

### 模拟器支持情况

从6.0.0(20) Beta5版本开始支持模拟器开发，但与真机存在部分能力差异，详情请参见“[模拟器与真机的差异](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-emulator-specification#section38231424133213)”。

关于如何使用模拟器调试，请参见[使用模拟器调试](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-emulator)。

## 计费说明

使用端云一体化开发服务时，会开通并使用云函数、云数据库、云存储服务。华为为每个服务都提供了免费额度以供试用，具体的配额明细可以参考各服务的配额说明：

- [云函数](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/agc-cloud-function-price-0000001211271102)
- [云数据库](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/agc-clouddb-price-0000001256815629)
- [云存储](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/agc-cloudstorage-price-0000001253665999)

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddevguide "端云一体化开发")
