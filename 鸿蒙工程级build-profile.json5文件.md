## 配置文件结构
[[如何在鸿蒙系统使用 ArkUI]]
# 构建任务说明

更新时间: 2025-12-16 15:59

本章节将对构建的任务进行说明，可以更直观地了解到构建的任务流程。

## 任务流程图

### HAP基础任务流程图

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155915.50134837046492302218549043129725:50001231000000:2800:B9B719F8B70E689E57AB86547AE7F93C8DBC72601862DE939D06049F4D11C479.png)

### HSP基础任务流程图

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155915.48761968710471847237049741577045:50001231000000:2800:594FAB7D165DE9FB4E8D6D9D48359D621767661EF8FE07B42DC3938AD705E5A9.png)

### HAR基础任务流程图

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155915.46636201374848853510110785054053:50001231000000:2800:4BD59C8444DBD993DEEE0D4BE0828B8F3BE65FFC02CA4C33CF5D7B9A9C1EA777.png)

## 使用命令查看任务

在DevEco Studio中可以通过以下命令获得任务相关的信息。

1. hvigorw taskTree

获取任务树时会根据工程中的模块将模块中注册的任务以下图形式输出：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155915.73542356824737492442510610415630:50001231000000:2800:511AD5DCFAB4E3F50E427BE7F669BF70D40B4330879FA78DECEE5C500EEDCAED.png)

执行顺序举例说明：如图所示，assembleHap依赖CollectDebugSymbol，CollectDebugSymbol依赖于PackageHap；则任务执行顺序为PackageHap->CollectDebugSymbol->assembleHap。

## 任务详细说明

根据任务职能的不同主要分为以下几个类型的任务。

|任务类别|任务说明|
|:--|:--|
|Hook|hook任务|
|ArkTS|ArkTS编译相关任务|
|JS|JS编译相关任务|
|Resources|资源编译、处理、链接、合并相关的任务|
|Package|打包相关的任务|
|Sign|签名相关的任务|
|Verification|验证项目或者依赖项设置等相关的任务|
|Generate|生成和转换前置文件等相关的任务|
|Config|生成，合并，处理配置文件等相关的任务|
|Native|Native编译等相关的任务|
|Help|查询hvigor帮助信息的相关任务|
|Other|未分类的任务|

### Hook

- assembleHap 编译构建hap模块的Hook任务。
- assembleHsp 编译构建hsp模块的Hook任务。
- assembleHar 编译构建har模块的Hook任务。
- assembleApp 编译构建app模块的Hook任务。
- assembleDevHqf 支持增量部署的Hook任务。
- HotReloadBuild HotReloadArkTS前置Hook任务。
- PreviewBuild PreviewArkTS前置Hook任务。
- buildHotReloadResource 热加载资源相关前置Hook任务。
- PreviewHookCompileResource 预览时资源编译处理是否支持Restool增量方式编译的Hook任务。
- GenerateBuildProfile 生成BuildProfile.ets文件的Hook任务。
- BuildUnitTestHook 单元测试编译资源相关前置Hook任务。
- buildPreviewerResource 预览资源相关前置Hook任务。
- compileNative native资源相关前置Hook任务。
- UnitTestBuild UnitTestArkTS前置Hook任务。
- test 使用命令行执行Local Test的Hook任务。
- onDeviceTest 使用命令行执行Instrument Test的Hook任务。

### ArkTS

- CompileArkTS/BuildArkTS 通过rollup调用loader编译ArkTS源码。
- PreviewArkTS 预览模式下，通过rollup调用loader编译ArkTS源码。
- HotReloadArkTS 热加载场景下，通过rollup调用loader编译ArkTS源码。
- OhosTestCompileArkTS/OhosTestBuildArkTS ohos测试场景下，通过rollup调用loader编译ArkTS源码。
- HarCompileArkTS/HarBuildArkTS 构建HAR包场景下，通过rollup调用loader编译ArkTS源码。
- UnitTestArkTS 单元测试场景下，通过rollup调用loader编译ArkTS源码。

### JS

- CompileJS/BuildJS 调用loader编译js源码。
- OhosTestCompileJS/OhosTestBuildJS ohos测试场景下，调用loader编译js源码。

### Resources

- ProcessResource 处理和生成用文件方式编译资源的中间文件。
- PreviewProcessResource 预览场景下，处理和生成用文件方式编译资源的中间文件。
- CompileResource 调用restool 编译资源。
- PreviewCompileResource 预览场景下，调用restool编译资源。
- ProcessLibs 收集hap和har依赖中的.so文件。

### Package

- PackageHap 调用打包工具打hap包。
- PackageHar 调用打包工具打har包。
- PackageHsp 调用打包工具打hsp包。
- PackageApp 调用打包工具打app包。
- PackageHqf 调用打包工具打增量包。
- PackageSharedHar 调用打包工具打hsp模块的har包。
- PackageSharedTgz 调用打包工具将hsp模块生成的未签名hap和har包打包成tgz包。
- PackageSignHar 调用打包工具打带签名的har包，当前仅在daemon模式下生效。

### Sign

- SignHap 调用签名工具给hap包签名。
- SignHsp 调用签名工具给hsp包签名。
- SignApp 调用签名工具给app包签名。
- SignHqf 调用签名工具给增量包签名。
- SignModuleRemoteHsp 调用签名工具给模块级ohpm仓上的hsp包签名。
- SignProjectRemoteHsp 调用签名工具给工程级ohpm仓上的hsp包签名。

### Verification

- PreBuild 模块级预检查任务。
- PreBuildApp 工程级预检查任务。
- PreCheckSyscap syscap相关配置预检查任务。

### Generate

- GenerateLoaderJson 生成loader.json文件。
- GenerateMetadata 生成metadata.json文件。
- SyscapTransform syscap转换任务。
- MakePackInfo 生成模块级别的pack.info。
- MakeProjectPackInfo 生成工程级别的pack.info。
- ProcessPackageJson 对package.json文件进行处理。
- ProcessOHPackageJson 对oh_package.json5文件进行处理。
- GeneratePackRes 生成pack.res文件。
- CreateBuildProfile 生成hap/hsp的BuildProfile.ets文件。
- CreateHarBuildProfile 生成har的BuildProfile.ets文件。
- PrepareQuickfix 通过校验获取增量文件并输出到quickfix.json文件中。

### Config

- ProcessProfile 处理module.json5文件。
- PrepareSharedHarResource 生成打包shared library的package.json和module.json。
- UnitTestProcessProfile UnitTestBuild场景处理构建中间产物module.json文件。
- MergeProfile 合并module.json5文件。
- PreviewUpdateAssets 预览模式下，Stage模型在编译预览代码前更新前置任务生成的module.json和main_pages.json文件。

### Native

- BuildNativeWithNinja 将native代码编译成so文件。
- BuildNativeWithCmake 用CMake编译CPP源码。

### Help

- tasks 查看hvigor的全部任务及详情。
- taskTree 查看当前工程涉及的任务树。

### Other

- ReplaceUnitTestIndexFile 单元测试替换入口文件。
- ReplacePreviewerPage 接受预览器提供的参数替换页面文件中的参数。
- OhosTestCopyMockConfigJson 测试框架执行mock时将mock-config.json拷贝到测试包中。
- clean 清理生成的Build目录。
- collectCoverage 基于仪表打点数据生成覆盖率统计报表。

### Sync

- init 初始化工程。

### Init

该任务类型与Sync下的init不同，该过程中无具体任务，主要负责执行调用hvigor前的准备工作。
工程级build-profile.json5文件整体的结构如下。

1. app
2. └── signingConfigs
3.     └── name
4.     └── material
5.         └── storePassword
6.         └── certpath
7.         └── keyAlias
8.         └── keyPassword
9.         └── profile
10.         └── signAlg
11.         └── storeFile
12.     └── type
13. └── products
14.     └── name
15.     └── signingConfig
16.     └── bundleName
17.     └── buildOption
18.         └── packOptions
19.             └── buildAppSkipSignHap
20.             └── fastBuildApp
21.             └── enableSourceCodeCheck
22.             └── deduplicateHar
23.         └── debuggable
24.         └── generateSharedTgz
25.         └── resOptions
26.             └── compression
27.                 └── media
28.                     └── enable
29.                 └── filters
30.                     └── method
31.                         └── type
32.                         └── blocks
33.                     └── files
34.                         └── path
35.                         └── size
36.                         └── resolution
37.                     └── exclude
38.                         └── path
39.                         └── size
40.                         └── resolution
41.             └── resCompileThreads
42.             └── copyCodeResource
43.                 └── enable
44.                 └── includes
45.                 └── excludes
46.             └── ignoreResourcePattern
47.             └── excludeHarRes
48.             └── includeAppScopeRes
49.             └── idDefinedFilePath
50.         └── externalNativeOptions
51.             └── path
52.             └── abiFilters
53.             └── arguments
54.             └── cppFlags
55.         └── sourceOption
56.             └── workers
57.         └── nativeLib
58.             └── filter
59.                 └── excludes
60.                 └── pickFirsts
61.                 └── pickLasts
62.                 └── enableOverride
63.                 └── select
64.                     └── package
65.                     └── version
66.                     └── includePattern
67.                     └── excludePattern
68.                     └── include
69.                     └── exclude
70.             └── debugSymbol
71.                 └── strip
72.                 └── exclude
73.             └── headerPath
74.             └── collectAllLibs
75.             └── excludeFromHar
76.             └── excludeSoFromInterfaceHar
77.         └── napiLibFilterOption
78.             └── excludes
79.             └── pickFirsts
80.             └── pickLasts
81.             └── enableOverride
82.         └── arkOptions
83.             └── buildProfileFields
84.             └── types
85.             └── tscConfig
86.                 └── targetESVersion
87.                 └── maxFlowDepth
88.             └── autoLazyImport
89.             └── autoLazyFilter
90.                 └── include
91.                 └── exclude
92.             └── reExportCheckMode
93.             └── branchElimination
94.             └── skipOhModulesLint
95.             └── expandImportPath
96.                 └── enable
97.                 └── exclude
98.             └── apPath
99.             └── hostPGO
100.         └── strictMode
101.             └── noExternalImportByPath
102.             └── useNormalizedOHMUrl
103.             └── caseSensitiveCheck
104.             └── duplicateDependencyCheck
105.             └── harLocalDependencyCheck
106.             └── enableStrictCheckOHModule
107.         └── nativeCompiler
108.         └── removePermissions
109.             └── name
110.         └── preloadSystemSo
111.     └── runtimeOS
112.     └── arkTSVersion
113.     └── compileSdkVersion
114.     └── compatibleSdkVersion
115.     └── targetSdkVersion
116.     └── compatibleSdkVersionStage
117.     └── bundleType
118.     └── label
119.     └── icon
120.     └── versionCode
121.     └── versionName
122.     └── resource
123.         └── directories
124.     └── output
125.         └── artifactName
126.     └── vendor
127. └── buildModeSet
128.     └── name
129.     └── buildOption
130. └── multiProjects
131. └── capabilities
132.     └── bundleName
133.     └── config
134.         └── name
135.         └── capability
136.         └── subCapabilities
137.             └── name
138.             └── capability
139. modules
140. └── name
141. └── srcPath
142. └── targets
143.     └── name
144.     └── applyToProducts

## 配置文件字段说明

工程级build-profile.json5文件包含以下字段。

