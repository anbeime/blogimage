## 配置文件结构
[[如何在鸿蒙系统使用 ArkUI]]
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
# 动态生成编译构建产物Hap和App的名称

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