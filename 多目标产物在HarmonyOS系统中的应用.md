# 能力说明

更新时间: 2025-12-16 15:59

通常情况下，应用厂商会根据不同的部署环境，不同的目标人群，不同的运行环境等，将同一个应用定制为不同的版本，如国内版、国际版、普通版、VIP版、免费版、付费版等。针对以上场景，DevEco Studio支持通过少量的代码配置以实例化不同的差异版本，在编译构建过程中实现一个应用构建出不同的目标产物版本，从而实现源代码、资源文件等的高效复用。

在了解HarmonyOS应用的多目标构建产物如何定制前，先了解target和product的概念：

- 工程内的每一个Entry/Feature模块，对应的构建产物为HAP，HAP是应用/元服务可以独立运行在设备中的形态。由于在不同的业务场景中，同一个模块可能需要定制不同的功能或资源，因此引入target的概念。一个模块可以定义多个target，每个target对应一个定制的HAP，通过配置可以实现一个模块构建出不同的HAP。
- 一个HarmonyOS工程的构建产物为APP包，APP包用于应用/元服务发布上架应用市场。由于不同的业务场景，需要定制不同的应用包，因此引入product概念。一个工程可以定义多个product，每个product对应一个定制化应用包，通过配置可以实现一个工程构建出多个不同的应用包。