**表1** 工程级build-profile.json5文件字段说明
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|[app](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile-app#section1140014592111)|对象|必选|编译配置信息。|
|[modules](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile-app#section1961794812219)|对象数组|必选|工程中包含的所有模块的信息，数组长度至少为1。|

## app

app是工程级的编译配置，包含签名、product等信息。

**表2** app
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|[signingConfigs](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile-app#section153288223224)|对象数组|可选|签名方案信息，可配置多个。|
|[products](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile-app#section45865492619)|对象数组|可选|产品品类，可配置多个。如需配置多个，相关说明请参见[配置多目标产物](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-customized-multi-targets-and-products)章节。|
|[buildModeSet](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile-app#section137297344398)|对象数组|可选|构建模式集合，可配置多个。|
|multiProjects|布尔值|可选|当前工程是否支持多工程构建：<br><br>- true：支持。<br>- false（缺省默认值）：不支持。|
|[capabilities](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile-app#section1526318211219)|对象数组|可选|应用开通的开放能力，具体开通方式请参考[关联注册应用进行签名](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section20943184413328)。<br><br>从DevEco Studio 6.0.0 Beta5版本开始支持。|

## modules

modules是一个对象数组，用于描述工程中包含的所有模块，数组长度至少为1。模块配置包括名称、路径和target-product关联配置。

**表3** modules
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|name|字符串|必选|模块的名称。该名称需与module.json5文件中的[module.name](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6%E6%A0%87%E7%AD%BE)保持一致。<br><br>在FA模型中，对应的文件为config.json。|
|srcPath|字符串|必选|模块的源码路径，为模块根目录相对工程根目录的相对路径，允许模块根目录不在当前工程下，详情请参考[导入/引用模块](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-add-new-module#section1295434814255)。<br><br>说明<br><br>当前支持引用其他工程下的HAR和HSP模块。|
|[targets](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile-app#table1433185416814)|对象数组|可选|模块的target信息，用于[定制多目标构建产物](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-customized-multi-targets-and-products)时，配置模块target和应用product之间的关联关系。|

**表4** targets
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|name|字符串|必选|target名称，在各个模块级build-profile.json5中的targets字段定义。HAR模块无需配置。|
|applyToProducts|字符串数组|可选|target关联的product。HAR模块无需配置。|

modules字段示例：

1. {
2.   "modules": [
3.     {
4.       "name": "entry",
5.       "srcPath": "./entry",
6.       "targets": [
7.         {
8.           "name": "default",
9.           "applyToProducts": [  
10.             "default"    // 表示将该模块下的"default" Target打包到"default" Product中
11.           ]
12.         }
13.       ]
14.     }
15.   ]
16. }

## signingConfigs

signingConfigs是一个对象数组，用于配置签名方案，可配置多个。

**表5** signingConfigs
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|name|字符串|必选|签名方案的名称，仅支持数字和字母，长度为1~64个字符。|
|[material](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile-app#table1269413811158)|对象|必选|签名方案相关材料，如密码、证书等。<br><br>通过**File > Project Structure... > Project > Signing Configs**界面，进行自动签名后，material节点中的各配置项会自动填充。|
|type|字符串|可选|签名类型：<br><br>- HarmonyOS<br>- OpenHarmony|

**表6** material
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|storePassword|字符串|必选|密钥库密码，以密文形式呈现。|
|certpath|字符串|必选|调试或发布证书文件地址，文件后缀为.cer。|
|keyAlias|字符串|必选|密钥别名信息。|
|keyPassword|字符串|必选|密钥密码，以密文形式呈现。|
|profile|字符串|必选|调试或发布证书Profile文件地址，文件后缀为.p7b。|
|signAlg|字符串|必选|密钥库signAlg参数。当前可配置值SHA256withECDSA。|
|storeFile|字符串|必选|密钥库文件地址，文件后缀为.p12。|

signingConfigs字段示例：

1. {
2.   "app": { 
3.     "signingConfigs": [
4.       {
5.         "name": "default",
6.         "type": "HarmonyOS",
7.         "material": {  
8.           "certpath": "D:\\SigningConfig\\debug_hos.cer",
9.           "storePassword": "******",
10.           "keyAlias": "debugKey",
11.           "keyPassword": "******",
12.           "profile": "D:\\SigningConfig\\debug_hos.p7b", 
13.           "signAlg": "SHA256withECDSA",
14.           "storeFile": "D:\\SigningConfig\\debug_hos.p12"
15.         }
16.       }
17.     ]
18.   }
19. }

## products

products是一个对象数组，用于配置产品品类信息，可配置多个，如通用默认版、付费版、免费版等。如需配置多个，相关说明请参见[配置多目标产物](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-customized-multi-targets-and-products)章节。

**表7** products
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|name|字符串|必选|产品的名称，必须存在name为"default"的product。|
|signingConfig|字符串|可选|当前产品品类的签名方案名称，需要在[signingConfigs.name](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile-app#section153288223224)中定义。如果没有配置，默认不签名。|
|compatibleSdkVersion|字符串/数值|必选|标识应用/元服务运行所需兼容的最低SDK版本，应用/元服务不能安装在低于该版本的设备。当前支持的版本参考[所有HarmonyOS版本](https://developer.huawei.com/consumer/cn/doc/harmonyos-releases/overview-allversion)。相关字段与应用兼容性关系参见[应用兼容性说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-releases/app-compatibility)。<br><br>- 运行环境是HarmonyOS时，字段类型是字符串，配置示例："compatibleSdkVersion": "6.0.1(21)"。<br>- 运行环境是OpenHarmony时，字段类型是数值，配置示例："compatibleSdkVersion": 21。<br><br>说明<br><br>构建APP包时，打包工具会对HSP和HAP的compatibleSdkVersion字段进行校验，满足条件的才能打包，具体请参考[打包工具](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/packing-tool)。|
|targetSdkVersion|字符串/数值|可选|标识应用/元服务运行所需目标SDK版本，是系统提供的前向兼容手段。如果新SDK版本中API行为发生变更，将应用/元服务安装到新系统后，可通过该字段提供向前兼容手段，在新系统版本保持老的API行为。<br><br>如未配置，默认与compileSdkVersion保持一致。当前支持的版本参考[所有HarmonyOS版本](https://developer.huawei.com/consumer/cn/doc/harmonyos-releases/overview-allversion)。相关标签与应用兼容性关系参见[应用兼容性说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-releases/app-compatibility)。<br><br>- 运行环境是HarmonyOS时，字段类型是字符串，配置示例："targetSdkVersion": "6.0.1(21)"。<br>- 运行环境是OpenHarmony时，字段类型是数值，配置示例："targetSdkVersion": 21。<br><br>说明<br><br>- 建议配置该字段。<br>- 构建APP包时，打包工具会对HSP和HAP的targetSdkVersion字段进行校验，满足条件的才能打包，具体请参考[打包工具](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/packing-tool)。|
|compileSdkVersion|字符串/数值|可选|标识编译应用/元服务所使用的SDK版本。当前支持的版本参考[所有HarmonyOS版本](https://developer.huawei.com/consumer/cn/doc/harmonyos-releases/overview-allversion)。相关标签与应用兼容性关系参见[应用兼容性说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-releases/app-compatibility)。<br><br>- 运行环境是HarmonyOS时，字段类型是字符串，配置示例："compileSdkVersion": "6.0.1(21)"。<br>- 运行环境是OpenHarmony时，字段类型是数值，配置示例："compileSdkVersion": 21。<br><br>说明<br><br>- 运行环境是HarmonyOS时，该字段不需要显性配置，编译时默认使用DevEco Studio内置的SDK版本。如果配置，只能配置为当前DevEco Studio配套的SDK版本，不允许配置为其他SDK版本。<br>- 运行环境是OpenHarmony时，必须配置该字段。|
|compatibleSdkVersionStage|字符串|可选|当compatibleSdkVersion为API 12时，用于控制不同beta版本的兼容，默认值为beta1，应用/元服务不能安装在低于该版本的设备。<br><br>当compatibleSdkVersion高于API 12时，无需配置该字段。<br><br>说明<br><br>配置betaX就能生成在对应betaX版本镜像上运行的应用，但是无法使用高于betaX版本的特性，例如在API 12中beta3版本提供的sendable function和lazy import两个特性在配置beta2或beta1时无法正常使用。|
|bundleName|字符串|可选|产品的包名。|
|[buildOption](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile-app#section14222051575)|对象|可选|产品的编译构建配置。|
|runtimeOS|字符串|可选|产品的运行环境：<br><br>- HarmonyOS<br>- OpenHarmony|
|arkTSVersion|字符串|可选|ArkTS语法检查工具的版本号：1.0，1.1。<br><br>默认为当前ArkTS语法检查工具支持的最新版本。<br><br>仅API 11及以上版本工程支持。|
|bundleType|字符串|可选|包的类型：<br><br>- app：应用<br>- atomicService：元服务<br>- shared：共享包|
|label|字符串|可选|应用/元服务名称。<br><br>说明<br><br>配置products中的label、icon、versionCode、versionName、resource字段后，编译构建时将根据此处的配置替换app.json5中的相关配置，常用于应用和元服务可分可合构建打包场景。|
|icon|字符串|可选|应用/元服务图标。|
|versionCode|整型数值|可选|版本号。|
|versionName|字符串|可选|版本名称。|
|[resource](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile-app#table49010413236)|对象|可选|名称和图标对应的资源所在目录。|
|[output](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile-app#table41925113333)|对象|可选|定制产品生成的应用包的配置。|
|vendor|字符串|可选|供应商。|

**表8** resource
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|directories|字符串数组|必选|资源地址路径。|

**表9** output
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|artifactName|字符串|必选|自定义产品生成的应用包名称，可由数字、英文字母、中划线、下划线和英文句号（.）组成，支持输入版本号。|

products字段示例：

1. {
2.   "products": [
3.     {
4.       "name": "default",
5.       "signingConfig": "default",
6.       "bundleName": "com.example.myapplication",
7.       "compatibleSdkVersion": "6.0.1(21)",
8.       "targetSdkVersion": "6.0.1(21)",
9.       "runtimeOS": "HarmonyOS",
10.       "arkTSVersion": "1.1",
11.       "bundleType": "app",
12.       "label": "$string:app_name",
13.       "icon": "$media:app_background",
14.       "versionCode": 1000000,
15.       "versionName": "1.0.0",
16.       "resource": {
17.         "directories": [
18.           "./AppScope/resources"
19.         ]
20.       },
21.       "output": {
22.         "artifactName": "customizedTargetOutputName-1.0.0"
23.       },
24.       "vendor": "customizedProductVendorName",
25.     }
26.   ]
27. }

## buildModeSet

buildModeSet是一个对象数组，表示构建模式集合，可配置多个构建模式。

**表10** buildModeSet
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|name|字符串|必选|构建模式名称。默认生成debug，release和test三种模式，支持开发者自定义，其中test模式虽然没有出现在配置文件中，但是利用测试框架开启测试时会自动使用test编译模式。|
|[buildOption](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile-app#section14222051575)|对象|可选|构建模式使用的具体配置信息。|

## capabilities

capabilities是应用开通的开放能力，具体开通方式请参考[关联注册应用进行签名](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section20943184413328)。

**表11** capabilities
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|bundleName|字符串|必选|当前开放能力归属的包名。|
|[config](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile-app#section746298142519)|对象数组|必选|具体的开放能力配置。|

### config

**表12** config
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|name|字符串|必选|开放能力名称。|
|capability|字符串|可选|开放能力的唯一标识符。如果subCapabilities不存在，则该值必填。|
|[subCapabilities](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile-app#table98912388270)|对象数组|可选|具体的子开放能力。如果存在子开放能力，则该值必填。|

**表13** subCapabilities
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|name|字符串|必选|子开放能力名称。|
|capability|字符串|必选|子开放能力的唯一标识符。|

## buildOption

buildOption是构建使用的具体配置信息，buildModeSet和products下均支持配置buildOption。此外，模块级build-profile.json5中也支持配置buildOption。工程级别buildOption配置会与模块级别的buildOption进行合并，具体合并规则和优先级请参考[合并编译选项规则](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-compilation-options-customizing-guide#section1727865610255)。

**表14** buildOption
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|[packOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile-app#section03812484215)|对象|可选|打包相关配置项。|
|debuggable|布尔值|可选|当前编译产物是否为可调试模式：<br><br>- true：可调试。构建的产物包的ets目录下存在sourceMaps.map文件，此文件包含源码映射等信息。<br>- false：不可调试。<br><br>如果未配置debuggable字段，使用release的编译模式时，默认值为false，使用其他编译模式时，默认值为true。|
|generateSharedTgz|布尔值|可选|编译HSP模块时是否生成tgz包。<br><br>- true：生成。<br>- false：不生成。<br><br>如果未配置generateSharedTgz，根据debuggable字段决定是否生成tgz包。debuggable为true时，不生成tgz包，debuggable为false时，生成tgz包。<br><br>从DevEco Studio 5.1.1 Beta1版本开始支持。<br><br>说明<br><br>该字段配置后仅对HSP模块生效。|
|[resOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile-app#section5494153192911)|对象|可选|资源编译配置项。|
|[externalNativeOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-cpp#section0721057575)|对象|可选|Native编译配置项。|
|[sourceOption](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile-app#section15753419515)|对象|可选|源码相关配置。使用不同的标签对源代码进行分类，以便在构建过程中对不同的源代码进行不同的处理。|
|[nativeLib](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-cpp#section15889929155720)|对象|可选|Native 库（.so）相关配置。|
|[napiLibFilterOption](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile-app#section1488712919295)|对象|可选|NAPI库（.so）文件的筛选选项。标记为废弃，不建议使用，推荐使用[nativeLib/filter](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-cpp#section15889929155720)。|
|[arkOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile-app#section111543473013)|对象|可选|ArkTS 编译配置。|
|[strictMode](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile-app#section13181758123312)|对象|可选|严格模式。|
|nativeCompiler|字符串|可选|指定Native编译时使用的编译器，包括：<br><br>- Original（缺省默认值）：原有的OpenHarmony Native编译器。<br>- BiSheng：使用[毕昇编译器](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/bisheng-compiler)进行Native编译。<br><br>说明<br><br>升级到DevEco Studio 5.1.1 Release版本后，新建Native C++工程默认使用毕昇编译器，打开历史工程会弹窗提示，点击**立即体验**可以切换使用毕昇编译器。|
|[removePermissions](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile-app#section99591415322)|对象数组|可选|编译HAP/HSP模块时，指定需要删除的依赖包中的冗余权限，模块本身的权限不会被删除。|
|preloadSystemSo|布尔值|可选|是否收集应用入口所使用的系统so，收集的系统so会在应用冷启动时进行预加载，优化应用的冷启动性能。<br><br>- true：收集。<br>- false（缺省默认值）：不收集。<br><br>从DevEco Studio 6.0.0 Beta3版本开始支持。<br><br>说明<br><br>- 应用入口：在module.json5的module下配置的srcEntry标签，或者在module.json5的abilities中配置了具有入口能力的skills标签（即配置了entity.system.home和ohos.want.action.home）。<br>- 仅支持HAP和字节码HAR，编译HAP时，被应用入口import的文件或者源码HAR，如果存在系统so，也会被收集；字节码HAR在被集成时，系统so会被合并到HAP中。<br>- 变量动态import不支持收集。<br>- preloadSystemSo和hvigor-config.json5文件的ohos.arkCompile.singleFileEmit字段互斥，不支持同时设置为true。|

### packOptions

packOptions是打包相关配置项。

**表15** packOptions
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|buildAppSkipSignHap|布尔值|可选|构建APP时，是否跳过生成签名HAP：<br><br>- true：跳过，即不生成签名HAP。<br>- false（缺省默认值）：不跳过，即生成签名HAP。<br><br>编译构建APP时，无需生成签名HAP，可将此参数修改为true，从而提升编译构建性能。|
|fastBuildApp|布尔值|可选|构建APP时，是否在模块下生成HAP/HSP产物。<br><br>- true：不生成HAP/HSP产物，直接生成APP产物，可加快构建速度。<br>- false（缺省默认值）：生成HAP/HSP产物，同时生成APP产物。<br><br>说明<br><br>- 当fastBuildApp配置为true时，无论buildAppSkipSignHap配置为true还是false，都不会生成HAP产物。<br>- 当fastBuildApp配置为false时，是否生成HAP产物，以buildAppSkipSignHap配置为准。|
|enableSourceCodeCheck|布尔值|可选|是否检查HAP/HSP/HAR包（不包括未开启混淆的源码HAR）产物中的源码文件，如果检查，当产物中存在源码文件时，编译时会进行Warning提示。<br><br>- true（缺省默认值）：检查。<br>- false：不检查。<br><br>从DevEco Studio 6.0.0 Beta3版本开始支持。<br><br>说明<br><br>- 源码文件是指包含以下后缀的文件：['.c', '.h', '.cpp', '.cs', '.java', '.rs', '.py', '.go', '.ets', '.js', '.ts']。<br>- [release模式编译的混淆源码har包](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-har#section19788284410)中的'.js', '.ts'和'.d.ets'文件不会被检查。<br>- resources目录下的'.js'文件不会被检查。|
|deduplicateHar|布尔值|可选|构建APP/HAP/HSP时，当HAP/HSP依赖相同的HAR时（包括HAP和HSP依赖相同的HAR，多个HSP依赖相同的HAR），是否去除HSP中重复的HAR，减少包体积。<br><br>- true：去除，HAR仅会打包到HAP中，同时需要配置以下字段。<br>    - 工程级build-profile.json5中配置[idDefinedFilePath](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile-app#section5494153192911)。<br>    - 工程级build-profile.json5的useNormalizedOHMUrl配置为true。<br>    - [module.json5](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file)的libIsolation配置为false。<br>- false（缺省默认值）：不去除，HAR会打包到每个HAP/HSP中。<br><br>说明<br><br>- 从DevEco Studio 6.0.1 Beta1版本开始支持，并且设备系统需要升级到6.0.1(21)，工程级build-profile.json5的compatibleSdkVersion需要配置为6.0.1(21)。<br>- 多个HSP依赖相同的HAR时，依赖HSP的HAP需要显式配置依赖该HAR。<br>- 仅支持本地HSP模块，不支持已打包的HSP包。<br>- 不支持去除重复HAR的场景：<br>    - 一个应用包含多个HAP时<br>    - 单独运行或调试HSP<br>    - 仪器测试和本地单元测试<br>    - 预览场景|

1. "buildOption": {
2.   "packOptions": {
3.     "buildAppSkipSignHap": true,
4.     "fastBuildApp": false,
5.   }
6. }

### resOptions

resOptions是资源编译配置项。

**表16** resOptions
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|[compression](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile-app#section2095319147103)|对象|可选|对工程预置图片资源进行纹理压缩的编译配置参数。|
|resCompileThreads|整型数值|可选|资源编译的线程数量 ，最小为1，最大为主机的CPU核数。<br><br>该字段从DevEco Studio 5.1.0 Release版本开始支持。|
|[copyCodeResource](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile-app#table263894423012)|对象|可选|对模块的src/main/ets目录下的资源文件（非源码文件）拷贝的编译配置参数。<br><br>说明<br><br>该字段对[不开启混淆的源码HAR](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-har#section197792874110)不生效。|
|ignoreResourcePattern|字符串数组|可选|根据glob语法，对资源目录resources或开发者自定义的资源目录下的文件/文件夹名称进行过滤，匹配到的文件不会被打包到产物中。<br><br>从DevEco Studio 5.1.1 Beta1版本开始支持。<br><br>说明<br><br>- 如果规则中带有路径（例如./src/main/a.png），该规则不生效。<br>- 如果未配置该字段，打包HAP/HSP时存在默认的过滤规则：默认不打包.git、.svn、.scc、.ds_store、desktop.ini、picasa.ini、cvs、thumbs.db以及以.开头的隐藏文件/目录和以~结尾的文件。<br>- 配置该字段后，会覆盖默认的过滤规则；如果字段配置为空数组，则不应用任何过滤规则，即全部资源都打包。|
|excludeHarRes|字符串数组|可选|编译HAP/HSP模块时，指定不参与资源编译的三方HAR包的包名，配置后，依赖HAR包中的资源不会被打包到产物中，支持直接依赖和间接依赖。<br><br>从DevEco Studio 6.0.0 Beta2版本开始支持。<br><br>说明<br><br>该字段仅对编译HAP/HSP生效。|
|includeAppScopeRes|布尔值|可选|编译HSP时，是否将AppScope目录下的资源打包到产物中。<br><br>- true（缺省默认值）：打包。<br>- false：不打包。<br><br>从DevEco Studio 6.0.0 Beta2版本开始支持。<br><br>说明<br><br>- 该字段仅对HSP模块生效。<br>- 配置为false后，app.json5的icon和label字段不再对HSP模块生效。|
|idDefinedFilePath|字符串|可选|使用HAR包去重能力时（即工程级build-profile.json5的deduplicateHar配置为true），指定用户自定义的json5文件路径，用于固定资源id，支持绝对/相对路径，文件示例如下。<br><br>去除重复的HAR包后，HAR仅会打包到HAP中，因此HSP需要通过这些固定的id，跨包访问HAP中的资源。<br><br>从DevEco Studio 6.0.1 Beta1版本开始支持。|

idDefinedFilePath指定的固定资源id的json5文件示例：

1. // id-config.json5
2. {
3.   "record": [{
4.     "type": "string",        // 资源类型，推荐应用内所有的资源都固定id
5.     "name": "app_name",      // 资源名称
6.     "id": "0x01000000"       // 用户自定义的资源id，仅支持十六进制，支持的id范围是[0x01000000, 0x06FFFFFF]，[0x08000000, 0xFFFFFFFF]
7.   }, {
8.     "type": "float",
9.     "name": "float1",
10.     "id": "0x01000001"
11.   }, {
12.     "type": "media",
13.     "name": "background",
14.     "id": "0x01000002"
15.   }, {
16.     "type": "profile",
17.     "name": "profile1",
18.     "id": "0x01000003"
19.   }]
20. }

**表17** copyCodeResource
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|enable|布尔值|可选|是否将src/main/ets目录下的资源文件（.ets/.ts/.js以外的其他文件）打包到产物中。<br><br>- true（缺省默认值）：打包。<br>- false：不打包。|
|includes|字符串数组|可选|- 当enable为true时，用于指定打包的资源文件，其他资源文件均不会打包到产物中，支持glob语法，以"**/"开头。<br>- 当enable为false时，includes不生效。<br><br>从DevEco Studio 6.0.0 Beta2版本开始支持。<br><br>说明<br><br>includes和excludes互斥，只能配置一个。|
|excludes|字符串数组|可选|- 当enable为true时，用于指定不打包的资源文件，其他资源文件均会打包到产物中，支持glob语法，以"**/"开头。<br>- 当enable为false时，excludes不生效。|

注意

- 模块的src/main/ets目录下，编译时仅处理.ets/.ts/.js文件，其他文件会被当作资源文件打包进产物中，不会进行混淆或加密，如需过滤请配置excludes字段。
- 请勿将源码等文件放在以.开头的系统隐藏目录中，可能会导致过滤规则失效，会将src/main/ets目录下的所有文件作为资源文件打包进产物中，不会进行混淆或加密。

resOptions字段示例：

1. "buildOption": {
2.   "resOptions": {
3.     "resCompileThreads": 2,
4.     "copyCodeResource": {
5.       "enable": true,
6.       "excludes": ['**/entry/src/main/ets/component/big_picture.png', '**/*.yml', '**/subDir/**'],   // includes字段配置方式相同
7.     },
8.     "ignoreResourcePattern": ['*.png' ,'abc.json'],
9.     "excludeHarRes": ['har'],
10.     "idDefinedFilePath": "./id-config.json5",    // 支持绝对路径和相对路径
11.   }
12. }

### sourceOption

sourceOption是源码相关配置，使用不同的标签对源代码进行分类，以便在构建过程中对不同的源代码进行不同的处理。

**表18** sourceOption
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|workers|字符串数组|可选|指定使用node.js工作器的JS/TS源代码，源代码在构建过程中单独处理。|

sourceOption字段示例：

1. "buildOption": {
2.   "sourceOption": {
3.     "workers": [
4.       "./src/main/ets/common/constants/CommonConstants.ets"
5.     ]
6.   }
7. }

### napiLibFilterOption

napiLibFilterOption是NAPI库（.so）文件的筛选选项，字段已废弃，不建议使用，推荐使用[nativeLib/filter](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-cpp#section15889929155720)。

**表19** napiLibFilterOption
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|excludes|字符串数组|可选|排除的.so文件。罗列的NAPI库将不会被打包。|
|pickFirsts|字符串数组|可选|按照.so文件的优先级顺序，打包最高优先级的.so文件。|
|pickLasts|字符串数组|可选|按照.so文件的优先级顺序，打包最低优先级的.so文件。|
|enableOverride|布尔值|可选|是否允许当.so文件重名冲突时，使用高优先级的.so文件覆盖低优先级的.so文件：<br><br>- true：允许。<br>- false（缺省默认值）：不允许。|

### arkOptions

arkOptions是ArkTS编译配置。

**表20** arkOptions
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|[buildProfileFields](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-get-build-profile-para)|对象|可选|用于ArkTS的构建配置。自定义类型，key可由数字、英文、下划线、中划线组成，value类型仅支持string、number、boolean。|
|[types](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkoptions-guide#types)|字符串数组|可选|自定义类型，可配置包名或d.ts/d.ets文件路径。|
|[tscConfig](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile-app#table1714014154115)|对象|可选|与编译TS语法相关的配置选项。|
|autoLazyImport|布尔值|可选|编译时是否自动将符合lazy-import语法规范的import语句添加"lazy"关键字。仅支持在源码中添加"lazy"关键字，不包含依赖的字节码HAR包或HSP。关于lazy-import的介绍及相关影响请参考[延迟加载（lazy import）](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-lazy-import)。<br><br>- true：添加。<br>- false（缺省默认值）：不添加。<br><br>说明<br><br>- 如果配置为true，编译时不会做场景识别，即源码中任何符合语法规范的import语句都会被添加"lazy"。<br>- 仅支持Stage模型。|
|[autoLazyFilter](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile-app#table1551310818378)|对象|可选|自定义添加"lazy"关键字的模块，仅当autoLazyImport为true时生效。<br><br>从DevEco Studio 6.0.1 Beta1版本开始支持。|
|reExportCheckMode|字符串|可选|针对以下场景，编译时是否进行拦截报错：使用lazy import导入的变量，在同文件中被再次导出。<br><br>- noCheck（缺省默认值）：不检查，不报错。<br>- compatible：兼容模式，报Warning。<br>- strict：严格模式，报Error。<br><br>该字段从DevEco Studio 5.0.5 Release版本开始支持。|
|branchElimination|布尔值|可选|是否启用代码分支裁剪，减少编译产物大小，开启后，在release编译模式下，不会被执行到的代码分支会被裁剪掉，示例请参考[branchElimination示例](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile-app#li12224142193612)。<br><br>- true：启用（将导致使用"ApplyChanges"功能时，对const声明的常量的值进行的修改可能不生效）。<br>- false（缺省默认值）：不启用。<br><br>说明<br><br>- 仅支持API 11及以上的Stage模型。<br>- HAR模块仅字节码HAR配置生效，非字节码HAR配置不生效。<br>- 仅支持const声明的bool类型常量和const声明的string/number类型常量的判断表达式。<br>- 不支持间接导入，例如A文件中定义const变量A1，B文件导入A1，导出B1，ets导入B1进行判断，无法进行裁剪。|
|skipOhModulesLint|布尔值|可选|是否跳过工程中oh_modules目录的[ArkTS规则检查](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/typescript-to-arkts-migration-guide)。从DevEco Studio 6.0.0 Beta1版本开始支持。<br><br>- true：跳过。<br>- false（缺省默认值）：不跳过。|
|[expandImportPath](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile-app#table1921576135914)|对象|可选|import路径展开相关配置选项。<br><br>从DevEco Studio 6.0.0 Beta3版本开始支持。|
|apPath|字符串|可选|说明<br><br>API 11及以上版本不再支持，即该字段配置后不再生效。<br><br>应用热点信息文件路径。|
|hostPGO|布尔值|可选|是否启用配置文件引导优化功能：<br><br>- true：启用。<br>- false（缺省默认值）：不启用。<br><br>从API 10开始废弃，由于partial模式可能存在兼容性问题，请使用Target AOT能力，不建议使用Host AOT。|

- branchElimination字段配置为true时，代码分支的裁剪情况示例如下：
    
    1. # 编译生成的BuildProfile文件
    2. export const DEBUG = false;
    3. export const VERSION_CODE = 100;
    4. # 开发者自定义的ets文件
    5. import { DEBUG } from 'BuildProfile';
    6. import { VERSION_CODE } from 'BuildProfile';
    7. if (DEBUG)
    8.   {XXX} // 该分支会被裁剪掉
    9. else
    10.   {XXX}
    11. if (VERSION_CODE){XXX} // 该语法发生了类型转换，不支持代码裁剪。
    12. if (VERSION_CODE === 100){XXX} // 若需要裁剪代码，使用该方式，显式指定判断条件为boolean类型。
    

**表21** tscConfig
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|targetESVersion|字符串|可选|指定TS语法编译产物的目标运行时EcmaScript版本，包括：<br><br>- ES2017<br>- ES2021（缺省默认值）。|
|maxFlowDepth|整型数值|可选|设置最大控制流递归深度，范围为[2000,65535]，默认为2000。<br><br>该字段从DevEco Studio 5.1.0 Release版本开始支持。<br><br>说明<br><br>maxFlowDepth不支持动态修改，即在hvigorfile.ts/hvigorconfig.ts文件中，不支持通过[setBuildProfileOpt](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-build-expanding-context#section16692151412211)方法设置maxFlowDepth。|

**表22** expandImportPath
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|enable|布尔值|可选|是否启用import路径展开，启用后可以提升应用的运行时性能。关于import路径展开的原理及开启后的副作用请参考[通过import路径展开优化性能](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-module-side-effects#%E9%80%9A%E8%BF%87import%E8%B7%AF%E5%BE%84%E5%B1%95%E5%BC%80%E4%BC%98%E5%8C%96%E6%80%A7%E8%83%BD)。<br><br>- true：启用。<br>- false（缺省默认值）：不启用。<br><br>说明<br><br>- import XXX from 'A'，A必须为本地HAR模块，并且仅当A为包名时支持进行展开，A为相对路径或包名+路径都不支持展开。<br>- HAR模块单独编译时不生效。|
|exclude|字符串数组|可选|配置oh-package.json5中的依赖别名，用于指定不展开import语句的依赖，仅支持本地HAR模块。|

**表23** autoLazyFilter
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|include|字符串数组|可选|- 当autoLazyImport为true时，指定自动添加"lazy"关键字的包名（即oh-package.json5中的name），其他包不会添加"lazy"关键字，支持正则语法。<br>- 当autoLazyImport为false时，include不生效。<br><br>说明<br><br>- include和exclude互斥，只能配置一个。<br>- include不支持配置空数组或空字符串，至少配置一个包名，并且包名不能重复。|
|exclude|字符串数组|可选|- 当autoLazyImport为true时，指定不添加"lazy"关键字的包名，其他包都会添加"lazy"关键字，支持正则语法。<br>- 当autoLazyImport为false时，exclude不生效。<br><br>说明<br><br>- include和exclude互斥，只能配置一个。<br>- exclude不支持配置空数组或空字符串，至少配置一个包名，并且包名不能重复。|

arkOptions字段示例：

1. "buildOption": {
2.   "arkOptions": {
3.     "buildProfileFields": {
4.       "targetData": "TargetData",
5.       "data": "DataTargetDefault"
6.     },
7.     "tscConfig": {
8.       "targetESVersion": "ES2021",
9.       "maxFlowDepth": 3000,
10.     },
11.     "autoLazyImport": true,
12.     "autoLazyFilter": {
13.       "include": ['entry']
14.     },
15.     "reExportCheckMode": "compatible",
16.     "branchElimination": true,
17.     "expandImportPath": {
18.       "enable": true,
19.       "exclude": ['localhar']
20.     },
21.   }
22. }

### strictMode

strictMode用于定义严格模式。

**表24** strictMode
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|noExternalImportByPath|布尔值|可选|是否严格检查绝对路径导入方式和相对路径跨模块导入方式。<br><br>- true：严格检查。<br>- false：不严格检查。<br><br>说明<br><br>从DevEco Studio NEXT Beta1（5.0.3.800）版本开始，当工程级build-profile.json5中useNormalizedOHMUrl配置为true时，noExternalImportByPath缺省默认值为true；当useNormalizedOHMUrl配置为false时，noExternalImportByPath缺省默认值为false。|
|useNormalizedOHMUrl|布尔值|可选|是否使用标准化的OHMUrl（OHMUrl的定义参考以下说明）格式，标准化的OHMUrl统一了原有OHMUrl的格式。使用集成态HSP和[字节码HAR](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-har#section16598338112415)需使用标准化的OHMUrl格式。<br><br>- true：使用标准化的OHMUrl格式。<br>- false（缺省默认值）：不使用标准化的OHMUrl格式。<br><br>说明<br><br>- 从API 12开始支持。<br>- 一个ets文件在编译后会成为安装包的一部分，这个ets文件对应的字节码称为一个字节码段，OHMUrl是用来定位一个字节码段的标识。<br>- 若工程引用了HAR/HSP，需确保工程的useNormalizedOHMUrl配置和HAR/HSP的useNormalizedOHMUrl配置保持一致，同时配置为true或false。<br>- useNormalizedOHMUrl设置为true时，可能对本地源码HAR的混淆产生影响，具体请参考[本地源码HAR包](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/source-obfuscation-practice#%E6%9C%AC%E5%9C%B0%E6%BA%90%E7%A0%81har%E5%8C%85)。<br>- 从DevEco Studio NEXT Beta1（5.0.3.800）版本开始，当useNormalizedOHMUrl设置为true时，不允许通过相对路径跨模块或绝对路径导入文件，oh-package.json5中依赖的包使用的别名需要和依赖包的oh-package.json5的name保持一致，具体的适配指导请参考[变更说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-releases/ide-changelog-500-release#section1130320228353)。|
|caseSensitiveCheck|布尔值|可选|导入文件是否严格校验大小写，支持相对路径和软链接。<br><br>- true：严格校验。<br>- false（缺省默认值）：不严格校验。|
|duplicateDependencyCheck|布尔值|可选|是否校验本地HSP模块有无依赖相同的HAR。仅在Build App(s)起效。<br><br>- true：如果本地HSP模块依赖了相同的HAR（包括本地/远程、直接/间接），则编译报错。（注意：当依赖链中存在远程HSP，则该远程HSP及其依赖链不参与校验）。<br>- false（默认缺省值）：不启用校验。|
|harLocalDependencyCheck|布尔值|可选|是否对HAR产物启用本地依赖校验。<br><br>- true：如果oh-package.json5中的dependencies、dynamicDependencies存在本地依赖，则编译报错。<br>- false（默认缺省值）：不启用校验。<br><br>说明<br><br>除HAR模块外，HSP模块编译时也会生成HAR产物，该配置同样生效。|
|enableStrictCheckOHModule|布尔值|可选|调用远程HAR/HSP包中的方法时，是否严格校验传入参数的类型。<br><br>- true：严格校验，如果参数类型是undefined/null，报Error错误。<br>- false（默认缺省值）：不严格校验，如果参数类型是undefined/null，报Warning告警。<br><br>从DevEco Studio 6.0.1 Beta1版本开始支持。|

strictMode字段示例：

1. "buildOption": {
2.   "strictMode": {
3.     "useNormalizedOHMUrl": true,
4.     "caseSensitiveCheck": true,
5.   }
6. }

### removePermissions

removePermissions是一个对象数组，用于编译HAP/HSP模块时，指定需要删除的依赖包中的冗余权限，模块本身的权限不会被删除。

**表25** removePermissions
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|name|字符串|必选|待删除的权限名称，需要包含在依赖包的module.json的requestPermissions中。|

removePermissions字段示例：

1. "buildOption": {
2.   "removePermissions": [
3.     {
4.       "name": "ohos.permission.ABILITY_BACKGROUND_COMMUNICATION"
5.     },
6.     {
7.       "name": "ohos.permission.ACCELEROMETER"
8.     }
9.   ]
10. }

## compression

compression是对工程预置图片资源进行纹理压缩的编译配置参数。

**表26** compression
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|[media](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile-app#section1915545641714)|对象|可选|对资源目录下media目录的图片进行纹理压缩的配置参数。|
|[filters](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile-app#section185719543186)|对象数组|可选|文件过滤配置参数。<br><br>说明<br><br>编译过程中会依次遍历图片文件，并与filters条件进行匹配，一旦匹配成功，则完成该图片的处理。当工程级和模块级同时配置时，先按照模块级的过滤条件匹配，一旦匹配成功，则忽略工程级的过滤条件；如果模块级的没有匹配成功，继续按工程级的条件进行匹配。|

### media

media是对资源目录下media目录的图片进行纹理压缩的配置参数。

**表27** media
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|enable|布尔值|可选|是否对media图片启用纹理压缩。<br><br>- true：启用。<br>- false（缺省默认值）：不启用。<br><br>说明<br><br>- 在linux系统的构建场景下，请确认系统环境已[安装libGL1库](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-command-line-building-app#section1478651816216)。<br>- 对图片进行纹理压缩会改变文件名称和内容，在[分层图标](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arkui-drawabledescriptor#layereddrawabledescriptor)以及二次编辑的场景下会引起图片显示异常，请进一步使用filters排除掉这部分文件。|

### filters

filters是文件过滤配置参数。

**表28** filters
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|[method](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile-app#table1568916396220)|对象|必选|纹理压缩的方式。|
|[files](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile-app#table19762944112414)|对象|可选|指定用来参与压缩的文件，与exclude字段配合使用。|
|[exclude](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile-app#table6219104952519)|对象|可选|从files中剔除掉不需要压缩的文件。|

**表29** method
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|type|字符串|必选|转换类型。<br><br>- astc（Adaptive Scalable Texture Compression）：自适应可变纹理压缩，一种对GPU友好的纹理格式，可在设备侧更快地显示，有更少的内存占用。<br>- sut（SUper compression for Texture） ：纹理超压缩，可在设备侧更快地显示，有更少的内存占用，相比astc具备更大压缩率和更少ROM占用。|
|blocks|字符串|必选|astc/sut转换类型的扩展参数，决定画质和压缩率，当前仅支持"4x4"。|

**表30** files
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|path|字符串数组|可选|指定“按路径匹配”的过滤条件，符合glob规范，格式为相对路径。|
|size|二维数组|可选|指定“按大小匹配”的过滤条件，格式为[min,max]，闭区间，表示大小从min到max之间的文件。<br><br>- 每个数值可以填数字、字符串或字符串中带单位（大小写均可），如[0, '1k']。<br>- 单位K/k=1024，M/m=1024*1024，G/g=1024*1024*1024。<br>- 区间最大值可省略，表示无限大，如['3K']。|
|resolution|二维数组|可选|指定“按分辨率匹配”的过滤条件，配置示例：<br><br>1. resolution:[<br>2.   [<br>3.     { width:32, height:32 },  // 最小宽高<br>4.     { width:64, height:64 },  // 最大宽高<br>5.   ],  // 分辨率在32*32到64*64之间的图片<br>6.   [<br>7.     { width:200, height:200 }, // 最小宽高<br>8.     // 此处第2个不填表示最大宽高是无限大<br>9.   ],  // 分辨率大于200*200的图片<br>10. ]<br><br>- width和height只能是数字。<br>- 最大宽高可以省略，表示无限大。|

**表31** exclude
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|path|字符串数组|可选|同files/path。|
|size|二维数组|可选|同files/size。|
|resolution|二维数组|可选|同files/resolution。|

compression字段示例：

1. "buildOption": {
2.   "resOptions": {
3.     "compression": {
4.       "media": {
5.         "enable": true // 是否对media图片启用纹理压缩
6.       },
7.       // 纹理压缩文件过滤，非必填，不填会压缩资源目录中的所有图片
8.       "filters": [
9.         {
10.           "method": {
11.             "type": "sut", // 转换类型
12.             "blocks": "4x4" // 转换类型的扩展参数
13.           },
14.           // 指定用来参与压缩的文件，需要满足所有条件且不被exclude过滤的文件才会参与压缩
15.           "files": {
16.             "path": ["./**/*"], // 指定资源目录中的所有文件
17.             "size": [[0, '10k']], // 指定大小10k以下的文件
18.             // 指定分辨率小于2048*2048的图片
19.             "resolution": [
20.               [
21.                 { "width": 0, "height": 0 }, // 最小宽高
22.                 { "width": 2048, "height": 2048 } // 最大宽高
23.               ]
24.             ]
25.           },
26.           // 从files中剔除掉不需要压缩的文件，需要满足所有过滤条件的文件才会被剔除
27.           "exclude": {
28.             "path": ["./**/*.jpg"], // 过滤所有jpg文件
29.             "size": [[0, '1k']], // 过滤大小1k以下的文件
30.             // 过滤分辨率小于1024*1024的图片
31.             "resolution": [
32.               [
33.                 { "width": 0, "height": 0 }, // 最小宽高
34.                 { "width": 1024, "height": 1024 } // 最大宽高
35.               ]
36.             ]
37.           }
38.         }
39.       ]
40.     }
41.   }
42. }
# # 构建产物说明

更新时间: 2025-12-16 15:59

## HAP/HSP构建产物说明

以HAP为例，release模式的构建产物一般包含以下文件：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155922.26914130308093517834378772912181:50001231000000:2800:A86845997C4EBAD1D86DA9021685A654F7F9D7E96B8DE0F237772DEBDE845117.png)

- resources：构建产物中的资源文件目录，如图片、媒体资源、配置文件等。
- modules.abc：构建产物中通过源码编译出的字节码文件。
- module.json：构建产物中通过模块src目录中的module.json5处理后的运行时配置文件，具体参考[module.json5配置文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file)。
- resources.index：构建产物中的资源索引文件, 包含模块中所有的资源ID、资源名称、资源类型以及资源值等信息。
- pack.info：构建产物中的包内容描述文件，在安装升级时提供相关信息。
- pkgContextInfo.json：构建产物中的语境信息表文件，用于运行时查找依赖库信息。

注意

- resources.index文件中可以看到明文信息，为防止泄漏，请勿将敏感信息直接明文配置在如string.json等资源文件中。
- 模块的src/main/ets目录，编译时仅处理.ets/.ts/.js文件，其他文件会被当作资源文件打包进产物中，不会进行混淆或加密，因此请勿将敏感信息存放在该目录下。
- 以debug模式构建的HAP/HSP包中的ets目录下存在sourceMaps.map文件，此文件包含源码映射等信息。sourceMaps.map文件格式及解析流程请参考[ArkTS堆栈解析原理](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-exception-stack-parsing-principle#section5924954297)。
- LiteWearable设备使用标准JS运行时，因此对应的应用开发在release模式下的构建产物中包含JS源码，请注意代码资产保护。

## HAR构建产物说明

详情请参考[构建HAR](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-har)。

## App构建产物说明

APP构建产物如下，其中包名取决于个人项目中的模块名，与下图可能不同：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155922.48162420776963401028866918433587:50001231000000:2800:30C6560D01F52A3CCB8EF83FEEF91B3536956073A679ADE1CB738E35FD075524.png)

- entry-default.hap：由字节码、资源、三方库、配置文件等打包生成的entry类型的hap包，是App应用安装和运行的基本单元，application-default.hap是feature类型的hap。
- library-default.hsp：由字节码、资源、三方库、配置文件等打包生成的动态共享包，可实现代码和资源共享。
- pack.info：应用App构建产物中的包内容描述文件，提供应用市场发布上架所需信息。
- pac.json：应用App构建产物中的隐私清单文件，文件中可配置的字段请参考[pac.json5隐私清单文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-pac)，用于提供应用市场发布上架所需信息。
- # hvigor-config.json5文件

更新时间: 2025-12-16 15:59

## 配置文件结构

hvigor-config.json5文件整体的结构如下。

1. modelVersion
2. dependencies
3. execution
4. └── analyze
5. └── daemon
6. └── incremental
7. └── parallel
8. └── typeCheck
9. └── optimizationStrategy
10. logging
11. └── level
12. debugging
13. └── stacktrace
14. nodeOptions
15. └── maxOldSpaceSize
16. └── maxSemiSpaceSize
17. └── exposeGC
18. javaOptions
19. └── Xmx
20. properties
21. └── hvigor.cacheDir
22. └── ohos.buildDir
23. └── enableSignTask
24. └── ohos.arkCompile.maxSize
25. └── hvigor.pool.cache.capacity
26. └── hvigor.pool.maxSize
27. └── ohos.pack.compressLevel
28. └── hvigor.analyzeHtml
29. └── hvigor.dependency.useNpm
30. └── ohos.compile.lib.entryfile
31. └── ohos.align.target
32. └── ohos.fallback.target
33. └── ohos.arkCompile.sourceMapDir
34. └── ohos.collect.debugSymbol
35. └── hvigor.enableMemoryCache
36. └── hvigor.memoryThreshold
37. └── ohos.nativeResolver
38. └── ohos.arkCompile.noEmitJs
39. └── ohos.arkCompile.singleFileEmit
40. └── ohos.sign.har
41. └── hvigor.keepDependency
42. └── ohos.arkCompile.emptyBundleName
43. └── ohos.uiTransform.Optimization
44. └── ohos.har.excludeHspDependencies
45. └── ohos.processLib.optimization
46. └── ohos.obfuscationRules.optimization
47. └── hvigor.incremental.optimization
48. └── hvigor.task.schedule.optimization
49. └── ohos.byteCodeHar.integratedOptimization
50. └── ohos.rollupCache.usePathPlaceholder
51. └── ohos.rollupCache.useSourceHash
52. └── ohos.arkCompile.writeRollupCache
53. └── ohos.align.deviceTypes
54. └── ohos.dependencies.types.enable
55. └── ohos.defaults.release.cmakebuildtype

## 配置文件字段说明

hvigor-config.json5配置文件包含以下字段。

**表1** hvigor-config.json5文件字段说明
|字段名称|可选/必选|类型|含义|
|:--|:--|:--|:--|
|modelVersion|必选|字符串|开发态版本号。|
|dependencies|必选|对象|当前工程执行构建任务时，依赖的构建插件及版本，为npm源组件。<br><br>说明<br><br>修改dependencies后，请根据界面提示，点击编辑器右上角**Sync Now**安装依赖。|
|[execution](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-set-options#section6901191119219)|可选|对象|执行构建的相关配置参数，仅在命令行场景下生效。|
|[logging](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-set-options#section85176471028)|可选|对象|日志相关配置参数。|
|[debugging](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-set-options#section76575554217)|可选|对象|调测相关配置参数。|
|[nodeOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-set-options#section74431812314)|可选|对象|Node相关配置参数。|
|[javaOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-set-options#section7929682318)|可选|对象|java相关配置参数。|
|[properties](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-set-options#section260315160319)|可选|对象|额外配置参数。|

## execution

execution是执行构建的相关配置参数，除了optimizationStrategy字段外，其他字段仅在命令行构建场景下生效，如果通过DevEco Studio菜单栏构建，需要在**File >** **Settings**（macOS为**DevEco Studio > Preferences/Settings**） **> Build, Execution, Deployment > Build Tools > Hvigor**中设置。

**表2** execution字段说明
|字段名称|可选/必选|类型|含义|
|:--|:--|:--|:--|
|analyze|可选|字符串/布尔值|构建分析模式。<br><br>- normal（默认值）：普通模式，通过简单打点数据进行分析。原default模式已废弃。<br>- advanced：进阶模式，通过更加详细的打点数据进行分析。如果需要更详细的任务耗时数据，请选择该模式。原verbose模式已废弃。<br>- ultrafine：超精细化模式，与advanced模式相比，在ArkTS编译阶段记录更详细的打点数据，但开启后可能导致编译构建时间更长。从DevEco Studio 6.0.0 Beta1版本开始支持。<br>- false：不启用构建分析。|
|daemon|可选|布尔值|是否启用守护进程编译。<br><br>- true（缺省默认值）：启用。<br>- false：不启用。|
|incremental|可选|布尔值|是否启用增量编译。<br><br>- true（缺省默认值）：启用。<br>- false：不启用。|
|parallel|可选|布尔值|是否启用并行编译。<br><br>- true（缺省默认值）：启用。<br>- false：不启用。|
|typeCheck|可选|布尔值|是否启用构建脚本hvigorfile.ts文件的类型检查，启用后构建效率可能会有所降低。<br><br>- true：启用。<br>- false（缺省默认值）：不启用。|
|optimizationStrategy|可选|字符串|指定构建模式。从DevEco Studio 5.1.1 Release版本开始支持。<br><br>- performance：性能优先模式，可加快构建速度，但会占用更多内存。<br>- memory（缺省默认值）：内存优先模式，可以减少编译内存占用。<br><br>说明<br><br>更改模式后，首次编译会执行全量编译。|

execution字段示例：

1. {
2.   "execution": {
3.     "analyze": "normal",
4.     "daemon": true,
5.     "incremental": true,
6.     "parallel": true,
7.     "typeCheck": false,
8.     "optimizationStrategy": "performance",
9.   }
10. }

## logging

logging是日志相关配置参数。

**表3** logging字段说明
|字段名称|可选/必选|类型|含义|
|:--|:--|:--|:--|
|level|可选|字符串|构建时打印日志的级别。<br><br>- debug：调测日志。<br>- info（缺省默认值）：基本信息日志。<br>- warn：告警日志。<br>- error：错误日志。|

logging字段示例：

1. {
2.   "logging": {
3.     "level": "debug"
4.   }
5. }

## debugging

debugging是调测相关配置参数。

**表4** debugging字段说明
|字段名称|可选/必选|类型|含义|
|:--|:--|:--|:--|
|stacktrace|可选|布尔值|是否启用堆栈跟踪。<br><br>- true：启用。<br>- false（缺省默认值）：不启用。|

debugging字段示例：

1. {
2.   "debugging": {
3.     "stacktrace": true
4.   }
5. }

## nodeOptions

nodeOptions是Node相关配置参数。

**表5** nodeOptions字段说明
|字段名称|可选/必选|类型|含义|
|:--|:--|:--|:--|
|maxOldSpaceSize|可选|整型数值|启用守护进程编译时，为守护进程设置最大的老生代内存大小，单位为MB，默认为8192MB。当工程代码量较大出现JS内存溢出时，可以调整该参数。|
|maxSemiSpaceSize|可选|整型数值|启用守护进程编译时，为守护进程设置新生代内存最大的半空间大小，单位为MB，默认为16MB。增加半空间大小可能会提高Node.js的吞吐量，但会消耗更多内存。<br><br>该字段从DevEco Studio 5.1.0 Release版本开始支持。|
|exposeGC|可选|布尔值|是否启用GC（Garbage Collection，内存回收），启用后会优化编译过程的峰值内存。<br><br>- true（缺省默认值）：启用。<br>- false：不启用。|

nodeOptions字段示例：

1. {
2.   "nodeOptions": {
3.     "maxOldSpaceSize": 8192,
4.     "maxSemiSpaceSize": 16,
5.     "exposeGC": true,
6.   }
7. }

## javaOptions

javaOptions是java相关配置参数。

**表6** javaOptions字段说明
|字段名称|可选/必选|类型|含义|
|:--|:--|:--|:--|
|Xmx|可选|整型数值|设置JVM最大堆内存，单位为MB，默认为512MB。|

javaOptions字段示例：

1. {
2.   "javaOptions": {
3.     "Xmx": 512
4.   }
5. }

## properties

properties是额外配置参数。

**表7** properties字段说明
|字段名称|可选/必选|类型|含义|
|:--|:--|:--|:--|
|hvigor.cacheDir|可选|字符串|指定项目根目录下的.hvigor缓存文件夹的存放路径。<br><br>说明<br><br>同名的不同工程不可指定相同的存放位置。|
|ohos.buildDir|可选|字符串|指定项目的构建产物目录（build目录）存放位置。<br><br>说明<br><br>同名的不同工程不可指定相同的存放位置。|
|enableSignTask|可选|布尔值|是否启用HAP或HSP签名任务。<br><br>- true（缺省默认值）：启用。<br>- false：不启用。|
|ohos.arkCompile.maxSize|可选|整型数值|指定编译ArkTS线程的数量，默认为5。|
|hvigor.pool.cache.capacity|可选|整型数值|定义内存中缓存数据的容量，默认为4，数值越小，内存中缓存数据越少。配置为0，表示不启用内存缓存配置。|
|hvigor.pool.maxSize|可选|整型数值|指定编译过程中的线程数量，相比ohos.arkCompile.maxSize增加签名、打包等任务的线程。默认值为“工程的模块数”和“电脑虚拟核数-1”两者的较小值。|
|ohos.pack.compressLevel|可选|字符串|设置打包hap（压缩so）或app（压缩hap）时的压缩率等级。压缩率越高，压缩速度越慢。<br><br>- fast（缺省默认值）：最低等级的压缩率，压缩速度最快。<br>- standard：适中等级的压缩率，压缩速度适中。<br>- ultimate：最高等级的压缩率，压缩速度最慢。|
|hvigor.analyzeHtml|可选|布尔值|是否生成构建可视化html文件。<br><br>- true：生成构建可视化html文件。生成的html文件存放在工程的.hvigor/report目录下，该文件可直接在浏览器中打开。<br>- false（缺省默认值）：不生成构建可视化html文件。|
|hvigor.dependency.useNpm|可选|布尔值|指定是否使用npm下载hvigor依赖。<br><br>若未配置该字段，当Node.js版本 ≥ 16时，默认使用pnpm下载依赖。在某些特定场景，可以通过配置该字段指定使用npm下载依赖。<br><br>- true：对于任意Node版本，都使用npm下载依赖。<br>- false（缺省默认值）：Node.js版本 ≥ 16时，使用pnpm下载依赖；Node.js版本 ＜ 16时，使用npm下载依赖。|
|ohos.compile.lib.entryfile|可选|布尔值|指定是否从入口文件开始编译：<br><br>- true：表示从模块的入口文件开始编译，将编译入口文件及被引用的文件，没被引用的文件不会参与编译流程。<br>- false（缺省默认值）：表示将src/main/ets下的ets和ts文件进行全量编译，涉及到以下场景：<br>    1. 构建HSP时，存在于src/main/ets下的ets和ts文件都会被编译到产物中。<br>    2. release模式对HAR混淆或构建字节码HAR时，存在于src/main/ets下的ets和ts文件都会被编译到产物中。<br>    3. 构建HAP/HSP时，存在于动态依赖的HAR模块src/main/ets下的ets和ts文件都会被编译到产物中。|
|ohos.align.target|可选|字符串|指定本次构建任务所有涉及到的模块及其依赖的模块的target。详情请参考[多产物构建target](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-customized-multi-targets-and-products-guides#section7121513141619)。|
|ohos.fallback.target|可选|字符串数组|指定本次构建任务所有涉及到的模块及其依赖模块的fallback target，fallback target是一个特定优先级的target，各target的优先级顺序：align target > 命令行指定target > 被依赖的父模块target > fallback target > default target。详情请参考[多产物构建target](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-customized-multi-targets-and-products-guides#section7121513141619)。|
|ohos.arkCompile.sourceMapDir|可选|字符串|指定sourceMap文件的生成路径，方便开发者进行堆栈的回栈与错误信息的定位，当前仅支持Stage模型。若没有指定路径，默认生成在build/{productName}/outputs/{targetName}/mapping下。<br><br>说明<br><br>从API 12开始支持。|
|ohos.collect.debugSymbol|可选|布尔值|是否将[sourceMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-exception-stack-parsing-principle#section666114451518)、[nameCache](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-exception-stack-parsing-principle#section19215122372720)和带调试信息的so文件归档到产物路径下，根据选择的构建模式，如果是构建HAP/HSP/HAR，会归档到模块的build/{productName}/outputs/{targetName}/symbol的release或debug目录下；如果是构建APP，会将HAP/HSP模块的文件归档到工程的build/outputs/{productName}/symbol的release或debug目录下。<br><br>- true：归档。<br>- false：不归档。<br><br>说明<br><br>- 如果不配置，release模式时默认值为true，debug模式时默认值为false。<br>- 仅支持Stage模型。<br>- nameCache文件仅在release模式下且开启混淆后才会生成，release模式下不开启混淆以及debug模式下均不生成这个文件。|
|hvigor.enableMemoryCache|可选|布尔值|是否开启缓存，开启缓存会加快增量编译速度，关闭缓存能够节省内存占用，但是会增加增量编译时间。<br><br>- true（缺省默认值）：开启。<br>- false：不开启。|
|hvigor.memoryThreshold|可选|整型数值|内存管理阈值，单位为MB，当编译构建占用内存超过此阈值时，新加入的编译任务会等待，直到正在进行的编译任务结束，新的编译任务才能开始，此配置将导致编译时间延长。<br><br>说明<br><br>- 配置该字段后，即使hvigor.enableMemoryCache配置为true，也不进行缓存。<br>- 该字段配置为很小的值时，构建任务会串行执行，等效于配置ohos.arkCompile.maxSize:1；配置为很大的值时，与不配置没有差异。|
|ohos.nativeResolver|可选|布尔值|ArkTS编译过程中是否使用高性能插件进行依赖寻址，使用高性能插件可以降低编译过程的峰值内存，加快编译速度。<br><br>- true（缺省默认值）：使用。<br>- false：不使用。|
|ohos.arkCompile.noEmitJs|可选|布尔值|ArkTS编译过程中是否生成js中间产物，具体方案及开启后的影响请参考[优化编译中间产物生成](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-experimental-properties#section11117155101617)。<br><br>- true：不生成。<br>- false（缺省默认值）：生成。|
|ohos.arkCompile.singleFileEmit|可选|布尔值|是否开启单文件解析完成后写入磁盘的能力，具体方案及开启后的影响请参考[文件写入磁盘](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-experimental-properties#section1131619813214)。<br><br>- true：开启。<br>- false（缺省默认值）：不开启。|
|ohos.sign.har|可选|布尔值|是否启用HAR签名任务。详情请参考[构建签名HAR](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-har#section116791730173713)。<br><br>- true：启用。<br>- false（缺省默认值）：不启用。|
|hvigor.keepDependency|可选|布尔值|是否保持hsp中的所有依赖。如果保持则不对依赖进行处理，如果不保持，则只会保留hsp模块中的hsp相关依赖。<br><br>- true（缺省默认值）：保持。<br>- false：不保持。|
|ohos.arkCompile.emptyBundleName|可选|布尔值|ArkTS编译转换后的产物，bundleName字段是否为空值。<br><br>- true：bundleName字段的值是空值。<br>- false（缺省默认值）：bundleName字段是应用实际的包名。<br><br>说明<br><br>- 仅支持在EntryAbility中使用loadContentByName加载首页，同时使用Navigation导航进行页面跳转时设置为true，否则会导致应用闪退。<br>- 预览时暂不支持配置该字段，字段默认取值为false。|
|ohos.uiTransform.Optimization|可选|布尔值|是否对ArkTS编译转换后的产物中的bundleName字段开启优化。<br><br>- true：开启，bundleName字段的值是变量。<br>- false（缺省默认值）：不开启，bundleName字段是应用实际的包名。<br><br>该字段从DevEco Studio 5.0.5 Beta1版本开始支持。<br><br>说明<br><br>- 该字段对字节码HAR不生效，字节码HAR产物的bundleName字段的值默认是变量。<br>- 预览时暂不支持配置该字段，字段默认取值为false。|
|ohos.har.excludeHspDependencies|可选|布尔值|构建har包时，产物module.json中是否排除依赖的hsp，排除后，module.json中不包含dependencies字段。<br><br>- true：排除。<br>- false（缺省默认值）：不排除。<br><br>该字段从DevEco Studio 5.1.0 Release版本开始支持。|
|ohos.processLib.optimization|可选|布尔值|是否启用[ProcessLibs任务](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-task-process#li671313965913)性能优化，启用后可以减少ProcessLibs任务中so增量判定的耗时。<br><br>- true：启用。<br>- false（缺省默认值）：不启用。|
|ohos.obfuscationRules.optimization|可选|布尔值|release模式开启混淆时，是否优化三方依赖中混淆配置文件的收集方式，优化后可以减少收集耗时，加快编译速度。<br><br>- true：优化。<br>- false（缺省默认值）：不优化。<br><br>该字段从DevEco Studio 5.1.0 Release版本开始支持。|
|hvigor.incremental.optimization|可选|布尔值|是否开启任务增量判断优化，优化方案及开启后的影响请参考[任务增量判断优化](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-experimental-properties#section95571022144613)。<br><br>- true：开启。<br>- false（缺省默认值）：不开启。|
|hvigor.task.schedule.optimization|可选|布尔值|是否开启任务调度优化，优化方案及开启后的影响请参考[任务调度优化](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-experimental-properties#section09371546164610)。<br><br>- true：开启。<br>- false（缺省默认值）：不开启。|
|ohos.byteCodeHar.integratedOptimization|可选|布尔值|是否开启字节码HAR集成行为优化，开启后，字节码HAR使用的依赖支持配置在工程级oh-package.json5的dependencies或dynamicDependencies中，同时会优化部分依赖收集行为，具体请参考[编译行为差异说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-dependencies#section957371853712)。<br><br>- true：开启。<br>- false（缺省默认值）：不开启。<br><br>从DevEco Studio 5.1.1 Beta1版本开始支持。|
|ohos.rollupCache.usePathPlaceholder|可选|布尔值|是否将build目录下rollup缓存中的绝对路径替换为占位符。该功能是实验特性，开启后会造成读写缓存性能降低。<br><br>- true：是，即缓存中是占位符。<br>- false（缺省默认值）：否，即缓存中是绝对路径。<br><br>从DevEco Studio 6.0.0 Beta1版本开始支持。|
|ohos.rollupCache.useSourceHash|可选|布尔值|是否将build目录下rollup缓存中的源码替换为对应的hash内容，减少缓存大小。该功能是实验特性，可以提升缓存对比和读写性能。<br><br>- true：是，即缓存源码hash。<br>- false（缺省默认值）：否，即缓存源码内容。<br><br>从DevEco Studio 6.0.0 Beta1版本开始支持。|
|ohos.arkCompile.writeRollupCache|可选|布尔值|build目录下是否写入rollup缓存。<br><br>- true（缺省默认值）：写缓存。<br>- false：不写缓存。<br><br>从DevEco Studio 6.0.0 Beta2版本开始支持。|
|ohos.align.deviceTypes|可选|字符串数组|指定归一的设备类型，构建APP时，当HAP/HSP的module.json5中的设备类型是ohos.align.deviceTypes的超集时，模块才会被打包到APP中，同时打包后产物中的设备类型会被设置为ohos.align.deviceTypes的值。<br><br>从DevEco Studio 6.0.0 Beta2版本开始支持。<br><br>说明<br><br>仅支持Stage模型。|
|ohos.dependencies.types.enable|可选|布尔值|编译时是否收集依赖的HAR模块/[源码HAR包](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-har#section197792874110)的[类型声明文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkoptions-guide#types)参与语法校验。如果HAR中配置了类型声明文件，建议开启。<br><br>- true：收集。<br>- false（缺省默认值）：不收集。<br><br>从DevEco Studio 6.0.0 Beta3版本开始支持。|
|ohos.defaults.release.cmakebuildtype|可选|字符串|在release模式下构建时，指定cmake构建类型，对所有模块生效。<br><br>- Debug：不优化代码，附加调试信息。<br>- Release（缺省默认值）：最大化优化代码，但不包含调试信息。<br>- RelWithDebInfo：近似于Release模式，既进行了代码优化，同时保留部分调试信息。<br><br>从DevEco Studio 6.0.1 Beta1版本开始支持。<br><br>说明<br><br>- 模块级build-profile.json5文件中也可以通过[arguments字段](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-exception-stack-parsing-principle#section147714466283)指定cmake构建类型，例如"arguments": "-DCMAKE_BUILD_TYPE=RelWithDebInfo"。arguments字段的优先级比ohos.defaults.release.cmakebuildtype更高。<br>- 在debug模式下构建时，该字段配置无效，默认使用Debug构建类型。|

properties字段示例：

1. {
2.   "properties": {
3.     "hvigor.cacheDir": "D://tmp",
4.     "ohos.buildDir": "D://tmp",
5.     "enableSignTask": true,
6.     "ohos.arkCompile.maxSize": 6,
7.     "hvigor.pool.cache.capacity": 2,
8.     "hvigor.pool.maxSize": 8,
9.     "ohos.pack.compressLevel": "standard",
10.     "hvigor.analyzeHtml": true,
11.     "hvigor.dependency.useNpm": false,
12.     "ohos.compile.lib.entryfile": true,
13.     "ohos.align.target": "target1",
14.     "ohos.fallback.target": ["target1", "target2"],
15.     "ohos.arkCompile.sourceMapDir": "D://MyProject",
16.     "ohos.collect.debugSymbol": false,
17.     "hvigor.enableMemoryCache": true,
18.     "hvigor.memoryThreshold": 1000,
19.     "ohos.nativeResolver": true,
20.     "ohos.arkCompile.noEmitJs": true,
21.     "ohos.arkCompile.singleFileEmit": true,
22.     "ohos.sign.har": true,
23.     "hvigor.keepDependency": false,
24.     "ohos.arkCompile.emptyBundleName": true,
25.     "ohos.align.deviceTypes": ["phone", "tablet"],
26.     "ohos.defaults.release.cmakebuildtype": "RelWithDebInfo",
27.   }
28. }动态生成编译构建产物Hap和App的名称

更新时间: 2025-12-15 21:24

## 问题现象

在编译构建时，能够动态生成编译产物的名称，名称中包含：编译构建时间、版本号、编译模式（debug或者release）。

## 背景知识

hvigor支持在hvigorfile.ts里接收部分编译配置，以实现动态配置构建配置、并使能到构建的过程与结果中。可以自定义hvigor插件，实现编译产物名称的动态配置。

可以参考如下文档：[通过hook以及插件上下文动态配置构建配置](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-config-ohos-sample)。

## 解决方案

- 动态生成app名称实现方案。
    1. 在工程级根目录下的build-profile.json5中定义编译构建产物app名称。
        
        1. {
        2.   "app": {
        3.     "products": [
        4.       {
        5.         "name": "default",
        6.         "output": {
        7.           "artifactName": "testAppName" _// app__产物名称_
        8.         }
        9.       }
        10.     ]
        11.   }
        12. }
        
    2. 在模块级根目录下的build-profile.json5中定义编译构建产物hap名称。
        
        1. {
        2.   "targets": [
        3.     {
        4.       "name": "default",
        5.       "output": {
        6.         "artifactName": "testHapName" _// hap__产物名称_
        7.       }
        8.     }
        9.   ]
        10. }
        
    3. 在工程级根目录下的hvigorfile.ts中自定义hvigor插件动态生成Hap和App的名称。
        
        1. import { appTasks, OhosAppContext, OhosPluginId } from '@ohos/hvigor-ohos-plugin';
        2. import { hvigor, getNode } from '@ohos/hvigor'
        
        3. export function customPlugin(): HvigorPlugin {
        4.   return {
        5.     pluginId: 'customPlugin',
        6.     context() {
        7.       return {
        8.         data: 'modify output name'
        9.       };
        10.     },
        11.     async apply(currentNode: HvigorNode): Promise<void> {
        12.      _ // 获取app插件的上下文对象_
        13.       const appContext = currentNode.getContext(OhosPluginId.OHOS_APP_PLUGIN) as OhosAppContext;
        14.      _ // 通过上下文对象获取从根目录build-profile.json5文件中读出来的obj对象_
        15.       const buildProfileOpt = appContext.getBuildProfileOpt();
        16.       const appJsonOpt = appContext.getAppJsonOpt();
        17.    _   // 修改obj对象为想要的，此处举例修改app中的signingConfigs_
        18.       const products = buildProfileOpt.app.products;
        19.       let date = new Date();
        20.       let formatDate = date.getFullYear().toString() + (date.getMonth() + 1).toString().padStart(2, '0') +
        21.       date.getDate().toString().padStart(2, '0') + '_' + date.getHours().toString().padStart(2, '0') +
        22.       date.getMinutes().toString().padStart(2, '0') + date.getSeconds().toString().padStart(2, '0');
        23.       for (const product of products) {
        24.         if (product.name == 'default') {
        25.           product.output.artifactName = formatDate + '_' + appJsonOpt.app.versionName + '_' +
        26.           product.output.artifactName + '_' + appContext.getBuildMode();
        27.           console.info(`output app name: ${product.output.artifactName}`);
        28.         }
        29.       }
        30.     _  // 将obj对象设置回上下文对象以使能到构建的过程与结果中_
        31.       appContext.setBuildProfileOpt(buildProfileOpt);
        32.       hvigor.nodesEvaluated(async () => {
        33.         currentNode.subNodes((node: HvigorNode) => {
        34.         _  // 获取hpp插件的上下文对象_
        35.           const hapContext = node.getContext(OhosPluginId.OHOS_HAP_PLUGIN) as OhosHapContext;
        36.         _  // 通过上下文对象获取从根目录build-profile.json5文件中读出来的obj对象_
        37.           const hapBuildProfileOpt = hapContext?.getBuildProfileOpt();
        38.           if (hapBuildProfileOpt != undefined) {
        39.             const targets = hapBuildProfileOpt['targets'];
        40.             for (const target of targets) {
        41.               if (target.name == 'default' && target.output?.artifactName != undefined) {
        42.                 target.output.artifactName = formatDate + '_' + appJsonOpt.app.versionName + '_' +
        43.                 target.output.artifactName + '_' + appContext.getBuildMode();
        44.                 console.info(`output hap name: ${target.output?.artifactName}`);
        45.               }
        46.             }
        47.             hapContext.setBuildProfileOpt(hapBuildProfileOpt);
        48.           }
        49.         })
        50.       })
        51.     }
        52.   }
        53. }
        
        54. export default {
        55.   system: appTasks, _/* Built-in plugin of Hvigor. It cannot be modified. */_
        56.   plugins: [customPlugin()]        _/* Custom plugin to extend the functionality of Hvigor. */_
        57. }
        
- 直接修改app名称实现方案。
    
    首先通过afterNodeEvaluate hook获取插件向node中注册的context，然后通过这个context可以修改buildOption或者操作一些任务。
    
    - OhosPluginId：本组件是hvigor-ohos-plugin插件id常量类。
    - OhosAppContext：本组件是appTasks插件对外提供的上下文扩展接口，包括工程信息、product信息等。
    - afterNodeEvaluate：为所有的node添加一个node评估后的回调函数。
    - getBuildProfileOpt：获取当前构建的根目录下build-profile.json5文件中内容的obj对象。
    - setBuildProfileOpt：设置当前构建的build-profile.json5文件中内容的obj对象。
    
    1. _//_ _动态修改App包名加版本号，工程级hvigorfile.ts_
    2. import { appTasks, OhosPluginId } from '@ohos/hvigor-ohos-plugin';
    3. import { hvigor } from '@ohos/hvigor'
    
    4. hvigor.afterNodeEvaluate((hvigorNode) => {
    5.   const context = hvigorNode.getContext(OhosPluginId.OHOS_APP_PLUGIN)
    6.   if (context && context.getBuildProfileOpt) {
    7.     const buildProfile = context.getBuildProfileOpt();
    8.     const products = buildProfile.app.products;
    9.     for (const product of products) {
    10.       if (product.name === context.getCurrentProduct().productBuildOpt.name) {
    11.         product['output'] = {
    12.           'artifactName': 'app-v1.0.3'
    13.         }
    14.       }
    15.     }
    16.     context.setBuildProfileOpt(buildProfile);
    17.   }
    18. })
    
    19. export default {
    20.   system: appTasks, _/* Built-in plugin of Hvigor. It cannot be modified. */_
    21.   plugins: [] _/* Custom plugin to extend the functionality of Hvigor. */_
    22. }
    
- 动态生成har包名称实现方案。
    
    1. import { harTasks, OhosPluginId } from '@ohos/hvigor-ohos-plugin';
    2. import { hvigor } from '@ohos/hvigor'
    
    3. hvigor.afterNodeEvaluate((hvigorNode) => {
    4.   const context = hvigorNode.getContext(OhosPluginId.OHOS_HAR_PLUGIN)
    5.   if (context && context.getBuildProfileOpt) {
    6.     const buildProfile = context.getBuildProfileOpt();
    7.     const targets = buildProfile.targets
    8.     for (const target of targets) {
    9.       if (target.name === 'default') {
    10.         target['output'] = {
    11.           'artifactName': 'myTestHar'
    12.         }
    13.       }
    14.     }
    15.     context.setBuildProfileOpt(buildProfile);
    16.   }
    17. })
    
    18. export default {
    19.   system: harTasks, _/* Built-in plugin of Hvigor. It cannot be modified. */_
    20.   plugins: [] _/* Custom plugin to extend the functionality of Hvigor. */_
    21. }
    

## 常见FAQ

Q：如何在hvigor自定义任务中使用npm包？

A：在“hvigor/hvigor-config.json5”的dependencies中指定依赖，然后在自定义任务中使用。

Q：如何查看编译的详细过程？

A：在hvigor->hvigor-config.json5中"logging": { //"level": "info" }的注释取消，改为debug，改完后的结果为"logging": { "level": "debug" }，在编译时就可以看到编译的详细过程。
# hvigor-config.json5文件

更新时间: 2025-12-16 15:59

## 配置文件结构

hvigor-config.json5文件整体的结构如下。

1. modelVersion
2. dependencies
3. execution
4. └── analyze
5. └── daemon
6. └── incremental
7. └── parallel
8. └── typeCheck
9. └── optimizationStrategy
10. logging
11. └── level
12. debugging
13. └── stacktrace
14. nodeOptions
15. └── maxOldSpaceSize
16. └── maxSemiSpaceSize
17. └── exposeGC
18. javaOptions
19. └── Xmx
20. properties
21. └── hvigor.cacheDir
22. └── ohos.buildDir
23. └── enableSignTask
24. └── ohos.arkCompile.maxSize
25. └── hvigor.pool.cache.capacity
26. └── hvigor.pool.maxSize
27. └── ohos.pack.compressLevel
28. └── hvigor.analyzeHtml
29. └── hvigor.dependency.useNpm
30. └── ohos.compile.lib.entryfile
31. └── ohos.align.target
32. └── ohos.fallback.target
33. └── ohos.arkCompile.sourceMapDir
34. └── ohos.collect.debugSymbol
35. └── hvigor.enableMemoryCache
36. └── hvigor.memoryThreshold
37. └── ohos.nativeResolver
38. └── ohos.arkCompile.noEmitJs
39. └── ohos.arkCompile.singleFileEmit
40. └── ohos.sign.har
41. └── hvigor.keepDependency
42. └── ohos.arkCompile.emptyBundleName
43. └── ohos.uiTransform.Optimization
44. └── ohos.har.excludeHspDependencies
45. └── ohos.processLib.optimization
46. └── ohos.obfuscationRules.optimization
47. └── hvigor.incremental.optimization
48. └── hvigor.task.schedule.optimization
49. └── ohos.byteCodeHar.integratedOptimization
50. └── ohos.rollupCache.usePathPlaceholder
51. └── ohos.rollupCache.useSourceHash
52. └── ohos.arkCompile.writeRollupCache
53. └── ohos.align.deviceTypes
54. └── ohos.dependencies.types.enable
55. └── ohos.defaults.release.cmakebuildtype

## 配置文件字段说明

hvigor-config.json5配置文件包含以下字段。

**表1** hvigor-config.json5文件字段说明
|字段名称|可选/必选|类型|含义|
|:--|:--|:--|:--|
|modelVersion|必选|字符串|开发态版本号。|
|dependencies|必选|对象|当前工程执行构建任务时，依赖的构建插件及版本，为npm源组件。<br><br>说明<br><br>修改dependencies后，请根据界面提示，点击编辑器右上角**Sync Now**安装依赖。|
|[execution](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-set-options#section6901191119219)|可选|对象|执行构建的相关配置参数，仅在命令行场景下生效。|
|[logging](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-set-options#section85176471028)|可选|对象|日志相关配置参数。|
|[debugging](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-set-options#section76575554217)|可选|对象|调测相关配置参数。|
|[nodeOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-set-options#section74431812314)|可选|对象|Node相关配置参数。|
|[javaOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-set-options#section7929682318)|可选|对象|java相关配置参数。|
|[properties](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-set-options#section260315160319)|可选|对象|额外配置参数。|

## execution

execution是执行构建的相关配置参数，除了optimizationStrategy字段外，其他字段仅在命令行构建场景下生效，如果通过DevEco Studio菜单栏构建，需要在**File >** **Settings**（macOS为**DevEco Studio > Preferences/Settings**） **> Build, Execution, Deployment > Build Tools > Hvigor**中设置。

**表2** execution字段说明
|字段名称|可选/必选|类型|含义|
|:--|:--|:--|:--|
|analyze|可选|字符串/布尔值|构建分析模式。<br><br>- normal（默认值）：普通模式，通过简单打点数据进行分析。原default模式已废弃。<br>- advanced：进阶模式，通过更加详细的打点数据进行分析。如果需要更详细的任务耗时数据，请选择该模式。原verbose模式已废弃。<br>- ultrafine：超精细化模式，与advanced模式相比，在ArkTS编译阶段记录更详细的打点数据，但开启后可能导致编译构建时间更长。从DevEco Studio 6.0.0 Beta1版本开始支持。<br>- false：不启用构建分析。|
|daemon|可选|布尔值|是否启用守护进程编译。<br><br>- true（缺省默认值）：启用。<br>- false：不启用。|
|incremental|可选|布尔值|是否启用增量编译。<br><br>- true（缺省默认值）：启用。<br>- false：不启用。|
|parallel|可选|布尔值|是否启用并行编译。<br><br>- true（缺省默认值）：启用。<br>- false：不启用。|
|typeCheck|可选|布尔值|是否启用构建脚本hvigorfile.ts文件的类型检查，启用后构建效率可能会有所降低。<br><br>- true：启用。<br>- false（缺省默认值）：不启用。|
|optimizationStrategy|可选|字符串|指定构建模式。从DevEco Studio 5.1.1 Release版本开始支持。<br><br>- performance：性能优先模式，可加快构建速度，但会占用更多内存。<br>- memory（缺省默认值）：内存优先模式，可以减少编译内存占用。<br><br>说明<br><br>更改模式后，首次编译会执行全量编译。|

execution字段示例：

1. {
2.   "execution": {
3.     "analyze": "normal",
4.     "daemon": true,
5.     "incremental": true,
6.     "parallel": true,
7.     "typeCheck": false,
8.     "optimizationStrategy": "performance",
9.   }
10. }

## logging

logging是日志相关配置参数。

**表3** logging字段说明
|字段名称|可选/必选|类型|含义|
|:--|:--|:--|:--|
|level|可选|字符串|构建时打印日志的级别。<br><br>- debug：调测日志。<br>- info（缺省默认值）：基本信息日志。<br>- warn：告警日志。<br>- error：错误日志。|

logging字段示例：

1. {
2.   "logging": {
3.     "level": "debug"
4.   }
5. }

## debugging

debugging是调测相关配置参数。

**表4** debugging字段说明
|字段名称|可选/必选|类型|含义|
|:--|:--|:--|:--|
|stacktrace|可选|布尔值|是否启用堆栈跟踪。<br><br>- true：启用。<br>- false（缺省默认值）：不启用。|

debugging字段示例：

1. {
2.   "debugging": {
3.     "stacktrace": true
4.   }
5. }

## nodeOptions

nodeOptions是Node相关配置参数。

**表5** nodeOptions字段说明
|字段名称|可选/必选|类型|含义|
|:--|:--|:--|:--|
|maxOldSpaceSize|可选|整型数值|启用守护进程编译时，为守护进程设置最大的老生代内存大小，单位为MB，默认为8192MB。当工程代码量较大出现JS内存溢出时，可以调整该参数。|
|maxSemiSpaceSize|可选|整型数值|启用守护进程编译时，为守护进程设置新生代内存最大的半空间大小，单位为MB，默认为16MB。增加半空间大小可能会提高Node.js的吞吐量，但会消耗更多内存。<br><br>该字段从DevEco Studio 5.1.0 Release版本开始支持。|
|exposeGC|可选|布尔值|是否启用GC（Garbage Collection，内存回收），启用后会优化编译过程的峰值内存。<br><br>- true（缺省默认值）：启用。<br>- false：不启用。|

nodeOptions字段示例：

1. {
2.   "nodeOptions": {
3.     "maxOldSpaceSize": 8192,
4.     "maxSemiSpaceSize": 16,
5.     "exposeGC": true,
6.   }
7. }

## javaOptions

javaOptions是java相关配置参数。

**表6** javaOptions字段说明
|字段名称|可选/必选|类型|含义|
|:--|:--|:--|:--|
|Xmx|可选|整型数值|设置JVM最大堆内存，单位为MB，默认为512MB。|

javaOptions字段示例：

1. {
2.   "javaOptions": {
3.     "Xmx": 512
4.   }
5. }

## properties

properties是额外配置参数。

**表7** properties字段说明
|字段名称|可选/必选|类型|含义|
|:--|:--|:--|:--|
|hvigor.cacheDir|可选|字符串|指定项目根目录下的.hvigor缓存文件夹的存放路径。<br><br>说明<br><br>同名的不同工程不可指定相同的存放位置。|
|ohos.buildDir|可选|字符串|指定项目的构建产物目录（build目录）存放位置。<br><br>说明<br><br>同名的不同工程不可指定相同的存放位置。|
|enableSignTask|可选|布尔值|是否启用HAP或HSP签名任务。<br><br>- true（缺省默认值）：启用。<br>- false：不启用。|
|ohos.arkCompile.maxSize|可选|整型数值|指定编译ArkTS线程的数量，默认为5。|
|hvigor.pool.cache.capacity|可选|整型数值|定义内存中缓存数据的容量，默认为4，数值越小，内存中缓存数据越少。配置为0，表示不启用内存缓存配置。|
|hvigor.pool.maxSize|可选|整型数值|指定编译过程中的线程数量，相比ohos.arkCompile.maxSize增加签名、打包等任务的线程。默认值为“工程的模块数”和“电脑虚拟核数-1”两者的较小值。|
|ohos.pack.compressLevel|可选|字符串|设置打包hap（压缩so）或app（压缩hap）时的压缩率等级。压缩率越高，压缩速度越慢。<br><br>- fast（缺省默认值）：最低等级的压缩率，压缩速度最快。<br>- standard：适中等级的压缩率，压缩速度适中。<br>- ultimate：最高等级的压缩率，压缩速度最慢。|
|hvigor.analyzeHtml|可选|布尔值|是否生成构建可视化html文件。<br><br>- true：生成构建可视化html文件。生成的html文件存放在工程的.hvigor/report目录下，该文件可直接在浏览器中打开。<br>- false（缺省默认值）：不生成构建可视化html文件。|
|hvigor.dependency.useNpm|可选|布尔值|指定是否使用npm下载hvigor依赖。<br><br>若未配置该字段，当Node.js版本 ≥ 16时，默认使用pnpm下载依赖。在某些特定场景，可以通过配置该字段指定使用npm下载依赖。<br><br>- true：对于任意Node版本，都使用npm下载依赖。<br>- false（缺省默认值）：Node.js版本 ≥ 16时，使用pnpm下载依赖；Node.js版本 ＜ 16时，使用npm下载依赖。|
|ohos.compile.lib.entryfile|可选|布尔值|指定是否从入口文件开始编译：<br><br>- true：表示从模块的入口文件开始编译，将编译入口文件及被引用的文件，没被引用的文件不会参与编译流程。<br>- false（缺省默认值）：表示将src/main/ets下的ets和ts文件进行全量编译，涉及到以下场景：<br>    1. 构建HSP时，存在于src/main/ets下的ets和ts文件都会被编译到产物中。<br>    2. release模式对HAR混淆或构建字节码HAR时，存在于src/main/ets下的ets和ts文件都会被编译到产物中。<br>    3. 构建HAP/HSP时，存在于动态依赖的HAR模块src/main/ets下的ets和ts文件都会被编译到产物中。|
|ohos.align.target|可选|字符串|指定本次构建任务所有涉及到的模块及其依赖的模块的target。详情请参考[多产物构建target](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-customized-multi-targets-and-products-guides#section7121513141619)。|
|ohos.fallback.target|可选|字符串数组|指定本次构建任务所有涉及到的模块及其依赖模块的fallback target，fallback target是一个特定优先级的target，各target的优先级顺序：align target > 命令行指定target > 被依赖的父模块target > fallback target > default target。详情请参考[多产物构建target](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-customized-multi-targets-and-products-guides#section7121513141619)。|
|ohos.arkCompile.sourceMapDir|可选|字符串|指定sourceMap文件的生成路径，方便开发者进行堆栈的回栈与错误信息的定位，当前仅支持Stage模型。若没有指定路径，默认生成在build/{productName}/outputs/{targetName}/mapping下。<br><br>说明<br><br>从API 12开始支持。|
|ohos.collect.debugSymbol|可选|布尔值|是否将[sourceMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-exception-stack-parsing-principle#section666114451518)、[nameCache](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-exception-stack-parsing-principle#section19215122372720)和带调试信息的so文件归档到产物路径下，根据选择的构建模式，如果是构建HAP/HSP/HAR，会归档到模块的build/{productName}/outputs/{targetName}/symbol的release或debug目录下；如果是构建APP，会将HAP/HSP模块的文件归档到工程的build/outputs/{productName}/symbol的release或debug目录下。<br><br>- true：归档。<br>- false：不归档。<br><br>说明<br><br>- 如果不配置，release模式时默认值为true，debug模式时默认值为false。<br>- 仅支持Stage模型。<br>- nameCache文件仅在release模式下且开启混淆后才会生成，release模式下不开启混淆以及debug模式下均不生成这个文件。|
|hvigor.enableMemoryCache|可选|布尔值|是否开启缓存，开启缓存会加快增量编译速度，关闭缓存能够节省内存占用，但是会增加增量编译时间。<br><br>- true（缺省默认值）：开启。<br>- false：不开启。|
|hvigor.memoryThreshold|可选|整型数值|内存管理阈值，单位为MB，当编译构建占用内存超过此阈值时，新加入的编译任务会等待，直到正在进行的编译任务结束，新的编译任务才能开始，此配置将导致编译时间延长。<br><br>说明<br><br>- 配置该字段后，即使hvigor.enableMemoryCache配置为true，也不进行缓存。<br>- 该字段配置为很小的值时，构建任务会串行执行，等效于配置ohos.arkCompile.maxSize:1；配置为很大的值时，与不配置没有差异。|
|ohos.nativeResolver|可选|布尔值|ArkTS编译过程中是否使用高性能插件进行依赖寻址，使用高性能插件可以降低编译过程的峰值内存，加快编译速度。<br><br>- true（缺省默认值）：使用。<br>- false：不使用。|
|ohos.arkCompile.noEmitJs|可选|布尔值|ArkTS编译过程中是否生成js中间产物，具体方案及开启后的影响请参考[优化编译中间产物生成](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-experimental-properties#section11117155101617)。<br><br>- true：不生成。<br>- false（缺省默认值）：生成。|
|ohos.arkCompile.singleFileEmit|可选|布尔值|是否开启单文件解析完成后写入磁盘的能力，具体方案及开启后的影响请参考[文件写入磁盘](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-experimental-properties#section1131619813214)。<br><br>- true：开启。<br>- false（缺省默认值）：不开启。|
|ohos.sign.har|可选|布尔值|是否启用HAR签名任务。详情请参考[构建签名HAR](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-har#section116791730173713)。<br><br>- true：启用。<br>- false（缺省默认值）：不启用。|
|hvigor.keepDependency|可选|布尔值|是否保持hsp中的所有依赖。如果保持则不对依赖进行处理，如果不保持，则只会保留hsp模块中的hsp相关依赖。<br><br>- true（缺省默认值）：保持。<br>- false：不保持。|
|ohos.arkCompile.emptyBundleName|可选|布尔值|ArkTS编译转换后的产物，bundleName字段是否为空值。<br><br>- true：bundleName字段的值是空值。<br>- false（缺省默认值）：bundleName字段是应用实际的包名。<br><br>说明<br><br>- 仅支持在EntryAbility中使用loadContentByName加载首页，同时使用Navigation导航进行页面跳转时设置为true，否则会导致应用闪退。<br>- 预览时暂不支持配置该字段，字段默认取值为false。|
|ohos.uiTransform.Optimization|可选|布尔值|是否对ArkTS编译转换后的产物中的bundleName字段开启优化。<br><br>- true：开启，bundleName字段的值是变量。<br>- false（缺省默认值）：不开启，bundleName字段是应用实际的包名。<br><br>该字段从DevEco Studio 5.0.5 Beta1版本开始支持。<br><br>说明<br><br>- 该字段对字节码HAR不生效，字节码HAR产物的bundleName字段的值默认是变量。<br>- 预览时暂不支持配置该字段，字段默认取值为false。|
|ohos.har.excludeHspDependencies|可选|布尔值|构建har包时，产物module.json中是否排除依赖的hsp，排除后，module.json中不包含dependencies字段。<br><br>- true：排除。<br>- false（缺省默认值）：不排除。<br><br>该字段从DevEco Studio 5.1.0 Release版本开始支持。|
|ohos.processLib.optimization|可选|布尔值|是否启用[ProcessLibs任务](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-task-process#li671313965913)性能优化，启用后可以减少ProcessLibs任务中so增量判定的耗时。<br><br>- true：启用。<br>- false（缺省默认值）：不启用。|
|ohos.obfuscationRules.optimization|可选|布尔值|release模式开启混淆时，是否优化三方依赖中混淆配置文件的收集方式，优化后可以减少收集耗时，加快编译速度。<br><br>- true：优化。<br>- false（缺省默认值）：不优化。<br><br>该字段从DevEco Studio 5.1.0 Release版本开始支持。|
|hvigor.incremental.optimization|可选|布尔值|是否开启任务增量判断优化，优化方案及开启后的影响请参考[任务增量判断优化](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-experimental-properties#section95571022144613)。<br><br>- true：开启。<br>- false（缺省默认值）：不开启。|
|hvigor.task.schedule.optimization|可选|布尔值|是否开启任务调度优化，优化方案及开启后的影响请参考[任务调度优化](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-experimental-properties#section09371546164610)。<br><br>- true：开启。<br>- false（缺省默认值）：不开启。|
|ohos.byteCodeHar.integratedOptimization|可选|布尔值|是否开启字节码HAR集成行为优化，开启后，字节码HAR使用的依赖支持配置在工程级oh-package.json5的dependencies或dynamicDependencies中，同时会优化部分依赖收集行为，具体请参考[编译行为差异说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-dependencies#section957371853712)。<br><br>- true：开启。<br>- false（缺省默认值）：不开启。<br><br>从DevEco Studio 5.1.1 Beta1版本开始支持。|
|ohos.rollupCache.usePathPlaceholder|可选|布尔值|是否将build目录下rollup缓存中的绝对路径替换为占位符。该功能是实验特性，开启后会造成读写缓存性能降低。<br><br>- true：是，即缓存中是占位符。<br>- false（缺省默认值）：否，即缓存中是绝对路径。<br><br>从DevEco Studio 6.0.0 Beta1版本开始支持。|
|ohos.rollupCache.useSourceHash|可选|布尔值|是否将build目录下rollup缓存中的源码替换为对应的hash内容，减少缓存大小。该功能是实验特性，可以提升缓存对比和读写性能。<br><br>- true：是，即缓存源码hash。<br>- false（缺省默认值）：否，即缓存源码内容。<br><br>从DevEco Studio 6.0.0 Beta1版本开始支持。|
|ohos.arkCompile.writeRollupCache|可选|布尔值|build目录下是否写入rollup缓存。<br><br>- true（缺省默认值）：写缓存。<br>- false：不写缓存。<br><br>从DevEco Studio 6.0.0 Beta2版本开始支持。|
|ohos.align.deviceTypes|可选|字符串数组|指定归一的设备类型，构建APP时，当HAP/HSP的module.json5中的设备类型是ohos.align.deviceTypes的超集时，模块才会被打包到APP中，同时打包后产物中的设备类型会被设置为ohos.align.deviceTypes的值。<br><br>从DevEco Studio 6.0.0 Beta2版本开始支持。<br><br>说明<br><br>仅支持Stage模型。|
|ohos.dependencies.types.enable|可选|布尔值|编译时是否收集依赖的HAR模块/[源码HAR包](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-har#section197792874110)的[类型声明文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkoptions-guide#types)参与语法校验。如果HAR中配置了类型声明文件，建议开启。<br><br>- true：收集。<br>- false（缺省默认值）：不收集。<br><br>从DevEco Studio 6.0.0 Beta3版本开始支持。|
|ohos.defaults.release.cmakebuildtype|可选|字符串|在release模式下构建时，指定cmake构建类型，对所有模块生效。<br><br>- Debug：不优化代码，附加调试信息。<br>- Release（缺省默认值）：最大化优化代码，但不包含调试信息。<br>- RelWithDebInfo：近似于Release模式，既进行了代码优化，同时保留部分调试信息。<br><br>从DevEco Studio 6.0.1 Beta1版本开始支持。<br><br>说明<br><br>- 模块级build-profile.json5文件中也可以通过[arguments字段](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-exception-stack-parsing-principle#section147714466283)指定cmake构建类型，例如"arguments": "-DCMAKE_BUILD_TYPE=RelWithDebInfo"。arguments字段的优先级比ohos.defaults.release.cmakebuildtype更高。<br>- 在debug模式下构建时，该字段配置无效，默认使用Debug构建类型。|

properties字段示例：

1. {
2.   "properties": {
3.     "hvigor.cacheDir": "D://tmp",
4.     "ohos.buildDir": "D://tmp",
5.     "enableSignTask": true,
6.     "ohos.arkCompile.maxSize": 6,
7.     "hvigor.pool.cache.capacity": 2,
8.     "hvigor.pool.maxSize": 8,
9.     "ohos.pack.compressLevel": "standard",
10.     "hvigor.analyzeHtml": true,
11.     "hvigor.dependency.useNpm": false,
12.     "ohos.compile.lib.entryfile": true,
13.     "ohos.align.target": "target1",
14.     "ohos.fallback.target": ["target1", "target2"],
15.     "ohos.arkCompile.sourceMapDir": "D://MyProject",
16.     "ohos.collect.debugSymbol": false,
17.     "hvigor.enableMemoryCache": true,
18.     "hvigor.memoryThreshold": 1000,
19.     "ohos.nativeResolver": true,
20.     "ohos.arkCompile.noEmitJs": true,
21.     "ohos.arkCompile.singleFileEmit": true,
22.     "ohos.sign.har": true,
23.     "hvigor.keepDependency": false,
24.     "ohos.arkCompile.emptyBundleName": true,
25.     "ohos.align.deviceTypes": ["phone", "tablet"],
26.     "ohos.defaults.release.cmakebuildtype": "RelWithDebInfo",
27.   }
28. }
# 模块级build-profile.json5文件

更新时间: 2025-12-16 15:59

## 配置文件结构

模块级build-profile.json5文件整体的结构如下。

1. apiType
2. targets
3. └── name
4. └── runtimeOS
5. └── config
6.     └── distroFilter / distributionFilter
7.         └── apiVersion
8.             └── policy
9.             └── value
10.         └── screenShape
11.             └── policy
12.             └── value
13.         └── screenWindow
14.             └── policy
15.             └── value
16.         └── screenDensity
17.             └── policy
18.             └── value
19.         └── countryCode
20.             └── policy
21.             └── value
22.     └── deviceType
23.     └── buildOption
24.     └── atomicService
25.         └── preloads
26.             └── moduleName
27. └── source
28.     └── abilities
29.         └── name
30.         └── pages
31.         └── res
32.         └── icon
33.         └── label
34.         └── launchType
35.     └── pages
36.     └── sourceRoots
37. └── resource
38.     └── directories
39. └── output
40.     └── artifactName
41. showInServiceCenter
42. buildOption
43. buildOptionSet
44. └── name
45. └── debuggable
46. └── generateSharedTgz
47. └── copyFrom
48. └── resOptions
49.     └── compression
50.         └── media
51.             └── enable
52.         └── filters
53.             └── method
54.                 └── type
55.                 └── blocks
56.             └── files
57.                 └── path
58.                 └── size
59.                 └── resolution
60.             └── exclude
61.                 └── path
62.                 └── size
63.                 └── resolution
64.     └── resCompileThreads
65.     └── copyCodeResource
66.         └── enable
67.         └── includes
68.         └── excludes
69.     └── ignoreResourcePattern
70.     └── excludeHarRes
71.     └── includeAppScopeRes
72. └── externalNativeOptions
73.     └── path
74.     └── abiFilters
75.     └── arguments
76.     └── cppFlags
77.     └── cFlags
78.     └── targets
79. └── sourceOption
80.     └── workers
81. └── nativeLib
82.     └── filter
83.         └── excludes
84.         └── pickFirsts
85.         └── pickLasts
86.         └── enableOverride
87.         └── select
88.             └── package
89.             └── version
90.             └── includePattern
91.             └── excludePattern
92.             └── include
93.             └── exclude
94.     └── debugSymbol
95.         └── strip
96.         └── exclude
97.     └── headerPath
98.     └── collectAllLibs
99.     └── excludeFromHar
100.     └── excludeSoFromInterfaceHar
101.     └── librariesInfo
102.         └── name
103.         └── linkLibraries
104. └── napiLibFilterOption
105.     └── excludes
106.     └── pickFirsts
107.     └── pickLasts
108.     └── enableOverride
109. └── arkOptions
110.     └── runtimeOnly
111.         └── sources
112.         └── packages
113.         └── excludePackages
114.     └── types  
115.     └── obfuscation
116.         └── ruleOptions
117.             └── enable
118.             └── files
119.         └── consumerFiles
120.     └── buildProfileFields
121.     └── integratedHsp
122.     └── transformLib
123.     └── branchElimination
124.     └── byteCodeHar
125.     └── bundledDependencies
126.     └── packSourceMap
127.     └── autoLazyImport
128.     └── autoLazyFilter
129.         └── include
130.         └── exclude
131.     └── reExportCheckMode
132.     └── skipOhModulesLint
133.     └── expandImportPath
134.         └── enable
135.         └── exclude
136.     └── apPath
137.     └── hostPGO
138. └── packingOptions
139.     └── asset
140.         └── include
141.         └── exclude
142. └── removePermissions
143.     └── name
144. buildModeBinder
145. └── buildModeName
146. └── mappings
147.     └── targetName
148.     └── buildOptionName
149. entryModules

## 配置文件字段说明

下表为"Ability"类型的Module（HAP）对应的模块级build-profile.json5中配置项包含的字段，"Library"类型的Module（HAR和HSP）对应的模块级build-profile.json5中配置项为下表罗列范围的子集。

**表1** 模块级build-profile.json5文件字段说明
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|apiType|字符串|可选|API模型类型：<br><br>- stageMode：Stage模型，后续长期演进的模型，推荐使用该模型。<br>- faMode：FA模型。|
|[targets](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile#section517483765814)|对象数组|可选|定义的target，可配置多个；若配置，数组长度至少为1。|
|showInServiceCenter|布尔值|可选|是否显示在服务中心：<br><br>- true：显示。<br>- false（缺省默认值）：不显示。|
|[buildOption](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile#section1010733210421)|对象|可选|模块在构建过程中的相关配置。<br><br>其中不支持配置name、debuggable和copyFrom字段。<br><br>在FA模型中，arkOptions配置中仅支持配置types字段。|
|buildOptionSet|对象数组|可选|[表16](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile#table370712453588)buildOption的集合，其中name字段必填，每个配置都是当前支持的编译过程中所有可用工具的通用配置选项集。|
|[buildModeBinder](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile#section642017215409)|对象数组|可选|构建模式（debug、release 等）与构建配置（buildOption）的关联配置。通过该配置可以将不同的构建配置和target进行组合，并绑定到对应的构建模式上，其中构建模式需要在工程级别的构建模式列表中已定义。|
|entryModules|字符串数组|可选|Feature类型模块所关联的入口模块，仅对FA模型工程生效。|

## targets

targets用于给模块配置[多目标产物](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-customized-multi-targets-and-products)，可配置多个；若配置，数组长度至少为1。

**表2** targets
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|name|字符串|必选|target名称。|
|runtimeOS|字符串|可选|target的目标运行环境：<br><br>- HarmonyOS<br>- OpenHarmony|
|[config](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile#section1967714835919)|对象|可选|target相关配置。|
|[source](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile#section1838814817017)|对象|可选|target的源码范围。|
|[resource](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile#table2065415762214)|对象|可选|target包含的资源目录。|
|[output](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile#table965613111225)|对象|可选|定制产品生成的应用包的配置。|

**表3** resource
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|directories|字符串数组|可选|资源目录地址。|

**表4** output
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|artifactName|字符串|必选|自定义产品生成的应用包名称，可由数字、英文字母、中划线、下划线和英文句号（.）组成，支持输入版本号。|

targets字段示例：

1. "targets": [
2.   {
3.     "name": "default",
4.     "resource": {
5.       "directories": ["./src/main/resources"]
6.     },
7.     "output": {
8.       "artifactName": "customizedTargetOutputName-1.0.0"
9.     }
10.   }
11. ]

## config

config是target相关配置。

**表5** config
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|[distroFilter](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile#section113212281909)|对象|可选|应用市场分发规则。在FA模型中使用。|
|[distributionFilter](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile#section113212281909)|对象|可选|应用市场分发规则。在Stage模型中使用。|
|deviceType|字符串数组|可选|target支持的设备类型，必须在module.json5中已定义。<br><br>在FA模型中，对应的文件为config.json。|
|[buildOption](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile#section1010733210421)|对象|可选|模块在构建过程中的相关配置。<br><br>其中不支持配置name、debuggable和copyFrom字段。|
|[atomicService](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile#section106753237212)|对象|可选|元服务相关配置，仅支持在Stage模型中配置。|

## source

source用于指定target的源码范围。

**表6** source
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|[abilities](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile#section1281869320)|对象数组|可选|自定义target的能力范围。<br><br>在FA模型工程中支持对Ability源码目录下的page页面进行定制。|
|[pages](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-customized-multi-targets-and-products-guides#section73018336472)|字符串数组|可选|Stage模型工程中支持对pages源码目录的page页面进行定制，数组长度至少为1。|
|[sourceRoots](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-customized-multi-targets-and-products-guides#section18668905913)|字符串数组|可选|Stage模型工程中支持对差异化代码空间进行定制，数组长度至少为1。数组中的值有以下限制：<br><br>1. 必须唯一；<br>2. 必须为相对路径；<br>3. 类型必须为文件夹；<br>4. 文件夹必须真实存在；<br>5. 文件夹必须与src/main同级；<br><br>当数组中存在多个值时，寻址的优先级为数组中值的顺序。|

source字段示例：

1. "targets": [
2.   {
3.     "name": "default",
4.     "source": {
5.        "pages": [         // Stage模型
6.         "pages/Index"
7.       ],
8.       "abilities": [     // FA模型
9.         {
10.           "name": ".MainAbility",
11.           "pages": [
12.             "pages/index"
13.           ]
14.         }
15.       ],
16.       "sourceRoots": [
17.         "./src/default"
18.       ]
19.     }
20.   }
21. ]

## distroFilter/distributionFilter

distroFilter/distributionFilter用于指定应用市场分发规则，distroFilter在FA模型中使用，distributionFilter在Stage模型中使用。

**表7** distroFilter/distributionFilter
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|[apiVersion](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile#section10176358110)|对象|可选|支持的apiVersion范围。|
|[screenShape](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile#section1927031812114)|对象|可选|屏幕形状的支持策略。|
|[screenWindow](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile#section79432241314)|对象|可选|应用运行时窗口的分辨率支持策略。|
|[screenDensity](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile#section99812302013)|对象|可选|屏幕的像素密度支持策略。|
|[countryCode](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile#section04873351417)|对象|可选|应用需要分发的国家地区码。|

### apiVersion

**表8** apiVersion
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|policy|字符串|必选|取值规则：<br><br>- include：需要包含的value属性。<br>- exclude：需要排除的value属性。|
|value|整型数组|必选|支持的取值为API Version存在的整数值，例如10。|

### screenShape

**表9** screenShape
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|policy|字符串|必选|取值规则：<br><br>- include：需要包含的value属性。<br>- exclude：需要排除的value属性。|
|value|字符串数组|必选|支持的取值范围：<br><br>- circle：圆形<br>- rect：矩形|

### screenWindow

**表10** screenWindow
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|policy|字符串|必选|当前取值仅支持“include”。<br><br>- include：需要包含的value属性。|
|value|字符串数组|必选|单个字符串的取值格式为“宽*高”，取值为整数像素值，例如"454*454"。|

### screenDensity

**表11** screenDensity
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|policy|字符串|必选|取值规则：<br><br>- include：需要包含的value属性。<br>- exclude：需要排除的value属性。|
|value|字符串数组|必选|取值范围：<br><br>- sdpi：小规模的屏幕密度（Small-scale Dots per Inch），适用于dpi取值为(0,120]的设备。<br>- mdpi：中规模的屏幕密度（Medium-scale Dots Per Inch），适用于dpi取值为(120,160]的设备。<br>- ldpi：大规模的屏幕密度（Large-scale Dots Per Inch），适用于dpi取值为(160,240]的设备。<br>- xldpi：大规模的屏幕密度（Extra Large-scale Dots Per Inch），适用于dpi取值为(240,320]的设备。<br>- xxldpi：大规模的屏幕密度（Extra Extra Large-scale Dots Per Inch），适用于dpi取值为(320，480]的设备。<br>- xxxldpi：表示大规模的屏幕密度（Extra Extra Extra Large-scale Dots Per Inch），适用于dpi取值为(480, 640]的设备。|

### countryCode

**表12** countryCode
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|policy|字符串|必选|取值规则：<br><br>- include：需要包含的value属性。<br>- exclude：需要排除的value属性。|
|value|字符串数组|必选|国家地区码取值，具体值以ISO-3166-1标准为准。支持多个国家和地区枚举定义。|

distroFilter/distributionFilter字段示例：

1. "targets": [
2.   {
3.     "name": "default",
4.     "config": {
5.       "distributionFilter": {
6.         "apiVersion": {
7.           "policy": "include",
8.           "value": [12]
9.         },
10.         "screenShape": {
11.           "policy": "include",
12.           "value": [
13.             "circle",
14.             "rect"
15.           ]
16.         },
17.         "screenWindow": {
18.           "policy": "include",
19.           "value": [
20.             "454*454",
21.             "466*466"
22.           ]
23.         },
24.         "screenDensity": {
25.           "policy": "exclude",
26.           "value": [
27.             "ldpi",
28.             "xldpi"
29.           ]
30.         },
31.         "countryCode": {
32.           "policy": "include",
33.           "value": [
34.             "CN"
35.           ]
36.         }
37.       }
38.     },
39.   }
40. ]

## atomicService

**表13** atomicService
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|[preloads](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-customized-multi-targets-and-products-guides#section206461457101917)|对象数组|可选|定义当前模块运行时预加载的模块。|

**表14** preloads
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|moduleName|字符串|可选|预加载的模块名称。|

atomicService字段示例：

1. "targets": [
2.   {
3.     "name": "default",
4.     "config": {
5.       "atomicService": {
6.         "preloads": [
7.           {
8.             "moduleName": "preloadSharedLibrary"
9.           }
10.         ]
11.       }
12.     }
13.   }
14. ]

## abilities

abilities用于自定义target的能力范围。

**表15** abilities
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|name|字符串|必选|指定target选择的ability的名称。|
|[pages](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-customized-multi-targets-and-products-guides#section73018336472)|字符串数组|可选|FA模型中，指定target选择的ability的page。|
|res|字符串数组|可选|指定资源目录。|
|icon|字符串|可选|指定ability图标文件的索引，格式为"$media:ability_icon"。|
|label|字符串|可选|指定对用户可见的名称，要求采用该名称的资源索引，以支持多语言。|
|launchType|字符串|可选|指定ability的启动模式：<br><br>- multiton：多实例模式，每次启动创建一个新实例。<br><br>- standard：同multiton，建议使用multiton替代。<br>- singleton（缺省默认值）：单实例模式，仅第一次启动创建新实例。<br>- specified：指定实例模式，运行时由开发者决定是否创建新实例。|

abilities字段示例：

1. "targets": [
2.   {
3.     "name": "default",
4.     "source": {
5.       "abilities": [
6.         {
7.           "name": "EntryAbility",
8.           "icon": "$media:layered_image",
9.           "label": "$string:EntryAbility_label",
10.           "launchType": "singleton"
11.         }
12.       ]
13.     }
14.   }
15. ]

## buildOption

buildOption是模块在构建过程中的相关配置，buildOptionSet和targets中也支持配置buildOption。此外，工程级build-profile.json5中也支持配置buildOption。工程级别buildOption配置会与模块级别的buildOption进行合并，具体合并规则和优先级请参考[合并编译选项规则](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-compilation-options-customizing-guide#section1727865610255)。

**表16** buildOption
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|name|字符串|可选|构建配置方案buildOption的名称。|
|debuggable|布尔值|可选|当前编译产物是否为可调试模式(debug)：<br><br>- true：可调试。<br>- false：不可调试。<br><br>如果未配置debuggable字段，使用release的编译模式时，默认值为false，使用其他编译模式时，默认值为true。|
|generateSharedTgz|布尔值|可选|编译HSP模块时是否生成tgz包。<br><br>- true：生成。<br>- false：不生成。<br><br>如果未配置generateSharedTgz，根据debuggable字段决定是否生成tgz包。debuggable为true时，不生成tgz包，debuggable为false时，生成tgz包。<br><br>从DevEco Studio 5.1.1 Beta1版本开始支持。<br><br>说明<br><br>该字段配置后仅对HSP模块生效。|
|copyFrom|字符串|可选|配置已定义的buildOption的name，表示从本模块已有的buildOption复制配置。|
|[resOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile#section754823013348)|对象|可选|资源编译配置项。|
|[externalNativeOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-cpp#section0721057575)|对象|可选|Native编译配置项。|
|[sourceOption](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile#section2611239115413)|对象|可选|源码相关配置。使用不同的标签对源代码进行分类，以便在构建过程中对不同的源代码进行不同的处理。|
|[nativeLib](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-cpp#section15889929155720)|对象|可选|Native 库（.so）相关配置。|
|[napiLibFilterOption](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile#section08781111115517)|对象|可选|NAPI库（.so）文件的筛选选项。标记为废弃，不建议使用，推荐使用[nativeLib/filter](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-cpp#section15889929155720)。|
|[arkOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile#section8368152412552)|对象|可选|ArkTS编译配置。|
|[packingOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile#section1744183710558)|对象|可选|打包配置项，仅支持HAR模块。|
|[removePermissions](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile#section155111918175715)|对象数组|可选|指定编译时需要删除的依赖包中的冗余权限，模块本身的权限不会被删除，仅HAP/HSP模块支持配置。|

### resOptions

resOptions是资源编译配置项。

**表17** resOptions
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|[compression](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile#section2095319147103)|对象|可选|对工程预置图片资源进行纹理压缩的编译配置参数。|
|resCompileThreads|整型数值|可选|资源编译的线程数量 ，最小为1，最大为主机的CPU核数。<br><br>该字段从DevEco Studio 5.1.0 Release版本开始支持。|
|[copyCodeResource](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile#table1476161719356)|对象|可选|对模块的src/main/ets目录下的资源文件（非源码文件）拷贝的编译配置参数。<br><br>说明<br><br>该字段对[不开启混淆的源码HAR](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-har#section197792874110)不生效。|
|ignoreResourcePattern|字符串数组|可选|根据glob语法，对资源目录resources或开发者自定义的资源目录下的文件/文件夹名称进行过滤，匹配到的文件不会被打包到产物中。<br><br>从DevEco Studio 5.1.1 Beta1版本开始支持。<br><br>说明<br><br>- 如果规则中带有路径（例如./src/main/a.png），该规则不生效。<br>- 如果未配置该字段，打包HAP/HSP时存在默认的过滤规则：默认不打包.git、.svn、.scc、.ds_store、desktop.ini、picasa.ini、cvs、thumbs.db以及以.开头的隐藏文件/目录和以~结尾的文件。<br>- 配置该字段后，会覆盖默认的过滤规则；如果字段配置为空数组，则不应用任何过滤规则，即全部资源都打包。|
|excludeHarRes|字符串数组|可选|编译HAP/HSP模块时，指定不参与资源编译的三方HAR包的包名，配置后，依赖HAR包中的资源不会被打包到产物中，支持直接依赖和间接依赖。<br><br>从DevEco Studio 6.0.0 Beta2版本开始支持。<br><br>说明<br><br>仅支持在HAP/HSP中配置。|
|includeAppScopeRes|布尔值|可选|编译HSP时，是否将AppScope目录下的资源打包到产物中。<br><br>- true（缺省默认值）：打包。<br>- false：不打包。<br><br>从DevEco Studio 6.0.0 Beta2版本开始支持。<br><br>说明<br><br>- 该字段仅对HSP模块生效。<br>- 配置为false后，app.json5的icon和label字段不再对HSP模块生效。|

**表18** copyCodeResource
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|enable|布尔值|可选|是否将src/main/ets目录下的资源文件（.ets/.ts/.js以外的其他文件）打包到产物中。<br><br>- true（缺省默认值）：打包。<br>- false：不打包。<br><br>说明<br><br>从DevEco Studio 6.0.0 Beta2版本开始，新建工程或模块时，默认配置enable字段并且值为false，即默认不打包ets目录下的资源文件。|
|includes|字符串数组|可选|- 当enable为true时，用于指定打包的资源文件，其他资源文件均不会打包到产物中，支持glob语法，以"**/"开头。<br>- 当enable为false时，includes不生效。<br><br>从DevEco Studio 6.0.0 Beta2版本开始支持。<br><br>说明<br><br>excludes和includes互斥，只能配置一个。|
|excludes|字符串数组|可选|- 当enable为true时，用于指定不打包的资源文件，其他资源文件均会打包到产物中，支持glob语法，以"**/"开头。<br>- 当enable为false时，excludes不生效。|

注意

- 模块的src/main/ets目录下，编译时仅处理.ets/.ts/.js文件，其他文件会被当作资源文件打包进产物中，不会进行混淆或加密，如需过滤请配置excludes字段。
- 请勿将源码等文件放在以.开头的系统隐藏目录中，可能会导致过滤规则失效，会将src/main/ets目录下的所有文件作为资源文件打包进产物中，不会进行混淆或加密。

resOptions字段示例：

1. "buildOption": {
2.   "resOptions": {
3.     "resCompileThreads": 2,
4.     "copyCodeResource": {
5.       "enable": true,
6.       "excludes": ['**/entry/src/main/ets/component/big_picture.png', '**/*.yml', '**/subDir/**'],   // includes字段配置方式相同
7.     },
8.     "ignoreResourcePattern": ['*.png' ,'abc.json'],
9.     "excludeHarRes": ['har'],
10.   }
11. }

### sourceOption

sourceOption是源码相关配置，使用不同的标签对源代码进行分类，以便在构建过程中对不同的源代码进行不同的处理。

**表19** sourceOption
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|workers|字符串数组|可选|指定使用node.js工作器的JS/TS源代码，源代码在构建过程中单独处理。|

sourceOption字段示例：

1. "buildOption": {
2.   "sourceOption": {
3.     "workers": [
4.       "./src/main/ets/common/constants/CommonConstants.ets"
5.     ]
6.   }
7. }

### napiLibFilterOption

napiLibFilterOption是NAPI库（.so）文件的筛选选项，字段已废弃，不建议使用，推荐使用[nativeLib/filter](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-cpp#section15889929155720)。

**表20** napiLibFilterOption
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|excludes|字符串数组|可选|排除的.so文件。罗列的NAPI库将不会被打包。|
|pickFirsts|字符串数组|可选|按照.so文件的优先级顺序，打包最高优先级的.so文件。|
|pickLasts|字符串数组|可选|按照.so文件的优先级顺序，打包最低优先级的.so文件。|
|enableOverride|布尔值|可选|是否允许当.so文件重名冲突时，使用高优先级的.so文件覆盖低优先级的.so文件：<br><br>- true：允许。<br>- false（缺省默认值）：不允许。|

### arkOptions

arkOptions是ArkTS编译配置。

**表21** arkOptions
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|[runtimeOnly](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile#table19892123422118)|对象|可选|配置变量动态import的文件和依赖的包名，仅支持在Stage模型中配置。<br><br>runtimeOnly为非必选配置，当工程需要以变量方式动态import文件、目录的相对路径或三方包时，需要通过配置runtimeOnly来确保其加入编译流程。详情请参考[动态import变量表达式](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-dynamic-import#%E5%8A%A8%E6%80%81import%E5%8F%98%E9%87%8F%E8%A1%A8%E8%BE%BE%E5%BC%8F)。|
|[types](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkoptions-guide#types)|字符串数组|可选|自定义类型，可配置包名或d.ts/d.ets文件路径。|
|[obfuscation](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-build-obfuscation)|对象|可选|代码混淆配置。|
|[buildProfileFields](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-get-build-profile-para)|对象|可选|运行时可获取的自定义构建参数，支持键值对配置，key可由数字、英文、下划线、中划线组成，value类型仅支持string、number、boolean。|
|integratedHsp|布尔值|可选|是否为[集成态HSP](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/integrated-hsp)。<br><br>- true：是。<br>- false（缺省默认值）：否。<br><br>说明<br><br>- 从API 12开始支持。<br>- 需在工程级build-profile.json5中配置useNormalizedOHMUrl为true后使用。<br>- 该字段仅在HSP模块中配置后生效。|
|[transformLib](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/customize-bytecode-during-compilation)|字符串|可选|字节码插桩插件配置，允许开发者在编译时对字节码进行插桩修改，仅支持Stage模型，格式为相对路径，不同系统要求的文件类型如下，文件内容需要在对应平台生成，不能拷贝修改后缀名混用。<br><br>- Windows：.dll文件。<br>- Linux/Mac：.so文件。<br><br>说明<br><br>- Mac环境下添加配置后插桩未生效的问题请参考[FAQ](https://developer.huawei.com/consumer/cn/doc/harmonyos-faqs/faqs-compiling-and-building-133)。<br>- HAR模块仅字节码HAR配置生效，非字节码HAR配置不生效。|
|branchElimination|布尔值|可选|是否启用代码分支裁剪，减少编译产物大小，开启后，在release编译模式下，不会被执行到的代码分支会被裁剪掉，示例请参考[branchElimination示例](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile#li71611425123512)。<br><br>- true：启用（将导致使用"ApplyChanges"功能时，对const声明的常量的值进行的修改可能不生效）。<br>- false（缺省默认值）：不启用。<br><br>说明<br><br>- 仅支持API 11及以上的Stage模型。<br>- HAR模块仅字节码HAR配置生效，非字节码HAR配置不生效。<br>- 仅支持const声明的bool类型常量和const声明的string/number类型常量的判断表达式。<br>- 不支持间接导入，例如A文件中定义const变量A1，B文件导入A1，导出B1，ets导入B1进行判断，无法进行裁剪。|
|byteCodeHar|布尔值|可选|是否构建字节码HAR，仅在HAR模块中配置后生效。详情请参考[构建字节码HAR](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-har#section16598338112415)。<br><br>- true：支持。<br>- false：不支持。<br><br>说明<br><br>- 从API 12开始支持。<br>- 从DevEco Studio NEXT Beta1（5.0.3.800）版本开始，当工程级build-profile.json5中useNormalizedOHMUrl配置为true时，byteCodeHar缺省默认值为true；当useNormalizedOHMUrl配置为false时，byteCodeHar缺省默认值为false。|
|bundledDependencies|布尔值|可选|是否支持将多个源码HAR（本地+远程）打包成一个字节码HAR。字节码HAR、HSP、npm不会被打包进去，仅会合并源码HAR。<br><br>- true：支持。<br>- false（缺省默认值）：不支持。<br><br>说明<br><br>- 仅支持[字节码HAR](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-har#section16598338112415)配置该字段。<br>- 从API 12开始支持。<br>- 仅支持Stage模型。|
|packSourceMap|布尔值|可选|编译[字节码HAR](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-har#section16598338112415)时，是否将sourceMap文件打包到产物中。仅HAR模块支持配置，并且只对字节码HAR生效。<br><br>- true：打包。<br>- false：不打包。<br><br>该字段从DevEco Studio 5.1.0 Release版本开始支持。<br><br>说明<br><br>- 如果不配置，debug模式默认值为true，release模式默认值为false。<br>- 将sourceMap打包到release的HAR包中，可能会导致HAR中的代码资产泄漏。|
|autoLazyImport|布尔值|可选|编译时是否自动将符合lazy-import语法规范的import语句添加"lazy"关键字。仅支持在源码中添加"lazy"关键字，不包含依赖的字节码HAR包或HSP。关于lazy-import的介绍及相关影响请参考[延迟加载（lazy import）](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-lazy-import)。<br><br>- true：添加。<br>- false（缺省默认值）：不添加。<br><br>说明<br><br>- 如果配置为true，编译时不会做场景识别，即源码中任何符合语法规范的import语句都会被添加"lazy"。<br>- 仅支持Stage模型。|
|[autoLazyFilter](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile#table1551310818378)|对象|可选|自定义添加"lazy"关键字的模块，仅当autoLazyImport为true时生效。<br><br>从DevEco Studio 6.0.1 Beta1版本开始支持。|
|reExportCheckMode|字符串|可选|针对以下场景，编译时是否进行拦截报错：使用lazy import导入的变量，在同文件中被再次导出。<br><br>- noCheck（缺省默认值）：不检查，不报错。<br>- compatible：兼容模式，报Warning。<br>- strict：严格模式，报Error。<br><br>该字段从DevEco Studio 5.0.5 Release版本开始支持。|
|skipOhModulesLint|布尔值|可选|是否跳过工程中oh_modules目录的[ArkTS规则检查](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/typescript-to-arkts-migration-guide)。从DevEco Studio 6.0.0 Beta1版本开始支持。<br><br>- true：跳过。<br>- false（缺省默认值）：不跳过。|
|[expandImportPath](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile#table1921576135914)|对象|可选|import路径展开相关配置选项。<br><br>从DevEco Studio 6.0.0 Beta3版本开始支持。<br><br>说明<br><br>HAR模块不支持配置。|
|apPath|字符串|可选|说明<br><br>API 11及以上版本不再支持，即该字段配置后不再生效。<br><br>应用热点信息文件路径。|
|hostPGO|布尔值|可选|是否启用配置文件引导优化功能：<br><br>- true：启用。<br>- false（缺省默认值）：不启用。<br><br>从API 10开始废弃。|

- branchElimination字段配置为true时，代码分支的裁剪情况示例如下：
    
    1. # 编译生成的BuildProfile文件
    2. export const DEBUG = false;
    3. export const VERSION_CODE = 100;
    4. # 开发者自定义的ets文件
    5. import { DEBUG } from 'BuildProfile';
    6. import { VERSION_CODE } from 'BuildProfile';
    7. if (DEBUG)
    8.   {XXX} // 该分支会被裁剪掉
    9. else
    10.   {XXX}
    11. if (VERSION_CODE){XXX} // 该语法发生了类型转换，不支持代码裁剪。
    12. if (VERSION_CODE === 100){XXX} // 若需要裁剪代码，使用该方式，显式指定判断条件为boolean类型。
    

**表22** runtimeOnly
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|sources|字符串数组|可选|配置变量动态import的文件/文件夹的相对路径。<br><br>配置的文件/文件夹必须在工程中真实存在，且文件的后缀只能为ets或ts。|
|packages|字符串数组|可选|配置变量动态import依赖的包名。<br><br>该包名需要和工程级/模块级oh-package.json5的dependencies或dynamicDependencies中的名字保持一致。<br><br>从DevEco Studio 5.1.1 Beta1版本开始，packages中的三方包支持配置在dynamicDependencies中。|
|excludePackages|字符串数组|可选|编译HAP/HSP模块时，指定不参与变量动态import的源码HAR的包名，配置的源码HAR不会参与编译，支持直接/间接依赖。<br><br>仅支持在HAP/HSP模块中配置。<br><br>从DevEco Studio 6.0.0 Beta2版本开始支持。|

**表23** expandImportPath
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|enable|布尔值|可选|是否启用import路径展开，启用后可以提升应用的运行时性能。关于import路径展开的原理及开启后的副作用请参考[通过import路径展开优化性能](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-module-side-effects#%E9%80%9A%E8%BF%87import%E8%B7%AF%E5%BE%84%E5%B1%95%E5%BC%80%E4%BC%98%E5%8C%96%E6%80%A7%E8%83%BD)。<br><br>- true：启用。<br>- false（缺省默认值）：不启用。<br><br>说明<br><br>import XXX from 'A'，A必须为本地HAR模块，并且仅当A为包名时支持进行展开，A为相对路径或包名+路径都不支持展开。|
|exclude|字符串数组|可选|配置oh-package.json5中的依赖别名，用于指定不展开import语句的依赖，仅支持本地HAR模块。|

**表24** autoLazyFilter
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|include|字符串数组|可选|- 当autoLazyImport为true时，指定自动添加"lazy"关键字的包名（即oh-package.json5中的name），其他包不会添加"lazy"关键字，支持正则语法。<br>- 当autoLazyImport为false时，include不生效。<br><br>说明<br><br>- include和exclude互斥，只能配置一个。<br>- include不支持配置空数组或空字符串，至少配置一个包名，并且包名不能重复。|
|exclude|字符串数组|可选|- 当autoLazyImport为true时，指定不添加"lazy"关键字的包名，其他包都会添加"lazy"关键字，支持正则语法。<br>- 当autoLazyImport为false时，exclude不生效。<br><br>说明<br><br>- include和exclude互斥，只能配置一个。<br>- exclude不支持配置空数组或空字符串，至少配置一个包名，并且包名不能重复。|

arkOptions字段示例：

1. "buildOption": {
2.   "arkOptions": {
3.     "runtimeOnly": {
4.       "sources": ["./src/main/ets/utils/Calc.ets"],
5.       "packages": ["myHar"],
6.       "excludePackages": ["har1","har2"],  // myHar依赖har1、har2
7.     },
8.     "buildProfileFields": {
9.       "buildOptionSetData": "BuildOptionSetDataRelease",
10.       "data": "DataRelease"
11.     },
12.     "transformLib": "./dll/example.dll",
13.     "branchElimination": true,
14.     "autoLazyImport": true,
15.     "autoLazyFilter": {
16.       "include": ['entry']
17.     },
18.     "reExportCheckMode": "compatible",
19.     "expandImportPath": {
20.       "enable": true,
21.       "exclude": ['localhar']
22.     },
23.   }
24. }

### packingOptions

packingOptions是打包配置项，仅支持HAR模块。该字段从DevEco Studio 5.1.0 Release版本开始支持。

**表25** packingOptions
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|[asset](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile#table14927147191119)|对象|可选|打包资产配置项。|

**表26** asset
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|include|字符串数组|可选|配置打包到HAR产物中的文件，遵循glob语法。<br><br>说明<br><br>- 以下目录配置后不生效，即不会被打包到产物中：node_modules、oh_modules、.preview、build、.cxx、.test。<br><br>- 配置include字段后，构建源码HAR时，.gitignore和.ohpmignore文件不生效，详细请参考[以debug模式构建](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-har#section197792874110)。|
|exclude|字符串数组|可选|配置不打包到HAR产物中的文件，遵循glob语法。<br><br>说明<br><br>- 以下文件配置后不生效，默认会打包：oh-package.json5。<br>- 配置exclude字段后，构建源码HAR时，.gitignore和.ohpmignore文件不生效，详细请参考[以debug模式构建](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-har#section197792874110)。|

packingOptions字段示例：

1. "buildOption": {
2.   "packingOptions": {
3.     "asset": {
4.       "include": ["./src/router.json5", "router.json5"],
5.       "exclude": ["./config/*"]
6.     }
7.   }
8. }

### removePermissions

removePermissions是一个对象数组，用于编译HAP/HSP模块时，指定需要删除的依赖包中的冗余权限，模块本身的权限不会被删除。

**表27** removePermissions
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|name|字符串|必选|待删除的权限名称，需要包含在依赖包的module.json的requestPermissions中。|

removePermissions字段示例：

1. "buildOption": {
2.   "removePermissions": [
3.     {
4.       "name": "ohos.permission.ABILITY_BACKGROUND_COMMUNICATION"
5.     },
6.     {
7.       "name": "ohos.permission.ACCELEROMETER"
8.     }
9.   ]
10. }

## compression

compression是对工程预置图片资源进行纹理压缩的编译配置参数。

**表28** compression
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|[media](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile#section1915545641714)|对象|可选|对资源目录下media目录的图片进行纹理压缩的配置参数。|
|[filters](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile#section185719543186)|对象数组|可选|文件过滤配置参数。<br><br>说明<br><br>编译过程中会依次遍历图片文件，并与filters条件进行匹配，一旦匹配成功，则完成该图片的处理。当工程级和模块级同时配置时，先按照模块级的过滤条件匹配，一旦匹配成功，则忽略工程级的过滤条件；如果模块级的没有匹配成功，继续按工程级的条件进行匹配。|

### media

media是对资源目录下media目录的图片进行纹理压缩的配置参数。

**表29** media
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|enable|布尔值|可选|是否对media图片启用纹理压缩。<br><br>- true：启用。<br>- false（缺省默认值）：不启用。<br><br>说明<br><br>- 在linux系统的构建场景下，请确认系统环境已[安装libGL1库](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-command-line-building-app#section1478651816216)。<br>- 对图片进行纹理压缩会改变文件名称和内容，在[分层图标](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arkui-drawabledescriptor#layereddrawabledescriptor)以及二次编辑的场景下会引起图片显示异常，请进一步使用filters排除掉这部分文件。|

### filters

filters是文件过滤配置参数。

**表30** filters
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|[method](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile#table1568916396220)|对象|必选|纹理压缩的方式。|
|[files](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile#table19762944112414)|对象|可选|指定用来参与压缩的文件，与exclude字段配合使用。|
|[exclude](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile#table6219104952519)|对象|可选|从files中剔除掉不需要压缩的文件。|

**表31** method
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|type|字符串|必选|转换类型。<br><br>- astc（Adaptive Scalable Texture Compression）：自适应可变纹理压缩，一种对GPU友好的纹理格式，可在设备侧更快地显示，有更少的内存占用。<br>- sut（SUper compression for Texture） ：纹理超压缩，可在设备侧更快地显示，有更少的内存占用，相比astc具备更大压缩率和更少ROM占用。|
|blocks|字符串|必选|astc/sut转换类型的扩展参数，决定画质和压缩率，当前仅支持"4x4"。|

**表32** files
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|path|字符串数组|可选|指定“按路径匹配”的过滤条件，符合glob规范，格式为相对路径。|
|size|二维数组|可选|指定“按大小匹配”的过滤条件，格式为[min,max]，闭区间，表示大小从min到max之间的文件。<br><br>- 每个数值可以填数字、字符串或字符串中带单位（大小写均可），如[0, '1k']。<br>- 单位K/k=1024，M/m=1024*1024，G/g=1024*1024*1024。<br>- 区间最大值可省略，表示无限大，如['3K']。|
|resolution|二维数组|可选|指定“按分辨率匹配”的过滤条件，配置示例：<br><br>1. resolution:[<br>2.   [<br>3.     { width:32, height:32 },  // 最小宽高<br>4.     { width:64, height:64 },  // 最大宽高<br>5.   ],  // 分辨率在32*32到64*64之间的图片<br>6.   [<br>7.     { width:200, height:200 },  // 最小宽高<br>8.     // 此处第2个不填表示最大宽高是无限大<br>9.   ],  // 分辨率大于200*200的图片<br>10. ]<br><br>- width和height只能是数字。<br>- 最大宽高可以省略，表示无限大。|

**表33** exclude
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|path|字符串数组|可选|同files/path。|
|size|二维数组|可选|同files/size。|
|resolution|二维数组|可选|同files/resolution。|

compression字段示例：

1. "buildOption": {
2.   "resOptions": {
3.     "compression": {
4.       "media": {
5.         "enable": true // 是否对media图片启用纹理压缩
6.       },
7.       // 纹理压缩文件过滤，非必填，不填会压缩资源目录中的所有图片
8.       "filters": [
9.         {
10.           "method": {
11.             "type": "sut", // 转换类型
12.             "blocks": "4x4" // 转换类型的扩展参数
13.           },
14.           // 指定用来参与压缩的文件，需要满足所有条件且不被exclude过滤的文件才会参与压缩
15.           "files": {
16.             "path": ["./**/*"], // 指定资源目录中的所有文件
17.             "size": [[0, '10k']], // 指定大小10k以下的文件
18.             // 指定分辨率小于2048*2048的图片
19.             "resolution": [
20.               [
21.                 { "width": 0, "height": 0 }, // 最小宽高
22.                 { "width": 2048, "height": 2048 } // 最大宽高
23.               ]
24.             ]
25.           },
26.           // 从files中剔除掉不需要压缩的文件，需要满足所有过滤条件的文件才会被剔除
27.           "exclude": {
28.             "path": ["./**/*.jpg"], // 过滤所有jpg文件
29.             "size": [[0, '1k']], // 过滤大小1k以下的文件
30.             // 过滤分辨率小于1024*1024的图片
31.             "resolution": [
32.               [
33.                 { "width": 0, "height": 0 }, // 最小宽高
34.                 { "width": 1024, "height": 1024 } // 最大宽高
35.               ]
36.             ]
37.           }
38.         }
39.       ]
40.     }
41.   }
42. }

## buildModeBinder

buildModeBinder是构建模式（debug、release 等）与构建配置（buildOption）的关联配置。通过该配置可以将不同的构建配置和target进行组合，并绑定到对应的构建模式上。如果没有配置buildModeBinder，默认的绑定策略请参考[合并编译选项规则](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-compilation-options-customizing-guide#section1727865610255)。

**表34** buildModeBinder
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|buildModeName|字符串|可选|构建模式名称，需要在工程级别的buildModeSet中定义。|
|[mappings](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile#table4672142011561)|对象数组|可选|target和buildOption之间的一对一映射关系。|

**表35** mappings
|字段名称|类型|可选/必选|含义|
|:--|:--|:--|:--|
|targetName|字符串|可选|target名称。|
|buildOptionName|字符串|可选|构建配置buildOption名称。|

buildModeBinder字段示例：

1. "buildModeBinder": [
2.   {
3.     "buildModeName": "debug",
4.     "mappings": [
5.       {
6.         "targetName": "default",
7.         "buildOptionName": "release"
8.       }
9.     ]
10.   }
11. ]
# 多模块管理

更新时间: 2025-12-16 15:59

模块是应用/元服务的基本功能单元，包含了源代码、资源文件、第三方库及应用/元服务配置文件，Hvigor支持工程多模块管理。您可在工程下的build-profile.json5配置文件中增加对应模块信息，即可对模块进行工程绑定和管理，或在hvigorconfig.ts脚本中动态添加或排除某个模块。同时也支持分模块配置、编译和打包。

## 多模块配置

### 静态配置模块

工程级build-profile.json5配置文件中"modules"字段，用于记录工程下的模块信息，主要包含模块名称、模块的源码路径以及模块的 target 信息。target信息主要用于定制多目标构建产物，更多详细信息可参考[配置多目标产物](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-customized-multi-targets-and-products)章节。

例如以下目录中存在两个模块目录，您可在工程下的build-profile.json5配置文件，添加模块信息，使得模块与工程进行绑定：

1. 工程结构
2. └─ .hvigor目录    // 构建项目的缓存文件目录，不需要开发者改动，可以删除
3. └─ module1
4.    └─ 模块源码文件
5.    └─ build-profile.json5    // 模块级别的构建静态配置文件，主要用于定义当前模块的构建信息、hap(hsp、har)的构建行为等
6.    └─ hvigorfile.ts    // 模块级别的构建动态自定义脚本，主要用于定义和扩展hap(hsp、har)的构建流程
7.    └─ 其他配置文件
8. └─ module2
9. └─ hvigor目录
10.    └─ hvigor-config.json5    // 构建引擎的配置文件，主要用于定义开发态版本号、依赖插件的版本以及Hvigor相关能力的配置等
11. └─ build-profile.json5    // 工程级别的构建静态配置文件，主要用于定义整个项目的模块信息、应用信息、app的构建行为等
12. └─ hvigorfile.ts    // 工程级别的构建动态自定义脚本，主要用于定义和扩展app的构建流程
13. └─ 其他配置文件

其他配置文件：

- oh-package.json5：应用的三方包依赖配置文件。
- local.properties: 应用本地环境配置文件。
- obfuscation-rules.txt: 应用模块的混淆规则配置文件。
- consumer-rules.txt: HAR/HSP模块默认导出的混淆规则文件，会打包到HAR包中。

工程下的build-profile.json5文件中模块配置示例：

1. {
2.   "modules": [
3.     {
4.       "name": "module1", // 模块的名称。该名称需与module.json5文件中的module.name保持一致。在FA模型中，对应的文件为config.json。
5.       "srcPath": "./module1" // 模块的源码路径，为模块根目录相对工程根目录的相对路径
6.     },
7.     {
8.       "name": "module2",
9.       "srcPath": "./module2"
10.     }
11.   ]
12. }

### 动态配置模块

Hvigor支持在[hvigorconfig.ts脚本](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-life-cycle#section810245135914)中动态添加或排除某个模块，具体API及示例可参考[HvigorConfig](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-api#section7253174081515)。

## 分模块编译

Hvigor支持分模块编译和打包。您可以通过以下两种方式进行分模块构建：

- 在DevEco Studio中，选中需构建的模块目录后，点击Build菜单栏下的"Make module 'module1'"，其中"module1"根据具体工程模块名称显示；
- 在DevEco Studio的Terminal中，指定模块进行编译。比如模块名称为entry，目标产物target为default，构建HAP模块，可执行以下命令：
    
    1. hvigorw --mode module -p product=default -p module=entry@default assembleHap
    

更多构建HAR/HSP包命令，可参考[命令行工具](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-commandline#section9580122622012)章节。
# 添加依赖项

更新时间: 2025-12-16 15:59

应用/元服务支持通过包管理工具ohpm来安装、共享、分发代码，管理项目的依赖关系。本文介绍了在您的项目中如何配置依赖项，以及不同的配置方式在编译期间的处理逻辑和编译结果。

您可在工程或模块下的oh-package.json5文件中的dependencies（生产依赖）/devDependencies（开发依赖）字段中指定依赖项，以上两种依赖字段均支持引用远程三方包、本地模块和本地HAR/HSP三种方式。oh-package.json5文件中的dynamicDependencies（动态依赖）仅限于动态依赖HSP的使用场景。以下配置以dependencies为例，更多关于依赖的设置方式请参考[oh-package.json5](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-oh-package-json5)。

## 配置依赖项

### 远程三方包

在需要引入三方包的模块的oh-package.json5文件中设置三方包依赖，配置示例如下：

1. "dependencies": {
2.   "@ohos/lottie": "^2.0.0"
3. }

### 本地模块

在模块的oh-package.json5文件中设置本地模块依赖，有两种方式：

- 配置本地文件夹路径，示例如下：
    
    1. "dependencies": {
    2.   "folder": "file:../folder"
    3. }
    
- 配置本地模块名，例如依赖本地模块moduleA（从DevEco Studio 6.0.0 Beta1版本开始支持）：
    
    1. "dependencies": {
    2.   "moduleA": "@module:moduleA"
    3. }
    

### 本地HAR/HSP包

- 引用HAR：
    
    1. "dependencies": {
    2.   "package": "file:../package.har"
    3. }
    

- 引用HSP（在release模式下，构建HSP会生成tgz包）：
    
    1. "dependencies": {
    2.   "package": "file:../package.tgz"
    3. }
    

依赖设置完成后，需要执行**ohpm install**命令安装依赖包，依赖包会存储在对应模块的oh_modules目录下。

## 编译行为差异说明

根据当前的依赖配置规格，您可以在以下字段中指定依赖项：

- 工程级oh-package.json5文件中的dependencies、dynamicDependencies、devDependencies
- 模块级oh-package.json5文件中的dependencies、dynamicDependencies、devDependencies

虽然以上字段都可以指定依赖项，但使用不同的字段，在编译期间的处理逻辑和编译结果是不同的。举个例子：

1. 新建工程，新建HAR模块。
2. 在entry模块级oh-package.json5的dependencies设置HAR本地文件夹，编译entry：
    
    1. "dependencies": {
    2.   "har": "file:../har"
    3. }
    
3. 在entry模块级oh-package.json5的devDependencies设置HAR本地文件夹，编译entry：
    
    1. "devDependencies": {
    2.   "har": "file:../har"
    3. }
    

对比步骤2和3的构建日志，您会发现，步骤2会打印HAR相关的日志，如下图红框所示，步骤3并没有任何关于HAR的日志打印。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155915.49727813581682687398472461049691:50001231000000:2800:14CC23A07678F90EB22C71E141B7DC54E9C5360CEC03058F67C2B7FC2910817D.png)

以上仅仅是日志的差异，为了确保编译正常，不建议将依赖项配置在工程级oh-package.json5中，下文将通过表格说明编译时具体的处理逻辑和可能造成的异常结果。

为方便后续说明，需要了解以下名词，仅在本文内有效：

- 三方包依赖：通过[远程三方包](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-dependencies#section0999112011818)和[本地HAR/HSP包](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-dependencies#section636814917176)的方式指定依赖项
- 本地依赖：通过[本地模块](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-dependencies#section91117398178)的方式指定依赖项
- 开启bundledDependencies的字节码HAR：字节码HAR的build-profile.json5的buildOption/arkOptions下的bundledDependencies字段配置为true
- 依赖项的自身配置：依赖项自身的resources/workers/runtimeOnly/UIAbilities/ExtensionAbilities/C++编译产物/路由表等

说明

- 下表的devDependencies指工程级和模块级oh-package.json5中的devDependencies。
- 下表仅对可能导致编译异常的场景进行说明，其他编译正常的场景不进行说明，例如在模块级oh-package.json5中配置dependencies。

**表1** 编译行为差异说明
|依赖项|   |   |编译HAP|编译HSP|编译未开启 bundledDependencies 的字节码HAR|编译开启 bundledDependencies 的字节码HAR|
|:--|:--|:--|:--|:--|:--|:--|
|源码HAR|三方包依赖|devDependencies|1|1|**2**|1|
|工程级的dependencies|/|/|**3**|**3**|
|本地依赖|devDependencies|1|1|**2**|1|
|工程级的dependencies|/|1|**2**|1|
|字节码HAR|三方包依赖|devDependencies|**2**|**2**|**2**|**2**|
|工程级的dependencies|/|/|**3**|**3**|
|HSP|三方包依赖|devDependencies|1|1|**2**|**1**|
|工程级的dependencies、dynamicDependencies|/|/|/|/|
|本地依赖|devDependencies|**1**|**1**|**2**|**1**|
|工程级的dependencies、dynamicDependencies|/|1|**2**|**1**|

表格中各符号的含义如下：

- 1：依赖项仅代码文件（ets/ts/js等）参与编译，依赖项的自身配置不会参与收集，可能造成编译/运行时异常。
- 2：依赖项没有被收集，会导致编译异常。
- 3：编译正常，后续集成时可能会造成运行时异常。
- /：编译和运行都正常。

针对以上几类编译/运行时可能异常的场景，从DevEco Studio 5.1.1 Beta1版本开始，hvigor-config.json5文件提供一个字段ohos.byteCodeHar.integratedOptimization，开启后，可以优化表格中**加粗符号**对应的场景。

但该开关只是优化了依赖收集的逻辑，并没有优化依赖项的自身配置收集的逻辑，因此，加粗符号对应的场景中，只有编译字节码HAR，并且依赖配置在工程级的dependencies或dynamicDependencies对应的场景才能完全优化，其他场景无法保证编译/运行时无异常。

1. "properties": {
2.   "ohos.byteCodeHar.integratedOptimization": true
3. }

说明

依赖包提供方和集成方都需要配置该字段。

综上所述，我们建议您：

- 当前模块使用到的依赖配置在本模块的oh-package.json5中。
- 除辅助语法检查TypeScript的类型声明包（如：@types/commonmark）外，其他类型的依赖项，都不要配置在devDependencies中。