更多关于多目标产物的实践请参考[多目标产物构建开发实践](https://developer.huawei.com/consumer/cn/doc/best-practices/bpta-multi-target)。

## 定制HAP多目标构建产物

每一个Entry/Feature模块均支持定制不同的target，通过在模块中的build-profile.json5文件中实现差异化定制，当前支持HAP包名、设备类型（deviceType）、源码集（source）、资源（resource）、buildOption配置项（如C++依赖的.so、混淆配置、abi类型、cppFlags等）、分发规则（distributionFilter）的定制。

**定义目标产物target**

每一个target对应一个定制的HAP，因此，在定制HAP多目标构建产物前，应提前规划好需要定制的target名称。例如，以ArkTS Stage模型为例，定义一个免费版和付费版，模块级build-profile.json5文件示例如下：

1. { 
2.   "apiType": 'stageMode', 
3.   "buildOption": {   
4.   }, 
5.   "targets": [  //定义不同的target 
6.     { 
7.       "name": "default",  //默认target名称default 
8.     }, 
9.     { 
10.       "name": "free",  //免费版target名称 
11.     }, 
12.     { 
13.       "name": "pay",  //付费版target名称 
14.     } 
15.   ] 
16. }

按照上述target的定义，在编译构建时，会同时打包生成default、free和pay三个不同的HAP。

### 定义产物的HAP包名

每一个target均可以指定产物命名。

1. { 
2.   "apiType": "stageMode", 
3.   "buildOption": { 
4.   }, 
5.   "targets": [ 
6.     { 
7.       "name": "default", 
8.       "output": { 
9.         "artifactName": "customizedTargetOutputName-1.0.0"  //产物名称为customizedTargetOutputName-1.0.0
10.       } 
11.     }, 
12.     { 
13.       "name": "free", 
14.       "output": { 
15.         "artifactName": "customizedTargetOutputName1-1.0.0"  //产物名称为customizedTargetOutputName1-1.0.0
16.       } 
17.     }, 
18.     { 
19.       "name": "pay", 
20.       "output": { 
21.         "artifactName": "customizedTargetOutputName2-1.0.0"  //产物名称为customizedTargetOutputName2-1.0.0
22.       } 
23.     } 
24.   ] 
25. }

如果已配置签名，target产物对应的HAP包名为开发者定制的名称；如果未配置签名，target产物对应的HAP包名为开发者定制的名称+unsigned。

### 定义产物的deviceType

每一个target均可以指定支持的设备类型deviceType，也可以不定义。如果不定义，则该target默认支持module.json5/[config.json](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/application-configuration-file-overview-fa)中定义的设备类型。

同时，在定义每个target的deviceType时，支持的设备类型必须在module.json5或config.json中已经定义。例如，在上述定义的3个target中，分别定义default默认支持所有设备类型，free和pay版本只支持phone设备。

1. { 
2.   "apiType": 'stageMode', 
3.   "buildOption": { 
4.   }, 
5.   "targets": [ 
6.     { 
7.       "name": "default",  //未定义deviceType，默认支持config.json或module.json5中定义的设备类型 

8.     }, 
9.     { 
10.       "name": "free", 
11.       "config": { 
12.         "deviceType": [  //定义free支持的设备类型为phone 
13.           "phone" 
14.         ] 
15.       } 
16.     }, 
17.     { 
18.       "name": "pay", 
19.       "config": { 
20.         "deviceType": [  //定义pay支持的设备类型为phone 
21.           "phone" 
22.         ] 
23.       } 
24.     } 
25.   ] 
26. }

### 定义产物的distributionFilter

在未定义target的分发规则distributionFilter时，以module配置[distributionFilter](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#distributionfilter%E6%A0%87%E7%AD%BE)/[distroFilter](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-structure#distrofilter%E5%AF%B9%E8%B1%A1%E7%9A%84%E5%86%85%E9%83%A8%E7%BB%93%E6%9E%84)分发规则为准。

针对多target存在相同设备类型deviceType的场景，相同设备类型的target需要指定分发规则distributionFilter。

如果是FA工程，请将distributionFilter字段替换为distroFilter。

1. { 
2.   "apiType": "stageMode", 
3.   "buildOption": { 
4.   }, 
5.   "targets": [ 
6.     { 
7.       "name": "default", 

8.     }, 
9.     { 
10.       "name": "free", 
11.       "config": { 
12.         "distributionFilter": {  // 具体请参考distributionFilter标签
13.           "screenShape": { // 屏幕形状枚举 
14.             "policy": "include", 
15.             "value": ["circle"] 
16.           } 
17.         } 
18.       } 
19.     }, 
20.     { 
21.       "name": "pay", 
22.       "config": { 
23.         "distributionFilter": { 
24.           "screenShape": { 
25.             "policy": "include", 
26.             "value": ["rect"] 
27.           } 
28.         } 
29.       } 
30.     } 
31.   ] 
32. }

### 定义产物preloads的分包

对于元服务，每一个target均可以指定preloads的分包，也可以不定义。如果不定义，则以module.json5中的配置为准。

1. { 
2.   "apiType": 'stageMode', 
3.   "showInServiceCenter": true, 
4.   "buildOption": { 
5.   }, 
6.   "targets": [   
7.     { 
8.       "name": "default",   
9.     },
10.     { 
11.       "name": "free",   
12.     },
13.     { 
14.       "name": "pay",   
15.       "config": { 
16.         "atomicService": { 
17.           "preloads": [  //指定preloads的分包 
18.             { 
19.               "moduleName": "preloadSharedLibrary"
20.             } 
21.           ] 
22.         } 
23.       } 
24.     } 
25.   ] 
26. }

### 定义产物的source源码集-pages

对于source源码集的定制，由于Stage模型和FA模型的差异，Stage模型支持对pages源码目录的page页面进行定制，FA模型则支持对Ability源码目录下的page页面进行定制。

- 例如，Stage模型中的工程，在模块的pages目录下分别定义了Index.ets、Page1.ets和Page2.ets三个页面。其中default使用了Index.ets页面；free使用了Index.ets和Page1.ets页面；pay使用了Index.ets和Page2.ets页面，则示例代码如下所示：
    
    1. { 
    2.    "apiType": 'stageMode', 
    3.    "buildOption": { 
    4.    }, 
    5.    "targets": [ 
    6.      { 
    7.        "name": "default", 
    8.        "source": {  //定义Stage模型中默认版target的pages源码文件
    9.          "pages": [ 
    10.            "pages/Index" 
    11.          ] 
    12.        } 
    13.      }, 
    14.      { 
    15.        "name": "free", 
    16.        "config": { 
    17.          "deviceType": [ 
    18.            "phone" 
    19.          ] 
    20.        }, 
    21.        "source": {  //定义Stage模型中免费版target的pages源码文件
    22.          "pages": [ 
    23.            "pages/Index", 
    24.            "pages/Page1" 
    25.          ] 
    26.        } 
    27.      }, 
    28.      { 
    29.        "name": "pay", 
    30.        "config": { 
    31.          "deviceType": [ 
    32.            "phone" 
    33.          ] 
    34.        }, 
    35.        "source": {  //定义Stage模型中付费版target的pages源码文件
    36.          "pages": [ 
    37.            "pages/Index", 
    38.            "pages/Page2" 
    39.          ] 
    40.        } 
    41.      } 
    42.    ] 
    43.  }
    

- 例如，FA模型中的工程，在模块的MainAbility中定义了index.ets、page1.ets和page2.ets，其中：default使用了index.ets 页面；free使用了index.ets和page1.ets页面；pay使用了index.ets和page2.ets页面。
    
    1. { 
    2.    "apiType": 'faMode', 
    3.    "buildOption": { 
    4.    }, 
    5.    "targets": [ 
    6.      { 
    7.        "name": "default", 
    8.        "source": {  //定义FA模型中默认版target的pages源码文件
    9.          "abilities": [ 
    10.            { 
    11.              "name": ".MainAbility", 
    12.              "pages": [ 
    13.                "pages/index" 
    14.              ] 
    15.            } 
    16.          ], 
    17.        } 
    18.      }, 
    19.      { 
    20.        "name": "free", 
    21.        "config": { 
    22.          "deviceType": [ 
    23.            "phone" 
    24.          ] 
    25.        }, 
    26.        "source": {  //定义FA模型中免费版target的pages源码文件
    27.          "abilities": [ 
    28.            { 
    29.              "name": ".MainAbility", 
    30.              "pages": [ 
    31.                "pages/index", 
    32.                "pages/page1" 
    33.              ] 
    34.            } 
    35.          ], 
    36.        } 
    37.      }, 
    38.      { 
    39.        "name": "pay", 
    40.        "config": { 
    41.          "deviceType": [ 
    42.            "phone" 
    43.          ] 
    44.        }, 
    45.        "source": {  //定义FA模型中付费版target的pages源码文件
    46.          "abilities": [ 
    47.            { 
    48.              "name": ".MainAbility", 
    49.              "pages": [ 
    50.                "pages/index", 
    51.                "pages/page2" 
    52.              ] 
    53.            } 
    54.          ], 
    55.        } 
    56.      } 
    57.    ] 
    58.  }
    

### 定义产物的source源码集-sourceRoots

在模块的主代码空间（src/main）下，承载着开发者编写的公共代码。如果开发者需要实现不同target之间的差异化逻辑，可以使用差异化代码空间（sourceRoots）。配合差异化代码空间的能力，可以在主代码空间中代码不变的情况下，针对不同的target，编译对应的代码到最终产物中。

**概念说明**

- packageName：当前模块的oh-package.json5中的name字段对应的值。
- sourceRoot：<defaultSourceRoot> | <targetSourceRoot> ，其中<defaultSourceRoot>是 src/main，<targetSourceRoot>可自定义，寻址优先级为 <targetSourceRoot> > <defaultSourceRoot>。
- sourcePath：在sourceRoot中的代码结构目录。
- sourceFileName：代码目录下的ets文件名。

例如以下工程目录：

1. entry
2. |--src
3. |----main
4. |------ets
5. |--------code
6. |----------test.ets
7. |----target
8. |------util
9. |--------util.ets

- packageName为entry。
- sourceRoot为src/main、src/target。
- sourcePath为ets/code、util。
- sourceFileName为test.ets、util.ets。

**规格限制**

1. import xxx from '<packageName>/sourcePath/sourceFileName' ：通过packageName的方式，省略sourceRoot，可以实现不同target下的差异化构建。

2. 支持hap、hsp、har（请注意：开启[文件/文件夹名称混淆](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/source-obfuscation#section-enable-filename-obfuscation)的har模块需要使用-keep-file-name指定sourceRoot，sourcePath，sourceFileName对应的文件/文件夹名称不被混淆）。

3. 不支持跨模块引用。

4. 不支持动态import。

**编译时模块target的选择优先级说明**

在模块编译的过程中，该模块使用的sourceRoots由当前模块编译时的target来决定。当前模块编译时选择target的优先级则为：命令行显式指定 > 直接引用方target > default。

如以下示例：

hap -> hsp -> har（->表示依赖）

其中hap和hsp存在三个target：default、custom、static，而har存在两个target：default、static。

- 执行编译命令：hvigorw -p module=hap@custom assembleHap，hap指定target为custom进行编译，那么三个模块编译时的target分别为：
    
    hap: custom，命令行显式指定；
    
    hsp: custom，命令行没有显式指定，则基于直接引用方查找，hsp的直接引用方为hap，hap的target为custom，hsp存在该target，则hsp的target为custom；
    
    har: default，命令行没有显式指定，则基于直接引用方查找，har的直接引用方为hsp，hsp的target为custom，har不存在该target，则har的target为default；
    

- 执行编译命令：hvigorw -p module=hap@custom,hsp@static assembleHap assembleHsp，hap指定target为custom，hsp则指定target为static进行编译，那么三个模块编译时的target分别为：
    
    hap: custom，命令行显式指定；
    
    hsp: static，命令行显式指定；
    
    har: static，命令行没有显式指定，则基于直接引用方查找，har的直接引用方为hsp，hsp的target为static，har存在该target，则har的target为static。
    
- 在当前依赖关系的基础上，添加依赖：hap -> har。执行编译命令：hvigorw -p module=hap@custom,hsp@static assembleHap assembleHsp。由于har没有显式指定target，且存在两个target不同的直接引用方（hap和hsp，对应的target分别为custom和static），所以编译过程中har的target只能二选一。基于这种场景，建议开发者显式指定模块的target进行编译：hvigorw -p module=hap@custom,hsp@static,har@static assembleHap assembleHsp assembleHar。

**示例**

1. 在entry模块的build-profile.json5中添加sourceRoots：

2. {
3.   "apiType": "stageMode",
4.   "buildOption": {},
5.   "targets": [ 
6.     { 
7.       "name": "default", 
8.       "source": { 
9.         "sourceRoots": ["./src/default"] // 配置target为default的差异化代码空间
10.       } 
11.     }, 
12.     { 
13.       "name": "custom", 
14.       "source": { 
15.         "sourceRoots": ["./src/custom"] // 配置target为custom的差异化代码空间
16.       } 
17.     } 
18.   ]
19. }

20. 在src目录下新增default/Test.ets和custom/Test.ets，新增后的模块目录结构：

21. entry
22.   |--src
23.     |--main
24.       |--ets
25.         |--pages
26.           |--Index.ets
27.     |--default
28.       |--Test.ets  // 新增
29.     |--custom
30.       |--Test.ets  // 新增  

31. 在default/Test.ets中写入代码：

32. export const getName = () => "default"

33. 在custom/Test.ets中写入代码：

34. export const getName = () => "custom"

35. 修改src/main/ets/pages/Index.ets的代码：

36. import { getName } from 'entry/Test'; // 其中entry为模块级的oh-package.json5中的name字段的值
37. @Entry
38. @Component
39. struct Index { 
40.   @State message: string = getName(); 
41.   build() { 
42.     RelativeContainer() { 
43.       Text(this.message) 
44.     } 
45.     .height('100%') 
46.     .width('100%') 
47.   }
48. }

49. 在工程级的build-profile.json5中配置targets：

50. {
51.   "app": {
52.     "signingConfigs": [],
53.     "products": [
54.       {
55.         "name": "default",
56.         "signingConfig": "default",
57.         "compatibleSdkVersion": "6.0.1(21)",
58.         "runtimeOS": "HarmonyOS",
59.       }
60.     ],
61.     "buildModeSet": [
62.       {
63.         "name": "debug",
64.       },
65.       {
66.         "name": "release"
67.       }
68.     ]
69.   },
70.   "modules": [
71.     {
72.       "name": "entry",
73.       "srcPath": "./entry",
74.       "targets": [
75.         {
76.           "name": "default",
77.           "applyToProducts": [
78.             "default"
79.           ]
80.         },
81.         {
82.           "name": "custom",
83.           "applyToProducts": [
84.             "default"
85.           ]
86.         }
87.       ]
88.     }
89.   ]
90. }

91. Sync完成后，选择entry的target为default，点击Run，界面展示default；选择entry的target为custom，点击Run，则界面展示custom。

### 定义产物的资源

每个target使用的资源文件可能存在差异，在开发过程中，开发者可以将每个target所使用的资源存放在不同的资源目录下。其中，ArkTS工程支持对main目录下的资源文件目录（resource）进行定制；JS工程支持对main目录下的资源文件目录（resource）及 Ability下的资源文件目录（res）进行定制。如下为ArkTS工程的资源文件目录定制示例：

1. { 
2.   "apiType": 'stageMode', 
3.   "buildOption": { 
4.   }, 
5.   "targets": [ 
6.     { 
7.       "name": "default", 
8.       "source": { 
9.         "pages": [ 
10.           "pages/Index" 
11.         ] 
12.       }, 
13.       "resource": {  // 定义默认版target使用的资源文件目录 
14.         "directories": [ 
15.           "./src/main/resources_default" 
16.         ] 
17.       } 
18.     }, 
19.     { 
20.       "name": "free", 
21.       "config": { 
22.         "deviceType": [ 
23.           "phone" 
24.         ] 
25.       }, 
26.       "source": {   
27.         "pages": [ 
28.           "pages/Index", 
29.           "pages/Page1" 
30.         ] 
31.       }, 
32.       "resource": {  // 定义免费版target使用的资源文件目录 
33.         "directories": [ 
34.           "./src/main/resources_free",
35.           "./src/main/resources_default"
36.         ] 
37.       } 
38.     }, 
39.     { 
40.       "name": "pay", 
41.       "config": { 
42.         "deviceType": [ 
43.           "phone" 
44.         ] 
45.       }, 
46.       "source": {   
47.         "pages": [ 
48.           "pages/Index", 
49.           "pages/Page2" 
50.         ] 
51.       }, 
52.       "resource": {  // 定义付费版target使用的资源文件目录
53.         "directories": [ 
54.           "./src/main/resources_pay",
55.           "./src/main/resources_default"
56.         ] 
57.       } 
58.     } 
59.   ] 
60. }

编译构建时，资源文件存在以下优先级顺序：

- AppScope目录下的资源文件会合入到模块下相同路径的资源目录中。如果两个目录下存在重名文件，编译打包后AppScope目录下的资源文件会覆盖模块下的资源。
- 如果target引用的多个资源文件目录下，存在重名文件，则在构建打包过程中，将按照配置的资源文件目录顺序进行选择。例如，上述付费版target引用的资源中，resources_pay和resources_default中存在重名文件，则resources_pay中的资源会被打包到HAP中。

### 定义产物的icon、label、launchType

针对每一个的target的ability，均可以定制不同的icon、label和launchType。如果不定义，则该target采用module.json5中module.abilities配置的icon、label，launchType默认为"singleton"。示例如下所示：

1. { 
2.    "apiType": 'stageMode', 
3.    "buildOption": { 
4.    }, 
5.    "targets": [ 
6.      { 
7.        "name": "default", 
8.        "source": {
9.         "abilities": [
10.           {
11.             "name": "EntryAbility",
12.             "icon":"$media:layered_image",
13.             "label":"$string:EntryAbility_label",
14.             "launchType": "singleton"
15.           }
16.         ]
17.       }
18.      }, 
19.      { 
20.        "name": "free", 
21.        "source": {
22.         "abilities": [
23.           {
24.             "name": "EntryAbility",
25.             "icon":"$media:layered_image",
26.             "label":"$string:EntryAbility_label",
27.             "launchType": "multiton"
28.           }
29.         ]
30.       }
31.      }
32.    ] 
33.  }

### 定义C++工程依赖的.so文件

在 C++ 工程中，可以对每个target依赖的.so文件进行定制。例如某模块依赖了function1.so、function2.so和function3.so三个文件，其中target为default的产物依赖了function1.so和function2.so；其中target为vip的产物依赖了function1.so和 function3.so，则示例代码如下所示：

1. {
2.   "apiType": 'stageMode',
3.   "buildOption": {
4.     "externalNativeOptions": {
5.       "path": "./src/main/cpp/CMakeLists.txt",
6.       "arguments": [],
7.       "abiFilters": [
8.         "arm64-v8a",
9.         "x86_64"
10.       ],
11.       "cppFlags": "",
12.     }
13.   },
14.   "targets": [  //定义不同的target 
15.     {
16.       "name": "default",
17.       "config": {
18.         "buildOption": {
19.           "nativeLib": {
20.             "filter": {
21.               //按照.so文件的优先级顺序，打包最高优先级的function1.so文件 
22.               "pickFirsts": [
23.                 "**/function1.so"
24.               ],
25.               //排除不打包的function3.so文件 
26.               "excludes": [
27.                 "**/function3.so"
28.               ],
29.               //允许当.so中资源重名冲突时，使用高优先级的.so文件覆盖低优先级的.so文件 
30.               "enableOverride": true
31.             }
32.           }
33.         }
34.       }
35.     },
36.     {
37.       "name": "vip",
38.       "config": {
39.         "buildOption": {
40.           "nativeLib": {
41.             "filter": {
42.               //按照.so文件的优先级顺序，打包最高优先级的function1.so文件 
43.               "pickFirsts": [
44.                 "**/function1.so"
45.               ],
46.               //排除不打包的function2.so文件 
47.               "excludes": [
48.                 "**/function2.so"
49.               ],
50.               //允许当.so中资源重名冲突时，使用高优先级的.so文件覆盖低优先级的.so文件 
51.               "enableOverride": true
52.             }
53.           }
54.         }
55.       }
56.     }
57.   ]
58. }

## 定制HAR多目标构建产物

每一个HAR模块均支持定制不同的target，通过在模块中的build-profile.json5文件中实现差异化定制，当前支持设备类型（deviceType）、资源（resource）、buildOption配置项（如C++依赖的.so、混淆配置、abi类型、cppFlags等）、源码集（source）的定制。

说明

在DevEco Studio中编译HAR模块时，仅支持default target，若需指定其他target，需通过命令行来指定，并通过命令行来编译。

例如构建指定的自定义target:free的har，可参考执行以下命令：

1. hvigorw --mode module -p product=default -p module=library@free -p buildMode=debug assembleHar

### 定义产物的deviceType

每一个target均可以指定支持的设备类型deviceType，也可以不定义。如果不定义，则该target默认支持module.json5/[config.json](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/application-configuration-file-overview-fa)中定义的设备类型。

同时，在定义每个target的deviceType时，支持的设备类型必须在module.json5或config.json中已经定义。例如，在上述定义的2个target中，分别定义default默认支持所有设备类型，free版本只支持2in1设备。

1. { 
2.   "apiType": 'stageMode', 
3.   "buildOption": { 
4.   }, 
5.   "targets": [ 
6.     { 
7.       "name": "default"  //未定义deviceType，默认支持config.json或module.json5中定义的设备类型 
8.     }, 
9.     { 
10.       "name": "free",
11.       "config": { 
12.         "deviceType": [  //定义free支持的设备类型为2in1
13.           "2in1" 
14.         ] 
15.       } 
16.     }
17.   ] 
18. }

### 定义C++工程依赖的.so文件

在 C++ 工程中，可以对每个target依赖的.so文件进行定制。例如某模块依赖了function1.so、function2.so和function3.so三个文件，其中target为default的产物依赖了function1.so和function2.so；其中target为vip的产物依赖了function1.so和 function3.so，则示例代码如下所示：

1. {
2.   "apiType": 'stageMode',
3.   "buildOption": {
4.     "externalNativeOptions": {
5.       "path": "./src/main/cpp/CMakeLists.txt",
6.       "arguments": [],
7.       "abiFilters": [
8.         "arm64-v8a",
9.         "x86_64"
10.       ],
11.       "cppFlags": "",
12.     }
13.   },
14.   "targets": [  //定义不同的target 
15.     {
16.       "name": "default",
17.       "config": {
18.         "buildOption": {
19.           "nativeLib": {
20.             "filter": {
21.               //按照.so文件的优先级顺序，打包最高优先级的function1.so文件 
22.               "pickFirsts": [
23.                 "**/function1.so"
24.               ],
25.               //排除不打包的function3.so文件 
26.               "excludes": [
27.                 "**/function3.so"
28.               ],
29.               //允许当.so中资源重名冲突时，使用高优先级的.so文件覆盖低优先级的.so文件 
30.               "enableOverride": true
31.             }
32.           }
33.         }
34.       }
35.     },
36.     {
37.       "name": "vip",
38.       "config": {
39.         "buildOption": {
40.           "nativeLib": {
41.             "filter": {
42.               //按照.so文件的优先级顺序，打包最高优先级的function1.so文件 
43.               "pickFirsts": [
44.                 "**/function1.so"
45.               ],
46.               //排除不打包的function2.so文件 
47.               "excludes": [
48.                 "**/function2.so"
49.               ],
50.               //允许当.so中资源重名冲突时，使用高优先级的.so文件覆盖低优先级的.so文件 
51.               "enableOverride": true
52.             }
53.           }
54.         }
55.       }
56.     }
57.   ]
58. }

### 定义产物的资源

每个target使用的资源文件可能存在差异，在开发过程中，开发者可以将每个target所使用的资源存放在不同的资源目录下。其中，ArkTS工程支持对main目录下的资源文件目录（resource）进行定制；JS工程支持对main目录下的资源文件目录（resource）及 Ability下的资源文件目录（res）进行定制。如下为ArkTS工程的资源文件目录定制示例：

1. { 
2.   "apiType": 'stageMode', 
3.   "buildOption": { 
4.   }, 
5.   "targets": [ 
6.     { 
7.       "name": "default",
8.       "resource": {  //定义默认版target使用的资源文件目录 
9.         "directories": [ 
10.           "./src/main/resources_default" 
11.         ] 
12.       } 
13.     }, 
14.     { 
15.       "name": "free", 
16.       "config": { 
17.         "deviceType": [ 
18.           "2in1" 
19.         ] 
20.       }, 
21.       "resource": {  //定义免费版target使用的资源文件目录 
22.         "directories": [ 
23.           "./src/main/resources_free",
24.           "./src/main/resources_default"
25.         ] 
26.       } 
27.     },
28.   ] 
29. }

### 定义产物的source源码集-sourceRoots

请参考[定义产物的source源码集-sourceRoots](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-customized-multi-targets-and-products-guides#section18668905913)。

## 配置APP多目标构建产物

APP用于应用/元服务上架发布，针对不同的应用场景，可以定制不同的product，每个product中支持对bundleName、bundleType、签名信息、icon和label以及包含的target进行定制。

**定义目标产物product**

每一个product对应一个定制的APP包，因此，在定制APP多目标构建产物前，应提前规划好需要定制的product名称。例如，定义productA和productB。工程级build-profile.json5文件示例如下：

在定制product时，必须存在"default"的product，否则编译时会出现错误。

说明

在编译构建流程中，default product或者default target都承载着兜底机制，其中，default target可以缺省。当某个模块的default target缺省时，Hvigor会默认加上default target并挂载到default product中，因此，构建default product时，默认会构建出default target。如果不想构建出default target，建议参考[定义product中包含的target](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-customized-multi-targets-and-products-guides#section7613106105114)，自定义product以及包含的target。

1. "app": { 
2.   "signingConfigs": [], 
3.   "products": [ 
4.     { 
5.       "name": "default", 
6.       "signingConfig": "default", 
7.       "compatibleSdkVersion": "6.0.1(21)", 
8.       "runtimeOS": "HarmonyOS", 
9.     }, 
10.     { 
11.       "name": "productA", 
12.       "compatibleSdkVersion": "6.0.1(21)", 
13.       "runtimeOS": "HarmonyOS", 
14.     }, 
15.     { 
16.       "name": "productB", 
17.       "compatibleSdkVersion": "6.0.1(21)", 
18.       "runtimeOS": "HarmonyOS", 
19.     } 
20.   ], 
21.   "buildModeSet": [ 
22.     { 
23.       "name": "debug", 
24.     }, 
25.     { 
26.       "name": "release" 
27.     } 
28.   ] 
29. }

### 定义产物的APP包名和供应商名称

每一个product均可以指定产物命名和供应商名称。

1. { 
2.   "app": { 
3.     "signingConfigs": [], 
4.     "products": [ 
5.       { 
6.         "name": "default", 
7.         "signingConfig": "default", 
8.         "compatibleSdkVersion": "6.0.1(21)", 
9.         "runtimeOS": "HarmonyOS", 
10.         "output": { 
11.           "artifactName": "customizedProductOutputName-1.0.0"  //产物名称为customizedProductOutputName-1.0.0
12.         }, 
13.         "vendor": "customizedProductVendorName"   //供应商名称为customizedProductVendorName
14.       }, 
15.       { 
16.         "name": "productA", 
17.         "compatibleSdkVersion": "6.0.1(21)", 
18.         "runtimeOS": "HarmonyOS", 
19.         "output": { 
20.           "artifactName": "customizedProductOutputNameA-1.0.0"  //产物名称为customizedProductOutputNameA-1.0.0
21.         }, 
22.         "vendor": "customizedProductVendorNameA"   //供应商名称为customizedProductVendorNameA
23.       }, 
24.       { 
25.         "name": "productB", 
26.         "compatibleSdkVersion": "6.0.1(21)", 
27.         "runtimeOS": "HarmonyOS", 
28.         "output": { 
29.           "artifactName": "customizedProductOutputNameB-1.0.0" //产物名称为customizedProductOutputNameB-1.0.0
30.         }, 
31.         "vendor": "customizedProductVendorNameB"   //供应商名称为customizedProductVendorNameB
32.       } 
33.     ], 
34.     "buildModeSet": [ 
35.       { 
36.         "name": "debug", 
37.       }, 
38.       { 
39.         "name": "release" 
40.       } 
41.     ] 
42.   }, 
43. }

如果已配置签名，product产物对应的APP包名为开发者定制的名称；如果未配置签名，product产物对应的APP包名为开发者定制的名称+unsigned。

### 定义product的bundleName

针对每个定义的product，均可以定制不同的bundleName，如果product未定义bundleName，则采用工程默认的bundleName。示例如下所示：

1. "app": { 
2.   "signingConfigs": [], 
3.   "products": [ 
4.     { 
5.       "name": "default", 
6.       "signingConfig": "default",
7.       "compatibleSdkVersion": "6.0.1(21)", 
8.       "runtimeOS": "HarmonyOS", 
9.       "bundleName": "com.example00.com"  //定义default的bundleName信息 
10.     }, 
11.     { 
12.       "name": "productA", 
13.       "signingConfig": "default",

14.       "compatibleSdkVersion": "6.0.1(21)", 
15.       "runtimeOS": "HarmonyOS", 
16.       "bundleName": "com.example01.com"  //定义productA的bundleName信息
17.     }, 
18.     { 
19.       "name": "productB", 
20.       "signingConfig": "default",
21.       "compatibleSdkVersion": "6.0.1(21)", 
22.       "runtimeOS": "HarmonyOS", 
23.       "bundleName": "com.example02.com"  //定义productB的bundleName信息 
24.     } 
25.   ], 
26.   "buildModeSet": [ 
27.     { 
28.       "name": "debug", 
29.     }, 
30.     { 
31.       "name": "release" 
32.     } 
33.   ] 
34. }

### 定义product的bundleType

针对每个定义的product，均可以定制不同的bundleType。开发者可以通过定义每个product的bundleType，分别定义产物类型：

- bundleType值为app，表示产物为应用；
- bundleType值为atomicService，表示产物为元服务。

如果product未定义bundleType，则采用工程的bundleType（即创建工程时选择的Application/Atomic Service）。示例如下所示：

1. "app": { 
2.   "signingConfigs": [], 
3.   "products": [ 
4.     { 
5.       "name": "default", 
6.       "signingConfig": "default",
7.       "compatibleSdkVersion": "6.0.1(21)", 
8.       "runtimeOS": "HarmonyOS", 
9.       "bundleName": "com.example00.com",   
10.       "bundleType": "app" //定义default的bundleType信息 
11.     },
12.     { 
13.       "name": "productA", 
14.       "signingConfig": "default",
15.       "compatibleSdkVersion": "6.0.1(21)", 
16.       "runtimeOS": "HarmonyOS", 
17.       "bundleName": "com.example01.com",    
18.       "bundleType": "atomicService"  //定义productA的bundleType信息 
19.     },
20.     { 
21.       "name": "productB", 
22.       "signingConfig": "default",
23.       "compatibleSdkVersion": "6.0.1(21)", 
24.       "runtimeOS": "HarmonyOS", 
25.       "bundleName": "com.example02.com",    
26.       "bundleType": "atomicService"  //定义productB的bundleType信息 
27.     } 
28.   ], 
29.   "buildModeSet": [ 
30.     { 
31.       "name": "debug", 
32.     },
33.     { 
34.       "name": "release"
35.     } 
36.   ] 
37. }

### 定义product的签名配置信息

针对每个定义的product，均可以定制不同的signingConfig签名文件，如果product未定义signingConfig，则构建生成未签名的APP包。

通常情况下，您首先需要在签名配置界面或工程的build-profile.json5文件中配置签名信息。例如在**File > Project Structure > Project > Signing Configs**界面，分别配置default、productA和productB的签名信息，如下图所示：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155925.76859740333082173178241760995861:50001231000000:2800:4A3702A7B29B44525C493F03FAE55509528B34A9BD0021432613E1499B016C27.png)

签名信息配置完成后，再添加各个product对应的签名文件，示例如下所示：

您也可以提前在product中定义签名文件信息，然后在签名界面对每个product进行签名，确保配置的product签名文件与签名界面配置的签名文件保持一致即可。

1. "app": { 
2.   "signingConfigs": [], //此处通过界面配置签名后会自动生成相应的签名配置，本文略 
3.   "products": [ 
4.     { 
5.       "name": "default", 
6.       "signingConfig": "default", //定义default的签名文件信息
7.       "compatibleSdkVersion": "6.0.1(21)", 
8.       "runtimeOS": "HarmonyOS", 
9.       "bundleName": "com.example00.com"  
10.     }, 
11.     { 
12.       "name": "productA", 
13.       "signingConfig": "productA", //定义productA的签名文件信息
14.       "compatibleSdkVersion": "6.0.1(21)", 
15.       "runtimeOS": "HarmonyOS", 
16.       "bundleName": "com.example01.com"  
17.     }, 
18.     { 
19.       "name": "productB", 
20.       "signingConfig": "productB", //定义productB的签名文件信息
21.       "compatibleSdkVersion": "6.0.1(21)", 
22.       "runtimeOS": "HarmonyOS", 
23.       "bundleName": "com.example02.com" 
24.     } 
25.   ], 
26.   "buildModeSet": [ 
27.     { 
28.       "name": "debug", 
29.     }, 
30.     { 
31.       "name": "release" 
32.     } 
33.   ] 
34. }

### 定义product的icon和label

针对每个定义的product，均可以定制不同的icon和label，如果product未定义icon和label，则采用工程默认的icon和label。示例如下所示：

说明

products中的icon和label字段在编译时会替换[app.json5](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-configuration-file)中对应的字段，app.json5和module.json5均可以配置这两个字段，如果都配置，优先级顺序请参考[配置优先级](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/layered-image#%E9%85%8D%E7%BD%AE%E4%BC%98%E5%85%88%E7%BA%A7%E5%92%8C%E7%94%9F%E6%88%90%E7%AD%96%E7%95%A5)。

1. {
2.   "app": {
3.     "signingConfigs": [],
4.     "products": [
5.       {
6.         "name": "default",
7.         "signingConfig": "default",
8.         "compatibleSdkVersion": "6.0.1(21)",
9.         "runtimeOS": "HarmonyOS",
10.         "icon":"$media:default_icon", //定义default的icon
11.         "label":"$string:default_name", //定义default的label
12.       },
13.       {
14.         "name": "productA",
15.         "signingConfig": "default",
16.         "compatibleSdkVersion": "6.0.1(21)",
17.         "icon":"$media:productA_icon", //定义productA的icon
18.         "label":"$string:productA_name", //定义productA的label
19.       },
20.       {
21.         "name": "productB",
22.         "signingConfig": "default",
23.         "compatibleSdkVersion": "6.0.1(21)",
24.         "runtimeOS": "HarmonyOS",
25.         "icon":"$media:productB_icon", //定义productB的icon
26.         "label":"$string:productB_name",  //定义productB的label
27.       }
28.     ],
29.     "buildModeSet": [
30.       {
31.         "name": "debug",
32.       },
33.       {
34.         "name": "release"
35.       }
36.     ]
37.   },
38.   ...
39. }

### 定义product中包含的target

开发者可以选择需要将定义的target分别打包到哪一个product中，每个product可以指定一个或多个target。

同时每个target也可以打包到不同的product中，但是同一个module的不同target不能打包到同一个product中（除非该module的不同target配置了不同的deviceType或distributionFilter/distroFilter）。

例如，前面定义了default、free和pay三个target，现需要将default target打包到default product中；将free target打包到productA中；将pay target打包到productB中，对应的示例代码如下所示：

1. { 
2.   "app": { 
3.     "signingConfigs": [], //此处通过界面配置签名后会自动生成相应的签名配置，本文略 
4.     "products": [ 
5.       { 
6.         "name": "default", 
7.         "signingConfig": "default",
8.         "compatibleSdkVersion": "6.0.1(21)", 
9.         "runtimeOS": "HarmonyOS", 
10.         "bundleName": "com.example00.com"  
11.       }, 
12.       { 
13.         "name": "productA", 
14.         "signingConfig": "productA",
15.         "compatibleSdkVersion": "6.0.1(21)", 
16.         "runtimeOS": "HarmonyOS", 
17.         "bundleName": "com.example01.com"  
18.       }, 
19.       { 
20.         "name": "productB", 
21.         "signingConfig": "productB",  
22.         "compatibleSdkVersion": "6.0.1(21)", 
23.         "runtimeOS": "HarmonyOS", 
24.         "bundleName": "com.example02.com" 
25.       } 
26.     ], 
27.   "modules": [ 
28.     { 
29.       "name": "entry", 
30.       "srcPath": "./entry", 
31.       "targets": [ 
32.         { 
33.           "name": "default",  //将default target打包到default APP中 
34.           "applyToProducts": [ 
35.             "default" 
36.           ] 
37.         }, 
38.         { 
39.           "name": "free",  //将free target打包到productA APP中 
40.           "applyToProducts": [ 
41.             "productA" 
42.           ] 
43.         }, 
44.         { 
45.           "name": "pay",  //将pay target打包到productB APP中 
46.           "applyToProducts": [ 
47.             "productB" 
48.           ] 
49.         } 
50.       ] 
51.     } 
52.   ] 
53. }

## 构建定义的目标产物

每个target对应一个HAP，每个product对应一个APP包，在编译构建时，如果存在多product或多target时，您可以指定编译具体的包。

单击右上角的![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155925.33520190340992899505106998533655:50001231000000:2800:6665C2E87674036DB628802462B87D3826697F40955507536677169BAAF977A8.png)图标，指定需要打包的**Product**及**Target**，然后单击**Apply**保存。例如选择"ProductA"中，entry模块对应的"free" Target。

- **Product**：选择需要构建的APP包。
- **Build Mode**：选择[编译模式](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-compilation-options-customizing-guide#section192461528194916)。
- **Product Info**：该APP包的BundleName和SigningConfig信息。
- **Target Select**：选择各个模块的Target，该Target需要包含在定义的Product中才能选择，如果未包含则显示"No Target to apply"

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155925.07231273815904323073680600244676:50001231000000:2800:57AE7258A8AA556F56FAAC7311FC5B0BD065FF3440DEC36BC785B2BFA99464EF.png)

然后执行编译构建APP/HAP的任务：

- 单击菜单栏的**Build > Build Hap(s)/APP(s) > Build APP(s)** ，构建指定的Product对应的APP。例如，按照[上述配置文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-customized-multi-targets-and-products-guides#section7613106105114)和上图中的配置，此时DevEco Studio将构建生成ProductA的APP包。default和ProductB的APP均不会生成。
- 单击菜单栏的**Build > Build Hap(s)/APP(s) > Build Hap(s)**，构建指定Product下的所有Target对应的HAP。

如果您想将某个模块下的指定target打包生成HAP，可以在工程目录中，单击模块名，然后再单击**Build > Make Module** **‘模块名** **’**，此时DevEco Studio将构建生成模块下指定target对应的包。例如，按照上述配置，此时DevEco Studio将构建生成entry模块下free的HAP。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155925.89968572620569037744078547423111:50001231000000:2800:5B6D40436413A91ADEF4877252D80CD900CF23FFFD6C5FCC890C20D65550C898.png)

## 调试和运行指定的Target

使用DevEco Studio调试或运行应用/元服务时，每个模块只能选择其中的一个target运行，可以通过单击右上角的![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155925.43971437464333064536486430486909:50001231000000:2800:6E1617639F29F672CB44BC550564AA26E7D3E30C6AF4BD9C8EC7E2D797892F1B.png)图标，指定需要调试或运行的**Product**下对应的**Module Target**，然后单击**Apply**保存。

说明

在选择需要调试或运行的target时，需要注意选择该target所属的Product，否则将找不到可调试和运行的target。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155925.54479128479366383485868644744569:50001231000000:2800:E42063C3BC61DDBABB067B67A3659927846675F34535FCCCBE39AFD5CD4CEF05.png)

## 多产物构建target

- align target
    
    编译构建时，优先级最高的target。工程配置align target后，如果模块中存在align target，那么将自动选择align target进行构建。align target作用范围是整个工程，只能配置一个，支持命令行和配置文件两种方式。
    
    - 命令行方式示例如下：
        
        1. hvigorw -c properties.ohos.align.target=target1 assembleHap
        
    
    - 在hvigor-config.json5配置文件中添加ohos.align.target，示例如下：
        
        1. "properties": {
        2.   'ohos.align.target': 'target1'
        3. },
        

- fallback target
    
    当模块不存在指定的target时会选用default进行构建，但如果不想用default进行构建，那么可以配置fallback target，当找不到指定target时，如果模块中存在fallback target，则使用fallback target进行构建。fallback target作用范围是整个工程，可配置多个，配置多个时按数组顺序先命中的生效。
    
    - 命令行方式示例如下：
        
        1. hvigorw -c properties.ohos.fallback.target=target1,target2 assembleHap
        
    
    - 在hvigor-config.json5配置文件中添加ohos.fallback.target，示例如下：
        
        1. "properties": {
        2.   'ohos.fallback.target': ['target1', 'target2']
        3. }
        

说明

- align target和fallback target配置方式命令行优先级高于配置文件。

- 使用配置文件配置align target和fallback target，仅支持DevEco Studio界面**Build**菜单栏功能，不支持**Run**菜单栏功能，可通过[hdc命令行工具](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/hdc)进行推包运行、调试。

多个target的优先级顺序为：align target > 命令行指定模块target > 父级模块target > fallback target > default。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155926.74828193592432883506978091717509:50001231000000:2800:11D628602CD9A452E8D3A8AAF14061CCC592B805339F17D011600001797F845A.png)

举例说明：

工程依赖entry->lib1->lib2，需要构建多个产品A、B、C，工程中target配置如下：

entry: A、B、default

lib1: B、C、default

lib2: A、C、default

指定align target为A，fallback target为C。那么构建hap时的编译命令为：

1. hvigorw --mode module -p module=entry -c properties.ohos.align.target=A -c properties.ohos.fallback.target=C assembleHap

编译的target选择就是：entry@A, lib1@C, lib2@A。

说明

以上所有说明仅针对非ohosTest模式。在ohosTest模式下，依赖的target固定为default，其他target均不生效。
### 基本概念

- target：对应HAR、HSP、HAP的多目标产物。工程内的每一个模块可以定义多个target，每个Target对应一个定制的HAP、HAR包，通过配置可以实现一个模块构建出不同的HAP、HAR包。
- product：对应App的多目标产物。一个HarmonyOS工程的构建产物为App包，一个工程可以定义多个product，每个product对应一个定制化应用包，通过配置可以实现一个工程构建出多个不同的应用包。

在构建过程中，鸿蒙构建系统会根据配置文件中定义的product和target信息，生成相应的构建产物。对于每个target，构建系统会生成一个对应的HAP/HSP/HAR。这个HAP/HSP/HAR包含了该target所需的所有代码和资源。对于每个product，构建系统会生成一个包含了其所有依赖的target的App包。这个App包可以用于发布和上架到应用市场。

### 应用场景

主要应用场景:

- 不同用户群体：针对不同的用户群体（如国内用户与国际用户等），系统支持构建不同的应用版本。这些版本在功能、界面、语言等方面可能有所不同，以满足不同用户群体的需求。
- 不同业务场景：在不同的业务场景中，同一个应用可能需要提供不同的功能或资源。例如，一个在线教育应用可能需要为学生提供学习资料，而为教师提供教学资料。HarmonyOS系统支持通过配置不同的Target来实现这种差异化定制。

针对以上场景，开发者需要通过修改build-profile.json5、module.json5等配置文件，定义出不同的product和target。在这些配置文件中，开发者不仅可以为每个target指定不同的设备类型、源码集、资源等，并且还可以根据业务需要为不同的product分配不同的target。然后在构建过程中，构建工具会根据这些配置生成不同的target，然后通过不同的target搭配构建出不同的product产物。

本文将通过一个具体的案例来介绍如何配置不同资源以及如何构建出多目标产物。

## 实现原理

HarmonyOS多目标产物支持[HAP](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/hap-package)（应用安装的基本单位，每个HAP都对应一个应用模块）、[HAR](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/har-package)（静态共享包）、[HSP](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/in-app-hsp)（动态共享包）以及App（由多个HAP打包一起上架的完整应用程序）包多种类型的包，以满足不同业务场景下的应用开发和定制需求。

### 多目标产物定制项

目前多目标产物支持的定制项信息如下表所示，表中已给出每一项的作用。详细的每一个定制项的配置方法可以参考：[配置多目标产物](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-customized-multi-targets-and-products)。

**表1** 产物定制项
|多目标模块|定制项|作用|
|:--|:--|:--|
|HAP|HAP包名（artifactName）|产品生成的应用包名称，可由数字、英文字母、中划线、下划线和英文句号（.）组成，支持输入版本号。|
|设备类型（deviceType）|用于配置支持的设备类型，如Phone、Tablet等。|
|源码集（source）|target的源码范围：<br><br>- pages：定制pages源码目录的page页面，数组长度至少为1。<br>- sourceRoots：定制差异化代码空间，数组长度至少为1。|
|资源（resource）|配置需要的资源文件路径，支持配置多个资源文件路径。|
|分发规则（distributionFilter）|针对多target存在相同设备类型deviceType的场景，相同设备类型的target需要指定分发规则distributionFilter。|
|产物分包（preloads）|对于元服务，每一个target均可以指定preloads的分包。|
|abilities能力项（icon、label和launchType）|定制产物图标、名称、启动模式。|
|so库依赖（nativeLib-filter）|定制打包so库的过滤规则。|
|HAR/HSP|设备类型（deviceType）|用于配置支持的设备类型，如Phone、Tablet等。|
|so库依赖（nativeLib-filter）|定制打包so库的过滤规则。|
|源码集（source）|target的源码范围：<br><br>- pages：定制pages源码目录的page页面，数组长度至少为1。<br>- sourceRoots：定制差异化代码空间，数组长度至少为1。|
|资源（resource）|配置需要的资源文件路径，支持配置多个资源文件路径。|
|App|App包名和供应商名称(artifactName、vendor)|指定产物命名和供应商名称。|
|bundleName|定义工程的bundleName信息，在签名的时候可以选择对应的bundleName进行签名。如果product未定义bundleName，则采用工程默认的bundleName。|
|bundleType|定义产物类型：<br><br>- bundleType值为app，表示产物为应用；<br>- bundleType值为atomicService，表示产物为元服务。|
|签名配置信息(signingConfig)|为不同产物定制不同的签名文件。|
|应用图标、名称（icon、label）|为不同产物定制不同的图标和名称。|
|依赖的模块（modules）|定义product中包含的target，每个product可以指定一个或多个target。|

综上所述，App、HAP、HAR、HSP包目前并不支持配置所有配置项的差异化定制，开发者在开发过程中需要根据已支持的配置项合理的进行多目标定制。

### 构建原理图

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251212193142.24482997784580331477105756086491:50001231000000:2800:1631421593367B48AC9A64B339291F0FE7789B0E9937BFA4C7FE35ABEBDC9B72.png "点击放大")

如图所示，在HarmonyOS应用开发过程中，一个应用通常包含多个HAR/HAP/HSP模块。每个HAR/HAP/HSP模块可以通过配置模块级的build-profile.json文件定义多个target，每个target可以定制不同的资源（具体可参考上文定制项介绍）。因此形成了具有差异性的target，如：Module A通过定制生成了TargetA-1、TargetA-2；Module B通过定制生成了TargetB-1、TargetB-2、TargetB-3；Module C通过定制生成了TargetC-1、TargetC-2。然后通过配置工程级的build-profile.json定义多个product，每个product可以依赖不同的Target并且配置不同的App产物定制项。因此形成了具有差异的product，如：依赖TargetA-1、TargetB-1、TargetC-1构建出App-product1；依赖TargetB-3、TargetC-2构建出App-product2。最终在构建工程时选择相应的product就可以显示出对应的定制效果。

### 开发流程

1. 首先需要拆解需求，根据具体的业务场景判断出product、target信息。即确认我们要构建哪些product，每个product依赖哪些target以及每个target的定制项有哪些。
2. 分别定制每个target定制项的内容。
3. 分别定制product定制项并为其依赖需要的target。
4. 实现不同目标产物需要定制的业务逻辑。
5. 选择不同的product构建出不同目标产物。

## 场景案例

本节主要根据一个案例介绍构建多目标产物的流程和方法，该案例可以由同一套源代码构建出Official版本（官方版）和Test版本（测试版）两个product工程。两个工程的实现效果如下：

Official版本：工程会在首页中显示Official版的资源以及一个页面跳转按钮，该页面是一个HAP模块页面。通过点击按钮可以跳转到Official版定制页面，该页面是一个HAR模块页面，其中包含了一个运算器。该运算器支持加法和减法。

Test版本：工程会在首页中显示Test版的资源以及一个页面跳转按钮，该页面是一个HAP模块页面。通过点击按钮可以跳转到Test版定制页面，该页面是一个HAR模块页面，其中包含了一个普通版的运算器。该运算器仅支持减法。

该案例包含了HAP、HAR、APP相关定制项，具体差异项信息如下：

**表2** 定制项信息
|定制模块|Official版本定制项|Test版本定制项|
|:--|:--|:--|
|HAP模块(target)|1. target名称official<br>2. source源码集-pages<br>3. 资源文件目录<br>4. source源码集-sourceRoots|1. target名称test<br>2. source源码集-pages<br>3. 资源文件目录<br>4. source源码集-sourceRoots|
|HAR模块(target)|1. target名称official<br>2. buildProfileFields自定义参数<br>3. 产物名称<br>4. source源码集-sourceRoots<br>5. 资源文件目录<br>6. 剔除的.so文件|1. target名称test<br>2. buildProfileFields自定义参数<br>3. 产物名称<br>4. source源码集-sourceRoots<br>5. 资源文件目录|
|App工程（product）|1. product名称official<br>2. 产物bundleName<br>3. 签名配置信息<br>4. 应用图标<br>5. 依赖的target|1. product名称test<br>2. 产物bundleName<br>3. 签名配置信息<br>4. 应用图标<br>5. 依赖的target|

1. 拆解需求，根据具体的业务场景判断出product、target信息。
    
    首先，根据上面案例设计和定制项表格可以确认我们需要定制两个product版本，即Official版本和Test版本。每个product需要依赖两个模块，即一个HAP模块和一个HAR模块。
    
2. 定制target内容。
    
    HAP模块：在模块级build-profile.json5文件中配置。
    
    1. "targets": [
    2.   {
    3.     "name": "official",
    4.     "config": {
    5.       "buildOption": {
    6.         "arkOptions": {
    7.           "buildProfileFields": {
    8.             "productName": "official"
    9.           }
    10.         },
    11.         "nativeLib": {
    12.           "filter": {
    13.             "excludes": [
    14.               "../libs/arm64-v8a/libentry.so"
    15.             ]
    16.           }
    17.         }
    18.       }
    19.     },
    20.     "runtimeOS": "HarmonyOS",
    21.     "output": {
    22.       "artifactName": "official"
    23.     },
    24.     "source": {
    25.       "sourceRoots": [
    26.         "./src/official_pages"
    27.       ]
    28.     },
    29.     "resource": {
    30.       "directories": [
    31.         "./src/main/official/resources",
    32.         "./src/main/resources"
    33.       ]
    34.     }
    35.   },
    36.   {
    37.     "name": "test",
    38.     "config": {
    39.       "buildOption": {
    40.         "arkOptions": {
    41.           "buildProfileFields": {
    42.             "productName": "test"
    43.           }
    44.         }
    45.       }
    46.     },
    47.     "runtimeOS": "HarmonyOS",
    48.     "output": {
    49.       "artifactName": "test"
    50.     },
    51.     "source": {
    52.       "sourceRoots": [
    53.         "./src/test_pages"
    54.       ]
    55.     },
    56.     "resource": {
    57.       "directories": [
    58.         "./src/main/test/resources",
    59.         "./src/main/resources"
    60.       ]
    61.     }
    62.   }
    63. ],
    
    [build-profile.json5](https://gitee.com/harmonyos_samples/MultiTarget/blob/master/myhar/build-profile.json5#L22-L84)
    
    上述配置文件代码中，配置了official版本与test版本的target名称、source源码集-pages、source源码集-sourceRoots以及资源文件路径，因此我们需要在对应的目录结构下创建我们配置的文件以及目录。针对以上配置信息，我们需要创建pages目录下的Index.ets文件、src目录下的test_pages和official_pages目录以及src/main目录下的resource_test和resource_official目录。
    
    在配置不同target的资源文件目录时，可以配置多个资源文件目录，建议将共有的资源文件放置到默认的资源文件目录中，将有差异的资源部分放置到定制的资源文件目录中，然后在配置资源目录时将默认的资源目录和定制的资源目录都加上。例如：案例中即给不同版本配置了两个资源目录，一个用于存放共有资源，一个存放不同target的差异性资源。
    
    如果target引用的多个资源文件目录下，存在同名的资源，则在构建打包过程中，将按照配置的资源文件目录顺序进行选择。例如，上述official版target引用的资源中，resource_official和resource中存在同名的资源文件，则resource_official中的资源会被打包到HAP中。
    
    * 配置文件中，default为创建工程时默认生成的target，一般无需特殊处理。
    
    HAR模块：在模块级build-profile.json5文件中配置。
    
    1. {
    2.   "app": {
    3.     "signingConfigs": [],
    4.     "products": [
    5.       {
    6.         "name": "official",
    7.         "compatibleSdkVersion": "5.0.5(17)",
    8.         "targetSdkVersion": "5.0.5(17)",
    9.         "runtimeOS": "HarmonyOS",
    10.         "buildOption": {
    11.           "strictMode": {
    12.             "caseSensitiveCheck": true,
    13.             "useNormalizedOHMUrl": true
    14.           }
    15.         },
    16.         "bundleName": "com.official.com",
    17.         "bundleType": "app",
    18.         "icon": "$media:startIcon",
    19.         "label": "$string:official_app_name"
    20.       },
    21.       {
    22.         "name": "test",
    23.         "compatibleSdkVersion": "5.0.5(17)",
    24.         "targetSdkVersion": "5.0.5(17)",
    25.         "runtimeOS": "HarmonyOS",
    26.         "buildOption": {
    27.           "strictMode": {
    28.             "caseSensitiveCheck": true,
    29.             "useNormalizedOHMUrl": true
    30.           }
    31.         },
    32.         "bundleName": "com.test.com",
    33.         "bundleType": "app",
    34.         "icon": "$media:app_icon",
    35.         "label": "$string:test_app_name"
    36.       },
    37.       {
    38.         "name": "default",
    39.         "compatibleSdkVersion": "5.0.5(17)",
    40.         "targetSdkVersion": "5.0.5(17)",
    41.         "runtimeOS": "HarmonyOS",
    42.       }
    43.     ],
    44.     "buildModeSet": [
    45.       {
    46.         "name": "debug",
    47.       },
    48.       {
    49.         "name": "release"
    50.       }
    51.     ]
    52.   },
    53.   "modules": [
    54.     {
    55.       "name": "entry",
    56.       "srcPath": "./entry",
    57.       "targets": [
    58.         {
    59.           "name": "official",
    60.           "applyToProducts": [
    61.             "official"
    62.           ]
    63.         },
    64.         {
    65.           "name": "test",
    66.           "applyToProducts": [
    67.             "test"
    68.           ]
    69.         }
    70.       ]
    71.     },
    72.     {
    73.       "name": "myhar",
    74.       "srcPath": "./myhar"
    75.     }
    76.   ]
    77. }
    
    [build-profile.json5](https://gitee.com/harmonyos_samples/MultiTarget/blob/master/build-profile.json5#L0-L77)
    
    上述配置文件代码中，配置了official版本与test版本的target名称、buildProFields自定义参数、产物名称、source源码集-sourceRoots以及资源文件目录，并且在official版本中剔除了无需打包的.so文件。同样的，我们也需要创建我们需要的文件目录，因此我们需要在该HAR模块的src/main/目录下创建resources_test和resources_official文件夹，在src/目录下创建official_pages和test_pages文件夹。
    
3. 定制product内容。
    
    App工程：在工程级build-profile.json5文件中配置。
    
    1. {
    2.   "app": {
    3.     "signingConfigs": [],
    4.     "products": [
    5.       {
    6.         "name": "official",
    7.         "compatibleSdkVersion": "5.0.0(12)",
    8.         "runtimeOS": "HarmonyOS",
    9.         "buildOption": {
    10.           "strictMode": {
    11.             "caseSensitiveCheck": true,
    12.             "useNormalizedOHMUrl": true
    13.           }
    14.         },
    15.         "bundleName": "com.official.com",
    16.         "bundleType": "app",
    17.         "icon": "$media:startIcon",
    18.         "label": "$string:official_app_name"
    19.       },
    20.       {
    21.         "name": "test",
    22.         "compatibleSdkVersion": "5.0.0(12)",
    23.         "runtimeOS": "HarmonyOS",
    24.         "buildOption": {
    25.           "strictMode": {
    26.             "caseSensitiveCheck": true,
    27.             "useNormalizedOHMUrl": true
    28.           }
    29.         },
    30.         "bundleName": "com.test.com",
    31.         "bundleType": "app",
    32.         "icon": "$media:app_icon",
    33.         "label": "$string:test_app_name"
    34.       },
    35.       {
    36.         "name": "default",
    37.         "compatibleSdkVersion": "5.0.0(12)",
    38.         "runtimeOS": "HarmonyOS",
    39.       }
    40.     ],
    41.     "buildModeSet": [
    42.       {
    43.         "name": "debug",
    44.       },
    45.       {
    46.         "name": "release"
    47.       }
    48.     ]
    49.   },
    50.   "modules": [
    51.     {
    52.       "name": "entry",
    53.       "srcPath": "./entry",
    54.       "targets": [
    55.         {
    56.           "name": "default",
    57.           "applyToProducts": [
    58.             "default"
    59.           ]
    60.         },
    61.         {
    62.           "name": "official",
    63.           "applyToProducts": [
    64.             "official"
    65.           ]
    66.         },
    67.         {
    68.           "name": "test",
    69.           "applyToProducts": [
    70.             "test"
    71.           ]
    72.         }
    73.       ]
    74.     },
    75.     {
    76.       "name": "myhar",
    77.       "srcPath": "./myhar",
    78.       "targets": [
    79.         {
    80.           "name": "official",
    81.           "applyToProducts": [
    82.             "official"
    83.           ]
    84.         },
    85.         {
    86.           "name": "test",
    87.           "applyToProducts": [
    88.             "test"
    89.           ]
    90.         }
    91.       ]
    92.     }
    93.   ]
    94. }
    
    [build-profile.json5](https://gitee.com/harmonyos_samples/MultiTarget/blob/master/build-profile.json5#L2-L95)
    
    在该配置文件中，配置了product名称、产物bundleName、签名配置信息、应用图标、依赖的target信息。这里需要注意的是，依赖的HAR模块需要在引用他的模块内配置依赖关系。我们的案例是在entry模块里调用的HAR包，所以需要在其对应的oh-package.json5文件中配置dependencies依赖。
    
4. 实现不同目标产物需要定制的业务逻辑。
    - 通过[source源码集-sourceRoots配置](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-customized-multi-targets-and-products-guides#section18668905913)的差异性代码空间，实现标题（代码文件）多目标效果。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251212193142.05260022138999146076644831594595:50001231000000:2800:1D795D35632356D6734F4F33D7C625D37372BB9FB9C46E02D477F671D396AA70.png) ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251212193142.34424892153621911643794851656599:50001231000000:2800:85B9AFC2AFA8B1689655CDE96FAB43A72E702E28105583AB37D28774DCEB76BA.png)
        
        在上述配置文件中，配置了HAP模块的source源码集-sourceRoots目录，official版本与test版本分别对应src/official_pages和src/test_pages。
        
        分别在对应的sourceRoots目录下创建同名ets文件并创建同名同类型的方法，例如：示例中创建的是VersionInfo.ets文件。添加如下代码：
        
        src/official_pages/VersionInfo.ets
        
        1. export const getName = () => "This is official version."
        2. export const getTitleName = () => $r('app.string.title')
        
        [VersionInfo.ets](https://gitee.com/harmonyos_samples/MultiTarget/blob/master/entry/src/official_pages/VersionInfo.ets#L16-L17)
        
        src/test_pages/VersionInfo.ets
        
        1. export const getName = () => "This is test version."
        2. export const getTitleName = () => $r('app.string.title')
        
        [VersionInfo.ets](https://gitee.com/harmonyos_samples/MultiTarget/blob/master/entry/src/test_pages/VersionInfo.ets#L16-L17)
        
        在Index.ets文件中，通过import packageName的方式，省略sourceRoot，可以实现不同target下的差异化构建（ import xxx from '<packageName>/sourceFileName'）。该能力具体可参考：[source源码集-sourceRoots配置](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-customized-multi-targets-and-products-guides#section18668905913)。
        
        1. import { getName, getTitleName } from '../../../test_pages/VersionInfo'
        
        2. @Entry
        3. @Component
        4. struct Index {
        5.   @State message: string = getName();
        6.   @State titleMessage: Resource = getTitleName();
        
        7.   build() {
        8.     Column() {
        9.       Column() {
        10.         Text(this.titleMessage)
        11.           .height(40)
        12.           .fontSize(30)
        13.           .fontWeight(FontWeight.Medium)
        14.         Text(this.message)
        15.           .fontSize(14)
        16.           .fontWeight(FontWeight.Normal)
        17.           .fontColor(Color.Black)
        18.           .opacity(0.6)
        19.           .height(19)
        20.           .margin({ top: 2 })
        21.       }
        22.       // ...
        23.     }
        24.     // ...
        25.   }
        26. }
        
        [Index.ets](https://gitee.com/harmonyos_samples/MultiTarget/blob/master/entry/src/main/ets/pages/Index.ets#L17-L65)
        
    - 在HAR模块引用差异性资源，实现页面中资源多目标效果。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251212193142.77562873197520478719083339604162:50001231000000:2800:CA79CF023C2AD62AC58D247E6DBBCA473F2B14B64F5CDFF9B34173C861AB02D3.png) ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251212193142.71149392624958117366220101621863:50001231000000:2800:757DE1256131C5E34355DF2332639CF278518200E1B1A3D755BF20CD27B7EF21.png)
        
        在上述配置文件中，我们配置了HAR模块的资源文件路径，official版本和test版本分别对应src/main/resources_official和src/main/resources_test文件。
        
        分别在对应的资源文件目录下添加同名图片资源和json字符串。例如：示例中分别在资源文件目录下的media文件中放入同名的HarImage.jpg图片（图片内容不同），并在element文件下的string.json中添加同名参数"title_description"（其对应的"value"值不相同）。
        
        在页面中直接引用对应同名资源即可，代码如下：
        
        1. TextArea({ text: 'This is the first page of the beta version of the HAR module. Click the button below to jump to the second page of the beta version of the HAR module - the calculator page.' })
        2.   .fontSize(16)
        3.   .width('100%')
        4.   .fontColor('#e6000000')
        5.   .fontWeight(FontWeight.Normal)
        6.   .borderRadius(16)
        7.   .focusable(false)
        8. Image($r('app.media.HarImage'))
        9.   .width('100%')
        10.   .borderRadius(12)
        11.   .padding({ top: 16 })
        
        [MainPage.ets](https://gitee.com/harmonyos_samples/MultiTarget/blob/master/myhar/src/main/ets/components/MainPage.ets#L42-L52)
        
    - 在HAR模块中通过不同自定义参数信息跳转到不同页面，实现路由跳转多目标效果。
        
        效果对比如下：
        
        **图1** official版本  
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251212193142.73365647416845698743480051866265:50001231000000:2800:AEF37D7E652843AFB0A0922B1269A5976D93A20B5B018BD1942DBB0207E95E7F.gif)
        
        **图2** test版本  
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251212193142.31618739949542067673026564324458:50001231000000:2800:586072D80C9C7C1155C37F4A040FF7BAE3DBE9A464288868691B3CCFDEC61E1C.gif)
        
        在先前的案例中，已经介绍了如何在sourceRoot目录配置的差异性代码空间中实现对同名文件中的同名方法的调用。这里主要介绍在不同的target中如何调用不同名的文件中的不同方法。
        
        首先，需要通过配置文件中配置的自定义参数[生成相应的BuildProfile.ets文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-get-build-profile-para-guide#section8279154125918)。上述HAR模块的配置文件中，我们配置了buildProfileFields自定义参数"productName",在official和test版本中分别配置了不同的值"official"和"test"。这样我们构建不同的产物版本就会生成不同的"productName"值，用于在代码工程中区分不同的产物版本。
        
        然后，分别在official和test的对应的sourceRoots目录下创建不同的ets文件，并导出相应的组件。如示例中在HAR模块的src/official_pages目录下创建了OfficialSecondPages.ets并export了一个OfficialSecond组件，然后在src/test_pages目录下创建了TestSecondPages.ets并export了一个TestSecond组件。这两个组件中分别包含了不同的页面信息。
        
        最后在首页中import相应的方法实现跳转逻辑。具体代码如下：
        
        导入方法及组件：
        
        1. import BuildProfile from '../../../../BuildProfile';
        2. import { OfficialSecond } from '../../../official_pages/OfficialSecondPage';
        3. import { TestSecond } from '../../../test_pages/TestSecondPage';
        
        [MainPage.ets](https://gitee.com/harmonyos_samples/MultiTarget/blob/master/myhar/src/main/ets/components/MainPage.ets#L16-L18)
        
        定义页面跳转逻辑：接收到不同的参数值跳转不同页面。
        
        4. @Provide('pageInfos') pageInfos: NavPathStack = new NavPathStack();
        
        5. @Builder
        6. PagesMap(name: string) {
        7.   if (name == 'official') {
        8.     // According to the user-defined parameter value, if the value is Official, the
        9.     // second page of official will jump correspondingly.
        10.     OfficialSecond();
        11.   } else {
        12.     TestSecond();
        13.   }
        14. }
        
        [MainPage.ets](https://gitee.com/harmonyos_samples/MultiTarget/blob/master/myhar/src/main/ets/components/MainPage.ets#L23-L34)
        
        为按钮添加点击属性，并传递自定义参数，用于实现Navigation路由跳转：
        
        15. Button($r('app.string.button_describe'))
        16.   .fontSize(16)
        17.   .height(40)
        18.   .width('100%')
        19.   .onClick(() => {
        20.     this.pageInfos.pushPath({ name: 'official' });
        21.   })
        
        [MainPage.ets](https://gitee.com/harmonyos_samples/MultiTarget/blob/master/myhar/src/main/ets/components/MainPage.ets#L56-L62)
        
5. 选择不同的product构建出不同的目标产物。
    
    **图3** 构建图示  
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251212193142.65641268482498624617481720027151:50001231000000:2800:A1ECDE68EBFF51798D3D7B3AC032F314C0B990D8CE786DF4C4A285A39E9B81CD.png)
    
    首先点击DevEco Studio工具右上角的Product按钮，即图中的1号标识处，然后在2号标识处选择对应的product工程，选择完工程之后会自动映射出我们文件中已经依赖的target，最后点击Apply应用。上述操作完成之后就可以点击运行按钮查看多目标产物效果了。本案例运行效果图如下：
    
    **图4** Official版本
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251212193143.78322359308695005543034684269330:50001231000000:2800:C925783D4935BDB30DAA9A3404C8E1F1184912FDCFEF259DED4C515B41D1EC5C.gif)
    
    **图5** Test版本  
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251212193143.32060157002366306283670191125746:50001231000000:2800:ED69ED9C5D706A095B42F34473CABE898035833DEFC5BD93FF2D8D6CACE52B02.gif)
    

## 常见问题

### 如何为不同的product产物配置签名信息？

配置工程级的build-profile.json5文件.

首先需要在每个product下添加配置项"signingConfig"。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251212193143.93013629295686079928253244687536:50001231000000:2800:238059E4AE050701FB745888B496145A88C9DCC6A6BBEAE8D2DF5A3D4D64092A.png "点击放大")

然后进入到签名配置页面，点击加号，添加签名信息：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251212193143.21073196296408847812557469124314:50001231000000:2800:FCB8661C177AC6EFA6D00C57EE9C75059322A8CF8F8EAB3490FE44082EFF06A7.png "点击放大")

然后选择对应的bundle name，并填写上面配置的"signingConfig"信息（每个product产物都需要配置）：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251212193143.36697489391407090577211001761816:50001231000000:2800:03A4D833F16D6628306E843561D5667B230A0F8F52B8A80C2C7FC29CFA8BD953.png "点击放大")

点击ok之后，进行签名即可。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251212193143.77170128502284522960984638953880:50001231000000:2800:FF7D1A34D98E9CF726941A7BD66E9E289BB6CD3BE8363730370208D7AD642250.png "点击放大")

## 示例代码

- [构建多目标产物工程](https://gitee.com/harmonyos_samples/MultiTarget)