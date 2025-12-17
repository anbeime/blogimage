# 获取命令行工具

更新时间: 2025-12-16 15:59

该命令行工具集合了HarmonyOS应用开发所用到的系列工具，包括代码检查codelinter、堆栈解析hstack、命令行构建hvigorw、三方依赖管理ohpm和SDK中包含的一系列工具，本文主要讲解codelinter、hstack、hvigorw等工具的使用方式，关于SDK中包含的工具的使用指导请参考[SDK命令行工具](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/command-line-tools-overview)。

## 命令行工具获取

请前往[下载中心](https://developer.huawei.com/consumer/cn/download/command-line-tools-for-hmos)获取命令行工具Command Line Tools，并根据下载中心页面**工具完整性**指导进行完整性校验。

说明

HarmonyOS SDK已嵌入命令行工具中，无需额外下载配置。

## 配置环境变量

将命令行工具进行解压，codelinter、hstack等工具存放在Command Line Tools的bin目录下，需要将该目录配置到PATH变量中。

### Windows

命令行工具解压后，将${Command Line Tools解压路径}\command-line-tools\bin目录配置到系统或者用户的PATH变量中。下图是将命令行工具解压到D盘根目录后的示例路径。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155951.84614570235277393753316463217127:50001231000000:2800:6CC3E5AEDCA98687967EFC1AF3D98C996500E99731D1BB44F55CC69DDC1C99FD.png)

### macOS/Linux

1. 将下载后的命令行工具解压到本地。
2. 打开终端工具，执行以下命令，根据输出结果分别执行不同命令。
    
    1. echo $SHELL 
    
    - 如果输出结果为/bin/bash，则执行以下命令，打开.bash_profile文件。
        
        1. vi ~/.bash_profile
        
    - 如果输出结果为/bin/zsh，则执行以下命令，打开.zshrc文件。
        
        1. vi ~/.zshrc
        
3. 单击字母“i”，进入**Insert**模式。
4. 输入以下内容，在PATH路径下添加环境变量。请以实际命令行工具存储路径为准。
    
    1. export PATH=${Command Line Tools解压路径}/command-line-tools/bin:$PATH  
    
5. 编辑完成后，单击**Esc**键，退出编辑模式，然后输入“:wq”，单击**Enter**键保存。
6. 执行以下命令，使配置的环境变量生效。
    - 如果[步骤2](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-commandline-get#zh-cn_topic_0000001169160500_zh-cn_topic_0000001056725590_li56571525162613)时打开的是.bash_profile文件，请执行如下命令：
        
        1. source ~/.bash_profile
        
    - 如果[步骤2](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-commandline-get#zh-cn_topic_0000001169160500_zh-cn_topic_0000001056725590_li56571525162613)时打开的是.zshrc文件，请执行如下命令：
        
        1. source ~/.zshrc
        

说明

如需验证是否配置成功，可以使用相关命令验证，例如执行codelinter -v指令，检查是否可以正确获取codelinter工具版本。
# 代码检查工具（codelinter）

更新时间: 2025-12-16 15:59

codelinter同时支持使用命令行执行代码检查与修复，可将codelinter工具集成到门禁或持续集成环境中。

codelinter命令行格式为：

1. codelinter [options] [dir] 

options：可选配置，请参考[表1](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-command-line-codelinter#table25697717185)。

dir：待检查的工程根目录；为可选参数，如不指定，默认为当前上下文目录。

**表1** codelinter命令行配置
|指令|说明|
|:--|:--|
|--config/-c _<filepath>_|指定执行codelinter检查的规则配置文件，_<filepath>_指定执行检查的规则配置文件位置。|
|--fix|设置codelinter检查同时执行QuickFix。|
|--format/-f|设置检查结果的输出格式。目前支持default/json/xml/html四种格式；不指定时，默认是default格式（文本格式）。|
|--output/-o _<filepath>_|指定检查结果保存位置，且命令行窗口不展示检查结果。_<filepath>_指定存放代码检查结果的文件路径，支持使用相对/绝对路径。不使用--output指令时，检查结果默认会显示在命令行窗口中。|
|--version/-v|查看codelinter版本。|
|--product/-p _<productName>_|指定当前生效的product。 <productName> 为生效的product名称。|
|--incremental/-i|对Git工程中的增量文件（包含新增/修改/重命名的文件）执行Code Linter检查。|
|--help/-h|查询codelinter命令行帮助。|
|--exit-on/-e <levels>|指定哪些告警级别需要返回非零退出码，告警级别包括：error、warn和suggestion。若需要指定多个告警级别，级别间需要用英文逗号分开。<br><br>退出码的计算方式为：用一个3位的二进制数从高到低分别表示error、warn、suggestion告警级别。若在命令行中配置告警级别，并且代码检查结果中也包含该告警级别，则该二进制值为1，否则均为0。将二进制数转换为十进制数，则是退出码。<br><br>例如：<br><br>- 命令配置为--exit-on error，代码检查结果包括error、warn、suggestion三类告警，则退出码的二进制数为100，十进制数为4。<br>- 命令配置为--exit-on error，代码检查结果包括warn、suggestion两类告警，则退出码的二进制数为000，十进制数为0。|

1. 进行codelinter代码检查与修复。若您的工程存在多个product，请使用--product/-p指令，指定生效的product和执行检查的工程根目录。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155951.98615360275218336728075244963831:50001231000000:2800:5D10B63B98FA6DA3440767739FA7FBAA513CE5BFA121EE22E5E134F554888F67.png)
    
    - 在工程根目录下使用命令行工具：
        1. 直接执行 **codelinter** 指令。此时根据默认codelinter检查规则，对该工程中的TS/ArkTS文件进行代码检查。默认的规则清单可在检查完成后，根据命令行提示，查看相应位置的code-linter.json5文件。
            
            1. codelinter // 进行codelinter检查
            
            ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155951.26646448726592715290448208059693:50001231000000:2800:1002668A8769CD75DE6AC6EB4CC8167E6A4BDCBEB4B308CD3964C99BC489D49D.png "点击放大")
            
        2. 执行如下命令，指定codelinter检查所使用的code-linter.json5规则配置文件，并进行代码检查。
            
            1. codelinter -c _filepath_ // 指定执行检查的规则配置文件位置
            
            ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155951.93023427235241843896653694124565:50001231000000:2800:DE25119808A8AC2BFBB4E0AA0554819B8F12DD568202135B14C665439C1E08FF.png "点击放大")
            
        3. 执行如下命令，对指定工程将根据指定的规则配置文件执行codelinter检查，并对部分支持修复的告警信息进行自动修复。
            
            1. _codelinter -c filepath_ --fix // 对工程中的告警进行修复
            
            ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155951.28013978339011225344267926988390:50001231000000:2800:DFDCB00A618D868059EA9B63F519E3CE0962B1345B68CAE8B74ACD92A128FA0B.png)
            
    - 在非工程根目录下使用命令行工具：
        1. 执行如下命令，指定需要进行检查的工程目录或文件路径。此时根据默认codelinter检查规则，对该工程中的TS/ArkTS文件进行代码检查。默认的规则清单可在检查完成后，根据命令行提示，查看相应位置的code-linter.json5文件。
            
            1. codelinter dir [filepath] [dir1] // 指定执行检查的工程目录或文件路径。支持同时配置多个文件/文件夹路径。 filepath为待检查的文件所在位置，dir、dir1指定待检查的工程目录
            
            ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155951.92082181040267259847164054577124:50001231000000:2800:365115D52E883888679CF4A317D332F767103F4829890D96ABE95E351E5737CD.png "点击放大")
            
        2. 在指定的工程目录下，根据指定的codelinter规则配置文件进行代码检查。
            
            1. codelinter -c _filepath_ dir // filepath为指定的规则配置文件所在位置，dir指定执行检查的工程根目录
            
        3. 执行如下命令，对指定工程重新执行codelinter检查，并对部分支持修复的告警进行自动修复。
            
            1. _codelinter -c filepath dir_ --fix // 对指定工程中的告警进行修复。支持配置同时多个工程路径
            
            ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155951.90568686333496935989737563835312:50001231000000:2800:0B40DC2AC87833AC8C6C184BEF8589A362F3666E16C891775679ABA61F3237F6.png "点击放大")
            
    
2. 如需指定检查结果输出格式（以json格式为例），执行如下指令。检查结果将在命令行窗口展示。
    
    1. codelinter [dir] -f json  //[dir]为待检查的工程根目录             
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155951.36932349804583367349844679921464:50001231000000:2800:BEB1C34183336C340CE0D78CD6FAFB3E7D484C8C5A7DF468A474D6745FE021CA.png)
    
3. 执行如下指令，指定代码检查输出格式及结果保存位置。此时将不在命令行窗口中打印检查结果，可在指定的文件存放路径下查看。
    
    1. codelinter [dir] -f json -o _filepath_2     // [dir]为待检查的工程根目录，_filepath_2为指定存放代码检查结果的文件路径           
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155952.09325742624366619486381160648944:50001231000000:2800:26586AF87A1ABC08E5F3F42A8D2193C5B48E02ED8A40CC33A4AA9FECA75AA0DA.png)
    # 堆栈解析工具（hstack）

更新时间: 2025-12-16 15:59

## 简介

hstack是为开发人员提供的用于将release应用混淆后的crash堆栈解析为源码对应堆栈的工具，支持Windows、Mac、Linux三个平台，关于堆栈解析的原理，请查看[异常堆栈解析原理](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-exception-stack-parsing-principle)。

hstack命令行格式为：

1. hstack [options]

options: 可选配置，请参考[表hstack命令行配置](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-command-line-hstack#table25697717185)。

**表1** hstack命令行配置
|指令|说明|
|:--|:--|
|-i/--input|可选，指定工程crash文件归档目录。|
|-c/--crash|可选，指定一条crash堆栈。|
|-o/--output|可选，指定解析结果输出目录（输入指定为-c时， -o参数指定一个输出文件）。|
|-s/--sourcemapDir|可选，指定工程sourcemap文件归档目录。|
|--so/--soDir|可选，指定工程shared object文件归档目录。|
|-n/--nameObfuscation|可选 ，指定工程nameCache文件归档目录。|
|-v/--version|查看hstack版本。|
|-h/--help|查询hstack命令行帮助。|

说明

- crash文件归档目录与crash堆栈必须且只能提供一项。
- sourcemap与shared object文件归档目录至少提供一项。
- 如果需要对方法名进行解析还原，则需要同时提供sourcemap与nameCache文件。
- 路径参数不支持以下特殊字符：`~!@#$^&*=|{};,\s\[\]<>?~！@#￥……&*（）——|{}【】‘；：。，、？

## 环境配置

1. hstack工具在Command Line Tools的bin目录下，需要[将bin目录配置到PATH变量中](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-commandline-get#section17776863449)。
2. 本工具依赖Node环境，需要[将Node.js配置到环境变量中](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-command-line-building-app#section159168531288)。
3. 如果需要对C++文件产生的异常进行解析，则需要将SDK中的native\llvm\bin目录配置到环境变量中，变量名设置为“ADDR2LINE_PATH”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155952.29725751215445894852790520873968:50001231000000:2800:0A0AB6D91C65ADF93E921DFE811831E01A00934840EC2FC9314F69852BDDBB56.png)
    

## 使用示例

1. 将应用产生的crash文件归档到crashDir目录下（或者-c指定一条crash堆栈），关于堆栈的获取方式请参考[崩溃检测](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/crash-detection-overview)。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155952.69212812996503736942497067015025:50001231000000:2800:221643F07B1F786D457CD1EFCCFCD78940E7625F6B51880D31035E79DC2AA7AD.png)
    
2. 使用-o指定输出目录，当不指定时，会输出至-i指定的crashDir目录下（通过-c输入为crash堆栈时，可以使用-o指定一个输出文件，或不指定，直接将结果输出至控制台）。
3. 使用-s指定工程对应sourcemap文件归档目录（可选，与shared object文件归档目录至少提供一项）。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155952.61652560845106822384687222672661:50001231000000:2800:C91049669919673671BB6EB0C1412FB85AEE7793A756049FEB1FBBAEE1E3E114.png)
    
4. 使用--so指定shared object文件归档目录（可选，与sourcemap归档目录至少提供一项）。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155952.02747291745044277659999367130588:50001231000000:2800:AA4D43222F5FF85CA61388737394350D9256A5315DAFEA212C7A44EB62388FE9.png)
    
5. 使用-n指定nameCache文件归档目录（可选）。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155952.75618045716295469142020513965216:50001231000000:2800:F50A0F302AB1E7198076693E4E40A0CA3FB35645609F748B66CD188204DF1432.png)
    
6. 执行以下命令，可将release应用crash堆栈解析为源码对应堆栈，并将解析结果输出至outputDir目录：
    
    1. hstack -i crashDir -o outputDir -s sourcemapDir --so soDir -n nameCacheDir
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155952.24559371315819545668625687273216:50001231000000:2800:55DC42313A0F0A02493284A2C06F80F97A84732FA594E145B6423EDBE2633EAD.png)
    
    解析完成后，outputDir目录下会生成对应的解析结果，文件以原始crash文件名加“_”前缀进行命名。crash堆栈中的C++日志以及ArkTS日志均已解析为源码对应的文件路径以及行列号，结果如下图所示：
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155952.48399194256154133213652536276910:50001231000000:2800:DC95337AFCC9B3AD70CCF7DE7E9EB1D778DA7E43D5BECB8356A55D9BAE639B2A.png)
    
    说明：在构建Release应用时，so文件是默认不包含符号表信息的，如果需要在构建Release应用时生成包含符号表的so文件，需要在工程的模块级build-profile.json5文件的buildOption属性中，配置如下信息：
    
    2. "buildOption": {
    3.   "externalNativeOptions": {
    4.     "arguments": "-DCMAKE_BUILD_TYPE=RelWithDebInfo"
    5.   }
    6. }
    

## 堆栈解析方案说明

以如下代码为例。

Entry模块通过独立har包形式引用har模块中的har方法：

1. import {har} from 'Har'
2. @Entry
3. @Component
4. struct Index {
5.   @State har: string = 'Har';
6.   build() {
7.     Row() {
8.       Column() {
9.         Text(this.har)
10.           .fontSize(50)
11.           .fontWeight(FontWeight.Bold)
12.           .onClick(() => {
13.             let entryClass = new EntryClass();
14.             entryClass.callHarFunction();
15.           })
16.       }
17.       .width('100%')
18.     }
19.     .height('100%')
20.   }
21. }

22. class EntryClass {
23.   callHarFunction() {
24.     har()
25.   }
26. }

27. @Component
28. export struct MainPage {
29.   @State message: string = 'Hello World';

30.   build() {
31.     Row() {
32.       Column() {
33.         Text(this.message)
34.           .fontSize(50)
35.           .fontWeight(FontWeight.Bold)
36.       }
37.       .width('100%')
38.     }
39.     .height('100%')
40.   }
41. }

42. export function har() {
43.   BigInt(1.1)
44. }

生成的crash如下：

1. at har (entry|har|1.0.0|src/main/ets/components/mainpage/MainPage.js:58:58)
2. at i (entry|entry|1.0.0|src/main/ets/pages/Index.ts:71:71)
3. at anonymous (entry|entry|1.0.0|src/main/ets/pages/Index.ts:55:55)

crash中，包含混淆后的方法名（或属性名）、路径信息以及混淆后的行列号信息，其中：

- 方法名在配置相应混淆规则后，会进行混淆处理（例如上述例子中EntryClass的callHarFunction被混淆为i）。方法名混淆前后的映射关系保存在对应模块编译产物的nameCache文件中。
- 路径信息格式为：引用方entry-packageName|被引用方packageName|version|源码相对路径，其中packageName以及version保存在对应模块编译产物的sourcemap文件中。
- 行列号混淆前后的映射关系保存在对应模块编译产物的sourcemap文件中，可利用文件对应的mappings字段进行解析还原。

在对堆栈进行还原时，可分为以下三步：

1. 根据路径信息，找到引用方模块sourcemap。例如第一条堆栈：
    
    1. at har (entry|har|1.0.0|src/main/ets/components/mainpage/MainPage.js:58:58)
    
    根据路径信息entry|har|1.0.0|src/main/ets/components/mainpage/MainPage.js，可在entry模块sourcemap文件中找到如下字段：
    
    2. "entry|har|1.0.0|src/main/ets/components/mainpage/MainPage.js": {
    3.     "version": 3,
    4.     "file": "MainPage.js",
    5.     "sources": [
    6.       "oh_modules/.ohpm/Har@ue9rwlwgmslvadnmypsedjcin6a=/oh_modules/Har/src/main/ets/components/mainpage/MainPage.js"
    7.     ],
    8.     "names": [],
    9.     "mappings": "AAAA,IAAA,CAAA,CAAA,sBAAA,IAAA,MAAA,CAAA,SAAA,CAAA,EAAA;IACA,OAAA,CAAA,GAAA,CAAA,MAAA,CAAA,SAAA,EAAA,sBAAA,EAAA,GAAA,EAAA,GAAA,CAAA,CAAA,CAAA;CACA;AACA,MAAA,OAAA,QAAA,SAAA,MAAA;IACA,YAAA,CAAA,EAAA,EAAA,EAAA,CAAA,EAAA,CAAA,GAAA,CAAA,CAAA,EAAA,CAAA,GAAA,SAAA,EAAA,CAAA;QACA,KAAA,CAAA,CAAA,EAAA,CAAA,EAAA,CAAA,EAAA,CAAA,CAAA,CAAA;QACA,IAAA,OAAA,CAAA,KAAA,UAAA,EAAA;YACA,IAAA,CAAA,gBAAA,GAAA,CAAA,CAAA;SACA;QACA,IAAA,EAAA,GAAA,IAAA,wBAAA,CAAA,aAAA,EAAA,IAAA,EAAA,SAAA,CAAA,CAAA;QACA,IAAA,CAAA,yBAAA,IAAA,CAAA;QACA,IAAA,CAAA,oBAAA,EAAA,CAAA;IACA,CAAA;IACA,yBAAA,CAAA,EAAA;QACA,IAAA,GAAA,OAAA,KAAA,SAAA,EAAA;YACA,IAAA,CAAA,OAAA,GAAA,GAAA,OAAA,CAAA;SACA;IACA,CAAA;IACA,eAAA,CAAA,CAAA;IACA,CAAA;IACA,iCAAA,CAAA,CAAA;QACA,IAAA,EAAA,CAAA,uBAAA,CAAA,CAAA,CAAA,CAAA;IACA,CAAA;IACA,gBAAA;QACA,IAAA,EAAA,CAAA,gBAAA,EAAA,CAAA;QACA,iBAAA,CAAA,GAAA,EAAA,CAAA,MAAA,CAAA,IAAA,CAAA,IAAA,EAAA,CAAA,CAAA;QACA,IAAA,CAAA,wBAAA,EAAA,CAAA;IACA,CAAA;IACA,IAAA,OAAA;QACA,OAAA,IAAA,EAAA,CAAA,GAAA,EAAA,CAAA;IACA,CAAA;IACA,IAAA,OAAA,CAAA,EAAA;QACA,IAAA,EAAA,CAAA,GAAA,IAAA,CAAA;IACA,CAAA;IACA,aAAA;QACA,IAAA,CAAA,yBAAA,CAAA,CAAA,CAAA,EAAA,EAAA,EAAA,EAAA;YACA,GAAA,CAAA,MAAA,EAAA,CAAA;YACA,GAAA,CAAA,MAAA,CAAA,MAAA,CAAA,CAAA;QACA,CAAA,EAAA,GAAA,CAAA,CAAA;QACA,IAAA,CAAA,yBAAA,CAAA,CAAA,CAAA,EAAA,CAAA,EAAA,EAAA;YACA,MAAA,CAAA,MAAA,EAAA,CAAA;YACA,MAAA,CAAA,KAAA,CAAA,MAAA,CAAA,CAAA;QACA,CAAA,EAAA,MAAA,CAAA,CAAA;QACA,IAAA,CAAA,yBAAA,CAAA,CAAA,CAAA,EAAA,CAAA,EAAA,EAAA;YACA,IAAA,CAAA,MAAA,CAAA,IAAA,CAAA,OAAA,CAAA,CAAA;YACA,IAAA,CAAA,QAAA,CAAA,EAAA,CAAA,CAAA;YACA,IAAA,CAAA,UAAA,CAAA,UAAA,CAAA,IAAA,CAAA,CAAA;QACA,CAAA,EAAA,IAAA,CAAA,CAAA;QACA,IAAA,CAAA,GAAA,EAAA,CAAA;QACA,MAAA,CAAA,GAAA,EAAA,CAAA;QACA,GAAA,CAAA,GAAA,EAAA,CAAA;IACA,CAAA;IACA,QAAA;QACA,IAAA,CAAA,mBAAA,EAAA,CAAA;IACA,CAAA;CACA;AACA,MAAA,UAAA,GAAA;IACA,MAAA,CAAA,GAAA,CAAA,CAAA;AACA,CAAA",
    10.     "entry-package-info": "entry|1.0.0",
    11.     "package-info": "har|1.0.0"
    12.   }
    
2. 利用对应sourcemap信息进行堆栈路径以及行列号还原：
    
    基于步骤1找到的sourcemap信息，根据sources及mappings字段进行解析，可以将路径以及行列号还原如下：
    
    1. at har (oh_modules/.ohpm/Har@ue9rwlwgmslvadnmypsedjcin6a=/oh_modules/Har/src/main/ets/components/mainpage/MainPage.js:58:58)
    
    该文件位于entry模块oh_modules路径下。
    
    如果对应sourcemap中包含package-info字段，则可以利用package-info中对应模块的sourcemap，对该条堆栈进行二次解析。例如该堆栈中包package-info为har|1.0.0，可利用har中的sourcemap对该堆栈进行再次解析，方案如下：
    
    2. 由路径中最后一个oh_modules起，向下两级，截断上述第一次解析结果路径，结果如下：
        
        1. src/main/ets/components/mainpage/MainPage.js
        
    3. 上述路径拼接package-info， 拼接方式为：packageName|packageName|version|截断路径，得到拼接路径如下：
        
        1. har|har|1.0.0|src/main/ets/components/mainpage/MainPage.js
        
    4. 利用拼接后的路径，在har模块sourcemap文件中找到如下字段：
        
        1. "har|har|1.0.0|src/main/ets/components/mainpage/MainPage.js": {
        2.   "version": 3,
        3.   "file": "MainPage.ets",
        4.   "sources": [
        5.     "har/src/main/ets/components/mainpage/MainPage.ets"
        6.   ],
        7.   "names": [],
        8.   "mappings": ";;;AAEA,MAAA,OAAA,QAAA,SAAA,MAAA;IADA,YAAA,CAAA,EAAA,CAAA,EAAA,CAAA,EAAA,IAAA,CAAA,CAAA,EAAA,IAAA,SAAA,EAAA,CAAA;;;;;;;;IADyB,CAAA;;;;;;;;;;;;;;;;;;;;;;IAKvB,aAAA;;;;;;;;;;;;YAGM,IAAA,CAAA,UAAA,CAAA,UAAA,CAAA,IAAA,CAAA,CAAA;;;;;IAOL,CAAA;;;;;AAGH,MAAA,UAAA,GAAA;;AAEA,CAAA",
        9.   "entry-package-info": "har|1.0.0"
        10. }
        
    5. 根据该sourcemap的sources及mappings字段进行再次解析，可得到该堆栈对应的源码信息为：
        
        1. at har (har/src/main/ets/components/mainpage/MainPage.ets:20:1)
        
    
3. 利用nameCache文件，对方法名进行解析还原。
    
    以第二条堆栈为例：
    
    1. at i (entry|entry|1.0.0|src/main/ets/pages/Index.ts:71:71)
    
    通过步骤1与步骤2，将该堆栈路径以及行列号信息进行解析，结果如下：
    
    2. at i (entry/src/main/ets/pages/Index.ets:25:3)
    
    在对应模块编译产物中的nameCache文件中，通过解析后的文件路径找到如下字段：
    
    3. "entry/src/main/ets/pages/Index.ets": {
    4.   "IdentifierCache": {
    5.     "Index#initialRender#__function": "o",
    6.     "Index#initialRender#$2#__function": "t",
    7.     "Index#initialRender#$2#$0#entryClass": "u",
    8.     "$0#__function": "a1"
    9.   },
    10.   "MemberMethodCache": {
    11.     "initialRender:6:20": "initialRender",
    12.     "callHarFunction:24:26": "i"
    13.   },
    14.   "obfName": "entry/src/main/ets/pages/Index.ets"
    15. }
    
    该字段的IdentifierCache与MemberMethodCache中保存了方法名混淆前后的映射关系，对应格式为：
    
    "源码方法名:该方法起始行号:该方法结束行号":"混淆后方法名"。
    
    第二条堆栈混淆后的方法名为"i"，利用上述字段对该方法名进行还原：
    
    16. 在上述字段中找出所有混淆后方法名为"i"的条目，可能存在多个，该字段中为：
        
        1. "callHarFunction:24:26": "i"
        
    17. 找到行号范围包含步骤2中还原后行号的条目，根据步骤2得到还原后的行号为25，包含在24-26之内，因此可以得到源码对应方法名为"callHarFunction"。
    
    通过上述方式，可以得到源码的方法名。
    
4. 步骤2与步骤3所得结果进行整合，得到最终堆栈结果如下：
    
    1. at har (har/src/main/ets/components/mainpage/MainPage.ets:20:1)
    2. at callHarFunction (entry/src/main/ets/pages/Index.ets:25:3)
    3. at anonymous (entry/src/main/ets/pages/Index.ets:14:47)
    

通过上述方式，即可利用编译产物对release应用的crash信息进行解析还原。
# 命令行构建工具（hvigorw）

更新时间: 2025-12-16 15:59

hvigorw作为Hvigor的wrapper包装工具，支持自动安装Hvigor构建工具和相关插件依赖，以及执行Hvigor构建命令。

执行命令前，需要先配置JDK，配置Node.js、hvigor等环境变量，具体请参考[搭建流水线](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-command-line-building-app)。

## 命令行使用方式

hvigorw命令行格式为：

1. hvigorw [taskNames...] <options>

其中taskNames是任务，可同时执行多个任务，options是可选参数，具体的任务和可选参数请参考[常用命令](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-commandline#section16300629103)。

说明

从hvigorw 5.18.4版本开始，以下命令支持在任意路径下执行，其他hvigorw命令需要在工程根目录下执行。

- hvigorw -v
- hvigorw --version
- hvigorw version
- hvigorw -h
- hvigorw --help

## 常用命令

常见的任务和参数如下，更多任务请参考[任务详细说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-task-process#section196919100414)。

### 查询

|**参数**|说明|
|:--|:--|
|-h, --help|打印hvigorw的命令帮助信息。|
|-v, --version, version|打印hvigorw版本信息。|

### 编译构建

|任务|说明|
|:--|:--|
|clean|清理构建产物build目录。|
|collectCoverage|基于打点数据生成覆盖率统计报表。|
|assembleHap|构建Hap应用。|
|assembleApp|构建App应用。|
|assembleHsp|构建Hsp包。|
|assembleHar|构建Har包。|

编译构建命令行常用扩展参数：

|参数|说明|
|:--|:--|
|-p buildMode={debug \| release}|采用debug/release模式进行编译构建。<br><br>缺省时：构建Hap/Hsp/Har时为debug模式，构建App时为release模式。<br><br>关于构建模式的详细说明，请参考[指定构建模式](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-compilation-options-customizing-guide#section192461528194916)。针对HAR构建，请参考[构建HAR](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-har)。|
|-p debuggable=true/false|该配置会覆盖构建模式中对应的buildOption中的debuggable配置。<br><br>关于debuggable的合并优先级，请参考[合并编译选项规则](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-compilation-options-customizing-guide#section1727865610255)。|
|-p product={ProductName}|指定product进行编译, 编译product下配置的module target。<br><br>缺省时：默认为default。|
|-p module={ModuleName}@{TargetName}|指定模块及target进行编译，可指定多个相同类型的模块进行编译以逗号分割；TargetName不指定时默认为default。<br><br>限制：此参数需要与--mode module参数搭配使用。<br><br>缺省时：执行AssembleHap任务会编译工程下所有模块，默认指定target为default。|
|-p ohos-test-coverage={true \| false}|执行测试框架代码覆盖率插桩编译。|
|-p coverage={true \| false}|
|-p parameterFile=param.json/json5|设置oh-package.json5文件的参数配置文件，其中"param"可自行修改为对应配置文件名称。详细使用请参考[parameterFile](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-oh-package-json5#section122411462820)。|

测试相关的命令行：

|命令行|说明|
|:--|:--|
|hvigorw onDeviceTest -p module={moduleName} -p coverage={true \| false} -p scope={suiteName}#{methodName} -p ohos-debug-asan={true\|false}|通过命令行方式执行Instrument Test。<br><br>- module：执行测试的模块，缺省默认是执行所有模块的用例。HAP/HAR/HSP模块都支持。<br>- coverage：是否需要覆盖率报告，缺省默认为true。<br>- scope：格式为{suiteName}#{methodName}或{suiteName}，分别表示测试用例级别或测试套件级别的测试，缺省默认是执行当前模块的所有用例。<br>- ohos-debug-asan：是否启用ASan检测，缺省默认是false。从hvigorw 5.19.0版本开始支持。<br><br>多个module和scope之间用逗号分隔。<br><br>- 覆盖率测试报告路径：<module-path>/.test/default/outputs/ohosTest/reports<br>- 测试结果文件：path_to_project/module_name/.test/default/intermediates/ohosTest/coverage_data/test_result.txt<br>- ASan日志路径：<module-path>/.test/default/intermediates/ohosTest/coverage_data|
|hvigorw test -p module={moduleName} -p coverage={true \| false} -p scope={suiteName}#{methodName}|通过命令行方式执行Local Test。暂不支持在Linux上执行该命令。<br><br>- module：执行测试的模块，缺省默认是执行所有模块的用例。HAP/HAR/HSP模块都支持。<br>- coverage：是否需要覆盖率报告，缺省默认为true。<br>- scope：格式为{suiteName}#{methodName}或{suiteName}，分别表示测试用例级别或测试套件级别的测试，缺省默认是执行当前模块的所有用例。<br><br>多个module和scope之间用逗号分隔。<br><br>- 覆盖率测试结果文件：<br>    <br>    <module-path>/.test/default/outputs/test/reports<br>    <br>- 测试结果文件：path_to_project/module_name/.test/default/intermediates/test/coverage_data/test_result.txt|

### 日志

|参数|说明|
|:--|:--|
|-e, --error|设置hvigor的日志级别为error。|
|-w, --warn|设置Hvigor的日志级别为warn。|
|-i, --info|设置Hvigor的日志级别为info。|
|-d, --debug|设置Hvigor的日志级别为debug。|
|--stacktrace，--no-stacktrace|Hvigor默认使能关闭打印所有异常的堆栈信息，如需开启在命令行后添加该选项。|

### 可视化

|参数|说明|
|:--|:--|
|--analyze=normal|在DevEco Studio中开启Build Analyzer构建分析，设置为普通模式，通过简单打点数据进行分析。|
|--config properties.hvigor.analyzeHtml=true|在工程的.hvigor/report目录下生成构建可视化html文件，该文件可直接在浏览器中打开。|
|--analyze=false|不启用Build Analyzer构建分析。|
|--analyze=advanced|启用Build Analyzer构建分析，并设置为进阶模式，通过更加详细的打点数据进行分析。如果需要更详细的任务耗时数据，请选择该模式。|
|--analyze=ultrafine|启用Build Analyzer构建分析，并设置为超精细化模式，与advanced模式相比，在ArkTS编译阶段记录更详细的打点数据，但开启后可能导致编译构建时间更长。<br><br>从hvigorw 6.0.0版本开始支持。|
|--analyze|同--analyze=normal命令。<br><br>从hvigorw 4.3.0开始废弃，请使用--analyze=normal替换。|
|--no-analyze|同--analyze=false命令。<br><br>从hvigorw 4.3.0开始废弃，请使用--analyze=false替换。|
|--verbose-analyze|同--analyze=advanced命令。<br><br>从hvigorw 4.3.0开始废弃，请使用--analyze=advanced替换。|

### daemon

|参数|说明|
|:--|:--|
|--daemon|启用[守护进程](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-daemon)。|
|--no-daemon|Hvigor默认启用守护进程，如需关闭，可在命令行后添加该选项。<br><br>命令行模式下推荐使用此参数。|
|--stop-daemon|关闭当前工程的守护进程。|
|--stop-daemon-all|关闭所有工程的守护进程。|
|--status-daemon|查询当前环境中所有的Hvigor守护进程信息。|
|--max-old-space-size=12345|设置守护进程最大的老生代内存大小为12345MB。|
|--max-semi-space-size=32|设置守护进程新生代内存最大的半空间大小为32MB。<br><br>该参数从hvigorw 5.18.4版本开始支持。|

### 性能/内存

|参数|说明|
|:--|:--|
|--parallel, --no-parallel|Hvigor默认开启[并行构建](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-improve-performance)能力，如需关闭在命令行后添加--no-parallel。|
|--incremental, --no-incremental|Hvigor默认开启[增量构建](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-incremental-build)能力，如需关闭在命令行后添加--no-incremental。|
|--optimization-strategy=performance|设置构建模式为性能优先模式，可加快构建速度，但会占用更多内存。<br><br>从hvigorw 5.19.2版本开始支持。|
|--optimization-strategy=memory|设置构建模式为内存优先模式，可以减少编译内存占用，默认使用memory。<br><br>从hvigorw 5.19.2版本开始支持。|

### 公共命令

|任务|说明|
|:--|:--|
|tasks|打印工程各模块包含的任务信息。|
|taskTree|打印工程各模块的任务依赖关系信息。|
|prune|清除30天内未使用的Hvigor缓存文件并从pnpm存储中删除未引用的包。|
|buildInfo|打印工程级或模块级build-profile.json5中的配置信息，包含product、module、target、buildMode、buildOption，以树状结构输出。<br><br>该功能从hvigorw 5.18.4版本开始支持。|

buildInfo命令扩展参数：

|参数|说明|
|:--|:--|
|-p module={ModuleName}|指定需要打印配置信息的模块名，不指定时会打印工程级的配置信息。|
|-p buildOption|命令包含此参数时会打印buildOption配置，不含此参数时将不会展示buildOption配置，输出的buildOption优先级请参考[合并编译选项规则](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-compilation-options-customizing-guide#section1727865610255)。|
|-p json|将输出结果以json格式展示。|

### 其他命令

|参数|说明|
|:--|:--|
|-s,--sync|处理并持久化Hvigor部分工程信息到工程./hvigor/outputs/sync/output.json中。|
|-m,--mode|在对应的目录执行相应的task，例hvigorw clean -m project在工程目录下执行build目录清理（即清理工程级别的build文件夹）。|
|--enable-build-script-type-check|使能工程中hvigorfile.ts的类型检查，该字段已废弃，请使用--type-check替换。|
|--type-check, --no-type-check|Hvigor默认使能关闭工程中hvigorfile.ts的类型检查，如需开启，可在命令行后添加该选项。|
|--no-pnpm-frozen-lockfile，--pnpm-frozen-lockfile|Hvigor默认使能不忽略pnpm-lock.yaml文件，如需开启，可在命令行后添加该选项。<br><br>忽略pnpm-lock.yaml文件，按照hvigor-config.json5的配置安装Hvigor插件的依赖（如果不忽略pnpm-lock.yaml文件，在使用Hvigor 2.0.0及以上版本的CI场景下安装Hvigor插件依赖时将报错）。<br><br>说明<br><br>该命令在4.1 Release及以上版本中已废弃。在CI场景中将自动配置，无需开发者手动配置。|
|--config, -c|指定hvigor-config.json5配置文件中的参数。<br><br>当前仅支持设置properties里的参数，具体支持的参数请查看[hvigor-config.json5文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-set-options)中properties支持的参数。<br><br>--config properties.key=value 同 -c properties.key=value|
|--watch|使能观察模式，主要用于预览和热加载场景。|
|--generate-build-profile, --no-generate-build-profile|已废弃。使能生成BuildProfile.ets文件。|
|--node-home <string>|指定nodejs路径。|
# 系统平台要求

更新时间: 2025-12-16 15:59

ohpm支持在Windows、macOS、Linux操作系统下使用。

ohpm通过软链接或符号链接的方式构建依赖关系。不同操作系统需满足如下要求：

**Windows：**

- 工程代码文件所在文件系统类型需为NTFS（Windows系统下默认为NTFS）；
- 使用源码依赖时，依赖的源码模块与被依赖的源码模块需要在同一个盘符下，不允许配置跨盘符依赖。

**macOS**：

工程代码文件所在文件系统类型需为APFS（macOS系统下默认为APFS）。

如在macOS上挂载了其他不支持符号链接的文件系统（如FAT32或exFAT），则无法在其上创建符号链接。

**Linux**：

EXT4、Btrfs、XFS、ZFS等常见Linux文件系统类型均满足要求。

部分较老或简单的文件系统（不支持符号链接），可能存在无法在其上创建或正确解析软链接的情况。
# ohpmrc

更新时间: 2025-12-16 15:59

ohpm配置文件。

## 描述

ohpm从命令行和.ohpmrc文件中获取其配置内容。ohpm config命令可用于修改用户级.ohpmrc文件的内容。

## 文件

- 项目级配置文件：/path/to/my/project/.ohpmrc
- 用户级配置文件：~/.ohpm/.ohpmrc
- 所有 ohpm 配置文件均是 ini 格式：<key>= <value> 的参数列表

注意

- 命令行工具会优先读取项目级的配置文件。如果缺少某些配置项，将从用户级配置文件中读取缺失的配置项信息。
- 在工程任意子目录下执行ohpm命令，都可以读取到项目级的.ohpmrc配置。

## 注释

.ohpmrc 文件中以"#"或";"字符为注释符。

## 更新配置

执行如下命令可设置用户级配置：

1. ohpm config set key value

## 默认配置项

|**配置项**|**字段名称**|**字段说明**|**字段类型**|**默认值**|**备注**|
|:--|:--|:--|:--|:--|:--|
|**仓库设置**|registry|下载仓库|字符串|https://ohpm.openharmony.cn/ohpm/|支持配置多个仓库地址，以英文逗号分隔。系统将按照配置的先后顺序依次检索这些仓库，直到成功下载目标包。例如：当需要下载包a时，会优先从第一个配置的仓库地址查找，若未找到则自动尝试下一个仓库，依此类推。|
|@group:registry|指定仓库|字符串|""|根据group指定组织的仓库地址。支持配置多个仓库地址，以英文逗号间隔，且优先级大于registry配置，系统将按照配置的先后顺序依次检索这些仓库，直到成功下载目标包。|
|**发布设置**|publish_registry|发布仓库|字符串|https://ohpm.openharmony.cn/ohpm/|配置发布的仓库地址，仅支持配置一个仓库地址。|
|publish_id|用户发布号|字符串|""|用户发布号，用来发布三方库，全局唯一。|
|**路径设置**|cache|缓存路径|字符串|~/.ohpm/cache|-|
|key_path|私钥路径|字符串|""|利用ssh-keygen工具生成的私钥的放置路径地址。|
|crypto_path|加密组件路径|字符串|""|加密组件路径地址。详情请见：[crypto_path](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpmrc#section18322038185010)。|
|**网络设置**|no_proxy|不使用proxy代理|字符串|""|配置不使用代理的仓库地址，可配置多个，以英文逗号间隔；值可以是域名或者ip，支持二级域名通配符*（例如：*.huawei.com）。|
|http_proxy|http代理|字符串|""|支持用户名和密码的网络代理，特殊字符需要转义。示例：http://proxy_server:port、http://username:password@proxy_server:port。|
|https_proxy|https代理|字符串|""|支持用户名和密码的网络代理，特殊字符需要转义。示例：https://proxy_server:port、http://username:password@proxy_server:port。|
|strict_ssl|ssl校验|布尔|true|默认值为true，校验https证书；若配置为false，则不校验https证书。|
|ca_files|ca证书路径|字符串|""|strict_ssl=true时校验服务端证书需要的ca证书放置路径，可以放置多个证书路径，以英文逗号间隔。详情请见：[CA证书获取及配置](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpmrc#zh-cn_topic_0000001792216397_ca%E8%AF%81%E4%B9%A6%E8%8E%B7%E5%8F%96%E5%8F%8A%E9%85%8D%E7%BD%AE)。|
|fetch_timeout|请求超时时间|数值|60000|取值范围：[10000，360000]，单位为毫秒。如果设置的fetch_timeout值不在取值范围内，则默认为：60000。|
|**并发设置**|max_concurrent|最大并发量|数值|50|取值范围：[1, 200]，设置每个模块在安装时允许的最大并发量。|
|retry_times|出错重试次数|数值|1|取值范围：[0, 5], 针对白名单内的异常，程序会按配置重试指定次数，白名单有：<br><br>- ECONNRESET：连接被对端重置<br>- ECONNREFUSED：连接被服务器拒绝<br>- ETIMEDOUT：连接超时<br>- RESPONSETIMEOUT：响应超时<br>- TARBADARCHIVE：包格式异常|
|retry_interval|出错重试间隔时间|数值|1000|取值范围：[1000, 60000], 单位毫秒。|
|**依赖冲突设置**|resolve_conflict|开启自动解决依赖版本冲突功能|布尔|true|默认开启。当设置为true或缺省时，ohpm会自动处理依赖版本冲突，详情请见：[resolve_conflict](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpmrc#section368717475562)。|
|resolve_conflict_strict|开启严格模式依赖冲突处理功能|布尔|false|默认关闭。当设置为true时，ohpm会按照严格模式处理依赖版本冲突，详情请见：[resolve_conflict_strict](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpmrc#section1942983310492)。|
|**安全设置**|key_passphrase|已加密的私钥密码|字符串|""|默认为空，使用加密命令将私钥密码加密，执行涉及公私钥的认证命令时，自动使用key_passphrase对私钥文件进行解密，无需用户手动输入私钥密码。详情请见：[key_passphrase](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpmrc#section10698175182316)。|
|**其他设置**|log_level|日志级别|字符串|info|可设置日志输出级别，对应级别类型有debug、info、warn、error。详情请见：[log_level](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpmrc#section1539817345376)。|
|install_all|是否安装工程所有模块的依赖|布尔|true|默认为true。当设置为true或缺省时，在执行ohpm install、ohpm update、ohpm uninstall时，将会安装工程下所有模块的依赖。详情请见[install_all](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpmrc#section1260011476535)。|
|:_auth和:_read_auth|AccessToken配置项|字符串|无|ohpm-repo支持使用access token进行认证。详情请见[AccessToken](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpmrc#section74219299467)。|
|enforce_dependency_key|开启依赖名称校验|布尔|false|默认为false。设置为true后，ohpm会校验配置的本地依赖名称与其对应的包名是否一致，若不一致会导致命令执行失败。详情请见[enforce_dependency_key](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpmrc#section920325116547)。|
|ensure_dependency_include|开启依赖扫描功能|布尔|false|默认为false。从ohpm 1.7.0开始，在执行ohpm publish命令时，会检查发布包的源码中，静态导入的三方依赖是否都声明在oh-package.json5的dependencies或dynamicDependencies中。若缺少依赖声明且字段设置为false时，会提示相应告警信息；设置为true时，则会使命令执行失败并提示错误信息。详情请见[ensure_dependency_include](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpmrc#section1291814578276)。|
|projectPackageJson:<project_root>|工程oh-package.json5配置覆盖|字符串|无|用于覆盖工程根目录下oh-package.json5中的配置。<br><br>- 配置项名称中的<project_root>表示工程根目录路径（根据实际情况替换为真实的工程根目录路径）。<br>- 配置项的值为指定的工程级oh-package.json5文件的路径，支持使用相对路径（当使用相对路径时，根路径为<project_root>）。<br><br>详情请见[.ohpmrc中projectPackageJson配置](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-oh-package-json5#section140251819254)。|
|disallow_nested_package|开启包内.har/.tgz依赖<br><br>配置路径检测|布尔|false|默认为false。设置为true后，在执行prepublish/publish时，会扫描包内是否存在'./'形式配置且后缀为.har/.tgz格式的依赖，如果存在，则会使命令执行失败并提示报错信息。详情见[disallow_nested_package](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpmrc#section1237023983514)。|
|odm_r2_project_root|开启overrideDependencyMap中相对路径自动转换功能|布尔|false|默认为false。设置为true后，当存在overrideDependencyMap配置且其配置项对应的配置文件内存在相对路径的依赖配置时，ohpm会基于工程根路径解析来查找这些相对路径。详情见[odm_r2_project_root](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpmrc#section136621053184912)。|
|enable_cross_process_lock|启用跨进程锁|布尔|false|默认为false。由于oh_modules目录结构限制，ohpm不支持在同一个工程下并行运行多个ohpm install、ohpm update或ohpm uninstall命令，若需要在同一个工程下执行多个ohpm install、ohpm update或ohpm uninstall命令，则必须将该配置设置为true，以保证这多个命令以串行的方式运行。|
|compability_log_level|兼容性字段检测日志等级|字符串|warn|默认为warn。在执行prepublish、publish命令时，ohpm会检测oh-package.json5文件中是否配置了兼容性检测需要的所有字段（'compatibleSdkVersion', 'compatibleSdkType', 'obfuscated', 'nativeComponents'），如果未配置，则会根据日志等级打印提示或报错。详情请见[compability_log_level](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpmrc#section96369529419)。|
|use_stream_threshold_size|流式上传阈值|数值|5|取值范围：[0, 300]，单位mb。当publish三方库的文件体积大于此阈值时将会使用流式上传三方库，如果仓库不存在流式上传接口则自动转为Base64方式上传。|
|lockfile_stable_order|oh-package-lock.json5内容稳定排序|布尔|false|默认为false。若设置为true，会确保在oh-package.json5文件未变更时，当前已生成的oh-package-lock.json5各字段内容不变。|
|enable_unified_lockfile|lockfile合一|布尔|false|默认为false。若设置为true，会将所有模块的oh-package-lock.json5文件整合进项目下的oh-package-lock.json5。详情请见[enable_unified_lockfile](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpmrc#section101671095818)。|
|enable_boost_extraction_speed|文件解压提速|布尔|false|默认为false。若设置为true，在ohpm安装时，会使用更高效的文件解压方法，该功能当前处于实验阶段，详情请见[enable_boost_extraction_speed](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpmrc#section20410165616573)。|
|enable_lock_inner_pkg_version|依赖内部的.har或.tgz依赖版本锁定|布尔|true|默认为true。若设置为false，在ohpm安装时，不会将依赖内部的.har或.tgz子依赖的版本保存至oh-package-lock.json5，详情请见[enable_lock_inner_pkg_version](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpmrc#section1834543398)。|
|case_sensitive_check|路径大小写敏感检测|布尔|false|默认为false。若设置为true，在执行ohpm相关命令时，如果ohpm检测到工程中文件的配置路径和文件的实际路径存在大小写不一致问题时，则会报错提示开发者修改，详情请见[case_sensitive_check](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpmrc#section2045412394117)。<br><br>该配置项仅在Windows环境下生效。|

## CA证书获取及配置

说明

CA证书的获取需要区分系统：当从Windows系统浏览器下载的证书仅适用于Windows系统，当从Mac系统浏览器中获取的证书适用于Mac系统和Linux系统。

### Windows系统获取CA证书

依次访问以下证书下载地址，并根据下图操作下载CA证书到本地：

1. https://ohpm.openharmony.cn/
2. https://contentcenter-drcn.dbankcdn.cn/   //该域名用于文件资源下载，访问根路径仅可用于获取CA证书

访问https://ohpm.openharmony.cn/地址，下载证书，请选择保存类型为**证书链**（访问https://contentcenter-drcn.dbankcdn.cn/ 执行相同操作）。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155953.77219164142214615307381268763192:50001231000000:2800:E0C59E43A0A76F859F913C258724AD09538005B69BB7236579C557A2E8979F59.png "点击放大")

通过访问https://ohpm.openharmony.cn/地址获取证书openharmony.cn.crt，通过访问https://contentcenter-drcn.dbankcdn.cn/地址获取证书update.hicloud.crt，在 .ohpmrc 文件中配置 ca_files=证书路径1，证书路径2（两个文件均需配置）。

1. ca_files=D:\_.openharmony.cn.crt,D:\update.hicloud.crt

### Mac系统获取CA证书

依次访问以下证书下载地址，并根据下图操作下载CA证书到本地：

1. https://ohpm.openharmony.cn/
2. https://contentcenter-drcn.dbankcdn.cn/   //该域名用于文件资源下载，访问根路径仅可用于获取CA证书

访问https://ohpm.openharmony.cn/地址，下载证书，请选择保存类型为**证书链**（访问https://contentcenter-drcn.dbankcdn.cn/ 执行相同操作）。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155953.21781995384171487932495859771834:50001231000000:2800:4F9D76DF62EBF7D9F37B1C57490A9A3031543F30EB80FCCBDD280364FF103CC3.png "点击放大")

通过访问https://ohpm.openharmony.cn/地址获取证书openharmony.cn.pem，通过访问https://contentcenter-drcn.dbankcdn.cn/地址获取证书update.hicloud.pem，在 .ohpmrc 文件中配置 ca_files=证书路径1，证书路径2（两个文件均需配置）。

1. ca_file=/Users/用户名/_.openharmony.cn.pem,/Users/用户名/_.update.hicloud.pem

## log_level

可设置ohpm日志输出级别，对应级别类型有debug、info、warn、error，默认为：info。开发者在执行ohpm命令时，不同日志级别的区别和效果如下所示。

- debug：控制台会打印debug、info、warn、error日志。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155953.35314045563548143540588210754174:50001231000000:2800:D79B776EA13A1F1B4F682BC6A8EF6CA37B8CA4B4C75CBFCAFB81FB43A4F4DE29.png)
    
- info：控制台会打印info、warn、error日志。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155953.83731292759443589841949499164680:50001231000000:2800:18E729F2D5214075BDFAEF26DFC5C63922494C565D8B4E34D9E279530C45633B.png)
    
- warn：控制台会打印warn、error日志。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155953.73602188277849061697064024271188:50001231000000:2800:0CF150FC9BA9C9B78266DF66D1EA911B9C13D62C3E884AA7307515D7B71A9ECE.png)
    
- error：控制台只会打印error日志。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155953.53750406505987902354089299669721:50001231000000:2800:6C751194041DC2E80EF5D8E4CA4DB87814FC148D48714FC9C2F0B612DB01BBAD.png)
    

## install_all

在ohpm客户端1.8.0版本的.ohpmrc中支持install_all配置，用于控制ohpm install，ohpm update，ohpm uninstall的行为，install_all在.ohpmrc文件中设置为true或缺省时：

- 使用ohpm install命令时，将安装工程下所有模块的依赖，与使用ohpm install --all行为一致；
- 使用ohpm update时，将默认更新本模块下依赖并安装工程下所有模块的依赖，与使用ohpm update --all一致；
- 使用ohpm uninstall时，将默认删除本模块下依赖并安装工程下所有模块的依赖，与使用ohpm uninstall --all一致。

## resolve_conflict

在ohpm客户端1.5.0版本开始支持依赖版本冲突自动解决功能。只需要在.ohpmrc文件中，将resolve_conflict配置为true或缺省，即可开启该功能。依赖冲突的处理策略为：当您的项目同时依赖了某个三方库的不同版本时，ohpm将选择其中的最高版本进行安装。

注意

若某个三方库同时存在远程版本和本地版本（本地文件或源码依赖），无论本地版本的版本号是否大于远程版本，ohpm的冲突处理策略都会优先选择本地版本作为待安装的版本。

### 模块内依赖版本冲突

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155953.64388809398681279158721674335472:50001231000000:2800:9DA39FFD91268CDD4B4CB8C980FDC4C2389AC6797D8BDDACE223B1029A74D71E.png)

如上图所示的依赖路径中，moduleA 为您正在开发的模块，其直接依赖为 B@1.1，C@1.1。其中 B@1.1 与 C@1.1 分别依赖了 D 的两个版本 D@1.2 与 D@1.3。当您开启了依赖版本冲突自动解决功能，ohpm将会选择 D@1.3 版本作为待安装的版本，最终依赖路径被解析为下图蓝色箭头所指向的路径：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155953.29837892013001855828031684886575:50001231000000:2800:57B88E871F58698B622FDAA5CF44EFBA57B4CD1D0683144F6FBF16C2882A632F.png)

### 模块间依赖版本冲突

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155953.04505314555346381771808012629741:50001231000000:2800:9485C5BC3D5C8B5CD25FAE50705092FF4AAD4FD350D1C4609A7365AEF81F331D.png)

如上图所示的依赖路径中，moduleA、moduleB 为您同一项目下正在开发的两个模块，其中moduleA 依赖 B@1.1，moduleB 依赖 C@1.1，B@1.1 与 C@1.1 分别依赖了 D 的两个版本 D@1.2 与 D@1.3。当您开启了依赖版本冲突自动解决功能，并且您是使用 ohpm install --all 进行安装时，ohpm将会选择 D@1.3 版本作为待安装的版本，最终依赖路径被解析为下图蓝色箭头所指向的路径：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155954.29702194200427301154834466262212:50001231000000:2800:CFA8E10FF48CC28BDDFA4232CE7DBF7FC613D1AB9470EF7356D56F54E195EA58.png)

### 更新依赖版本的场景

当您希望将您某个模块的直接依赖更新成另一个版本，如下图所示，您手动将 C@1.1 更新为 C@1.2：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155954.30105683227265746725105406819609:50001231000000:2800:25C588637F226C090F409A30E1E2C447E857756E173FAA27BCE4998DB4273472.png)

由于 C 更新为 C@1.2 后，不再依赖 D，若依赖 D 的版本在更新 C 版本之前已经通过 ohpm 的自动冲突处理机制锁定为 D@1.3 版本，此时 C 版本的升级将不会导致 D 的版本由 D@1.3 回退为 D@1.2，这样可以保证每一次更新都只是在上一次结果上进行影响最小的修改，最终的依赖路径将会被解析为下图蓝色箭头所指向的路径：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155954.74967113550382512201994895590266:50001231000000:2800:C9385AC965C122187B3B9CBD82E663EFBCE2BBC89ABD42FEB56336A948598238.png)

对于上述场景，如果希望D版本同时也回退至D@1.2版本，则需要在ohpm install之前执行ohpm clean命令清理各模块下的oh-package-lock.json5文件，以消除上一次安装结果的影响。

### ohpm install命令带--target_path选项时依赖冲突处理

target_path下是hvigor在构建时根据目标产物target为各模块自动生成定制的依赖配置文件（oh-package.json5），详见[target_path](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-install#section79331822125611)。在生成的oh-package.json5中，依赖的版本部分可能包含targetName，示例："version": "1.0.0+targetName"。

包含targetName信息的版本完整格式为：<major>.<minor>.<patch>[-<pre-release>][+<targetName>]，此时冲突处理规则如下：

1、<major>.<minor>.<patch>[-<pre-release>]部分的比较规则依然遵循上文各场景所描述的处理规则，即取版本号最大的依赖。

2、当两个版本<major>.<minor>.<patch>[-<pre-release>]部分一致时，取尾部有[+<targetName>]信息的依赖。

注意

1、当两个版本尾部均有[+<targetName>]信息，且targetName不一致时，会根据<target_path>/dependencyMap.json5中targetName是否为空进行区分处理。

- 当targetName空时，打印警告提示。
- 当targetName有值时，报错提示并中断程序。

2、当两个依赖中有一个是本地依赖时，优先取本地依赖；当两个依赖均是本地依赖时，获取本地依赖包内oh-package.json5配置的version再次按照上述规则继续比较。

### 限制条件说明

1. 若希望解决当前项目所有模块下的依赖版本冲突，请使用ohpm install --all完成依赖安装。
2. 若在执行ohpm update或ohpm uninstall命令后，可能会破坏项目原有的依赖版本冲突处理结果。请额外执行一次ohpm install --all命令，重新处理当前项目所有模块下的依赖版本冲突。
3. 当本地文件（.har或.tgz后缀）依赖之间、本地源码模块依赖之间、本地文件（.har或.tgz后缀）依赖与本地源码模块依赖之间出现冲突时，ohpm自动冲突处理机制会比较该依赖内部oh-package.json5文件中version字段配置的版本号大小，版本号大的将会被安装。
    
    注意
    
    如难以感知本地文件或本地源码依赖中的版本号，建议使用[overrides](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-oh-package-json5#zh-cn_topic_0000001792256137_overrides)来处理冲突。
    

## resolve_conflict_strict

ohpm客户端从5.0.9版本，开始支持严格的依赖版本冲突处理机制。在.ohpmrc文件中，将resolve_conflict_strict配置为true开启该功能。

严格模式下，当您的项目同时依赖了某个三方库的不同版本时，ohpm将按照严格模式冲突决策算法决策出最符合要求的版本进行安装，当程序不能决策出符合要求的版本时将报错。

### 严格模式冲突决策算法

- 同一依赖，存在一个固定版本（如：1.0.1）、多个范围版本（如：^1.0.0、~1.1.0、>1.0.0等）时，如果该固定版本在所有范围版本交集区间内，则最终安装该固定版本，否则冲突决策失败；
- 同一依赖，仅存在多个范围版本时，如果所有范围版本存在交集，则最终安装仓库中存在且在交集区间内的最高版本；若所有范围版本不存在交集区间，则冲突决策失败；
- 使用同一本地依赖（如：./a.har），依赖存放路径不一致时，冲突决策失败；
- 同一依赖，同时存在本地版本（如：./a.har）与远程版本（如：^1.0.0）时，冲突决策失败；
- 同一依赖，存在多个固定版本时，冲突决策失败。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155954.32628723038966963919651729643273:50001231000000:2800:B88DC12BBEC15F156D315A625C43576D61C931A2A0EE1B1585914F02C2A6B417.png "点击放大")
    

注意

1. 严格模式下，依赖冲突决策成功时，ohpm会打印被解决冲突的依赖的警告信息，包含：依赖名称、所有冲突的版本、最终安装版本、受影响的模块列表。
2. 严格模式下，依赖冲突决策失败时，ohpm会打印依赖冲突树并在树上高亮显示解决失败的依赖及版本和所有解决失败的依赖的错误信息，包含：依赖名称、所有冲突的版本。当依赖存在版本冲突时，可以通过[overrides](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-oh-package-json5#zh-cn_topic_0000001792256137_overrides)配置解决。

### 示例

1. 将resolve_conflict_strict开关设置为true：
    
    1. ohpm config set resolve_conflict_strict true
    
2. 在AppTest3工程根目录的oh-package.json5中配置依赖@ohos/axios：
    
    1. {
    2.   "modelVersion": "6.0.1",
    3.   "description": "Please describe the basic information.",
    4.   "dependencies": {
    5.     "@ohos/axios": "2.2.5"
    6.   }
    7. }
    
3. 在AppTest3工程下entry模块的oh-package.json5中配置依赖@ohos/axios：
    
    1. {
    2.   "name": "entry",
    3.   "version": "1.0.0",
    4.   "description": "Please describe the basic information.",
    5.   "main": "",
    6.   "author": "",
    7.   "license": "",
    8.   "dependencies": {
    9.     "@ohos/axios": "2.2.6"
    10.   }
    11. }
    
4. 在AppTest3工程下任意目录执行命令：ohpm install --all，根据严格的依赖版本冲突处理规则，此时ohpm会安装失败并打印依赖冲突树，如下所示：
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155954.48112180768722295775677939510154:50001231000000:2800:4B651E27316392736CC07D351B6E1C9A83ABFA377F767D3892176C6D61AFA401.png)
    

## crypto_path

ohpm客户端从5.2.0版本开始，支持对敏感配置项进行加密存储和读取。

**支持加密的敏感配置项**：

|配置项|说明|示例格式|
|:--|:--|:--|
|[key_passphrase](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpmrc#section10698175182316)|必须加密，对应 key_path 的私钥密码|key_passphrase=security:xxx|
|http_proxy|代理用户名密码部分可加密（username:password替换为密文）|http_proxy=http://security:xxx@proxy:port|
|https_proxy|代理用户名密码部分可加密（username:password替换为密文）|https_proxy=https://security:xxx@proxy:port|
|[AccessToken](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpmrc#section74219299467)|仓库认证配置（:_auth 和 :_read_auth）|//<仓库地址>/:_auth=security:xxx<br><br>//<仓库地址>/:_read_auth=security:xxx|

用户可通过以下流程实现配置加密：

1. 使用 [ohpm config encrypt](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-config#section1085417514102) 命令生成加密组件并对标准输入的数据加密。
2. 在 .ohpmrc 文件中配置 crypto_path 加密组件路径和敏感配置项。
    
    1. crypto_path=D:\path\to\crypto_dir
    2. key_passphrase=security:xxx
    3. http_proxy=http://security:xxx@proxy:port
    4. https_proxy=https://security:xxx@proxy:port
    5. //<仓库地址>/:_auth=security:xxx
    6. //<仓库地址>/:_read_auth=security:xxx
    

说明

1、key_passphrase 配置项必须使用密文格式配置，其余敏感配置项仍兼容明文配置。

2、命令执行时，根据优先级（项目级 > 用户级 .ohpmrc）获取命令所需的敏感配置项后，使用该配置项同层级的 crypto_path 指定的加密组件进行解密。

## key_passphrase

ohpm 客户端从5.2.0版本开始，支持在 .ohpmrc 文件中配置 key_passphrase 私钥密码，用于自动解密 key_path 对应的私钥文件。

- 执行 ohpm publish、ohpm unpublish 等需要认证的命令时，系统会自动使用 key_passphrase 解密私钥，无需手动输入密码。
- key_passphrase 必须是通过 [ohpm config encrypt](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-config#section1085417514102) 命令生成的密文。
- 需同时配置 key_path 私钥文件路径。
- 需同时配置 [crypto_path](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpmrc#section18322038185010) 加密组件路径，用于运行时解密 key_passphrase。

**示例**

在项目级或用户级 .ohpmrc 文件中配置，执行 publish 命令，用户无需手动输入密码即可完成推包操作。

1. key_path=:\path\to\key_file
2. crypto_path=D:\path\to\crypto_dir
3. key_passphrase=security:xxx

## AccessToken

AccessToken是 ohpm-repo 2.1.0版本新引入的认证机制，用户通过ohpm-repo界面生成Token，并将其配置至ohpm客户端配置文件中。

在与 ohpm-repo 交互时，客户端会自动附带Token进行身份验证。该Token分两种权限等级：

1. 只读Token允许执行info和install操作；
2. 读写Token除了包含只读权限外，还支持publish和unpublish操作。

每位用户每种权限类型的Token最多可生成10个，首次生成时系统自动复制到剪贴板，后续不再显示完整Token内容。

### 如何获取AccessToken

当前AccessToken仅 ohpm-repo 支持，登录成功后，在ohpm-repo首页的右上角 > 认证管理 > AccessToken页面进行生成。![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155954.01128560838298897525390446888076:50001231000000:2800:25D492CF0C99FB89D4E443793BE5EFC4CF358F4A88C41150A1828718417F8C6C.png)

### 如何配置AccessToken

在".ohpmrc"文件配置示例如下：

1. //127.0.0.1:8088/repos/ohpm/:_auth=readWriteToken
2. //127.0.0.1:8088/repos/ohpm/:_read_auth=readOnlyToken

其中 ：

- //127.0.0.1:8088/repos/ohpm/ 是ohpm-repo的registry地址去除协议名的部分；
- :_auth 和 :_read_auth 分别代表配置为读写Token或只读Token，readWriteToken和readOnlyToken代表Token具体的值。ohpm客户端执行info、install操作会优先使用只读Token，如果只读Token不存在才会使用读写Token。ohpm客户端执行publish、unpublish操作时只会使用读写Token。每种Token最多配置三条。

## enforce_dependency_key

ohpm从1.7.0版本开始，支持在.ohpmrc文件中配置enforce_dependency_key，该配置项值为布尔类型，默认为false。将配置设置为true后，ohpm会校验各模块的oh-package.json5中配置的直接依赖中的本地依赖名称与其对应的包名(模块名)是否一致，若不一致会导致依赖安装失败并在错误日志中打印出不一致的依赖名称与其对应的包名(模块名)。

**示例：**

在MyApplication工程下存在一个名称为foo的模块，foo模块的oh-package.json5如下所示：

1. {
2.   "name": "foo",
3.   "version": "2.0.0",
4.   "description": "Please describe the basic information.",
5.  }

在MyApplication工程下存在另一个名称为bar的模块，且bar模块中依赖了foo模块，bar模块的oh-package.json5如下所示：

1. {
2.   "name": "bar",
3.   "version": "1.0.0",
4.   "description": "Please describe the basic information.",
5.   "dependencies": {
6.     "fee": "file:../foo"  
7.   },
8.  }

如上所示，bar模块的oh-package.json5中配置了对foo模块的依赖，并为foo模块起了一个别名为fee。当在.ohpmrc中将enforce_dependency_key配置为true时：

1. enforce_dependency_key=true

此时在MyApplication下执行ohpm install --all命令将打印如下错误日志，同时会中断命令的执行：

1. ohpm ERROR: local dependency "fee" found in "D:\DevecostudioProjects\MyApplication2\bar\oh-package.json5" does not match the actual name "foo" of its oh-package.json5
2. ohpm ERROR: Install failed, detail: There are some dependency names that are inconsistent with the actual package names.

若没有配置enforce_dependency_key或将其配置为false时，命令将不会被中断，同时上述错误日志的日志级别将会下调为告警日志：

1. ohpm WARN: local dependency "fee" found in "D:\DevecostudioProjects\MyApplication2\bar\oh-package.json5" does not match the actual name "foo" of its oh-package.json5

建议在.ohpmrc文件中配置enforce_dependency_key为true，禁止以别名的方式配置本地依赖，避免出现如下场景：

基于上述示例，在MyApplication下真的存在一个名称为fee的模块，且该模块的版本号小于foo模块，fee模块的oh-package.json5如下所示：

1. {
2.   "name": "fee",
3.   "version": "1.0.0",  // 小于foo的版本号2.0.0
4.   "description": "Please describe the basic information.",
5.  }

且entry模块中同时依赖了fee与bar，entry模块的oh-package.json5依赖配置如下所示：

1. {
2.   "name": "entry",
3.   "version": "1.0.0",
4.   "dependencies": {
5.     "fee": "file:../fee",
6.     "bar": "file:../bar"  
7.   },
8.  }

此时在entry的依赖树中，依赖fee存在两个版本：一个别名为fee的foo模块，一个名称为fee的fee模块，若此时开启了[resolve_conflict](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpmrc#section368717475562)，由于fee模块的实际版本号为1.0.0要小于foo模块的版本号2.0.0，在执行ohpm install时将只会在entry模块的oh_modules下安装以fee为别名的foo模块，而实际的fee模块则不会被安装，如下图所示：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155954.66847227410432009721820691733864:50001231000000:2800:4F14D051DBD0A1CF1D298BB3501E3D58C276854F7DE87C143B657806917BF7B0.png "点击放大")

在entry的oh_modules下会生成一个名称为fee的软链接，该链接却指向foo模块的实际路径：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155954.58127235533886129856714573776678:50001231000000:2800:AFA217354E934B203E2ACF507D184446E646D03752E44815757127B0BB6BA2BF.png "点击放大")

如果entry实际希望依赖的是真实的fee模块而不是foo模块，则此时会导致entry无法编译成功。

注意

1、从ohpm客户端5.0.7开始，若项目级build-profile.json5文件中strictMode字段下配置了useNormalizedOHMUrl开关且useNormalizedOHMUrl=true，则该配置优先级高于enforce_dependency_key，如果ohpm检测到依赖别名与oh-package.json5中name不一致时，会报错提示并中止程序执行；若未配置useNormalizedOHMUrl或useNormalizedOHMUrl=false时，是否校验别名一致性则根据enforce_dependency_key配置决定。

2、项目级build-profile.json5文件中，products节点下任意product字段配置了useNormalizedOHMUrl=true，则ohpm中useNormalizedOHMUrl开关会被设置为true，即ohpm检测到项目中依赖别名与oh-package.json5中name不一致时，会报错提示并中止程序执行。

## ensure_dependency_include

ohpm从1.7.0版本开始，支持在.ohpmrc文件中配置ensure_dependency_include，该配置项值为布尔类型，默认为false。

在ohpm prepublish/publish时，ohpm会扫描待发布包的内容，如果代码中import了某个包的内容，但相应的包没有配置在dependencies/dynamicDependencies中，即如果该配置项的值为true，则ohpm会打印错误信息并中断执行；否则，ohpm只会打印告警提示。

例如，test.har包的代码中import了@ohos/hypium包，但test.har的oh-package.json5的dependencies中未配置@ohos/hypium依赖。下面就ensure_dependency_include开关为true/false时ohpm publish的行为进行举例说明。

### 示例1

1. 将ensure_dependency_include开关置为false：
    
    1. ohpm config set ensure_dependency_include false
    
2. 发布test.har包。
    
    1. ohpm publish test.har
    
3. 当ensure_dependency_include=false时，发布完成后将打印告警提示。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155954.33348797867940035957564060268626:50001231000000:2800:BBCD7C31674B0016360707768410365480930D56A8685F09DC076A1E2D3782D3.png)
    

### 示例2

1. 将ensure_dependency_include开关置为true：
    
    1. ohpm config set ensure_dependency_include true
    
2. 发布test.har包。
    
    1. ohpm publish test.har
    
3. 当ensure_dependency_include=true时，发布时将报错。![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155954.07970733121953577600318937422319:50001231000000:2800:B77059879603C9BF6F87B21528A1CEC7B6ACD97257086F853AE08DE735A7B556.png)

## disallow_nested_package

ohpm从1.8.0版本开始，支持在.ohpmrc文件中配置disallow_nested_package，该配置项值为布尔类型，默认为false。在ohpm prepublish/publish时，ohpm会扫描待发布包的dependencies和dynamicDependencies依赖配置，如果依赖配置中存在相对路径或绝对路径配置的.har、.tgz依赖且disallow_nested_package开关为true，则ohpm会报错提示。

### 示例

1. lib_nested.har包的dependencies中配置了如下依赖：
    
    1. {
    2.   "dependencies": {
    3.     "liblib_nested.so": "file:./src/main/cpp/types/liblib_nested",
    4.     "hsp": "./libs/hsp-default.tgz",
    5.     "lib_har": "./libs/lib_har.har"
    6.   }
    7. }
    
2. 将disallow_nested_package 开关置为true。
    
    1. ohpm config set disallow_nested_package true
    
3. 发布lib_nested.har。
    
    1. ohpm publish lib_nested.har
    
4. 当disallow_nested_package=true时，发布时将报错。![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155954.53202917093436379093538350930658:50001231000000:2800:2AEEEA241B56A4C95E74B006632E4353C095767346E6840D7F9C27E053D087E6.png)

## odm_r2_project_root

odm_r2_project_root是ohpm客户端1.8.0新增的开关配置，默认为false，可以通过config命令或直接在.ohpmrc文件中修改其值。

当该配置为true时，若在overrideDependencyMap中配置的依赖项替换文件中存在以相对路径配置的本地依赖项时，在ohpm运行时会基于工程根路径来查找这些本地依赖项。

示例：

1. .ohpmrc中开启odm_r2_project_root：
    
    1. odm_r2_project_root=true
    
2. overrideDependencyMap配置示例：
    
    在工程根目录下的oh_package.json5中增加overrideDependencyMap配置，如下：
    
    1. {
    2.   "overrideDependencyMap": {
    3.      "lib1": "lib1-override-dep-map.json5",  
    4.      "lib2": "lib2-override-dep-map.json5"
    5.   }
    6. }
    
3. 依赖项"lib1"的依赖项替换文件lib1-override-dep-map.json5示例：
    
    1. {
    2.   "dependencies": {
    3.     "@ohos/test": "file:./test.har"
    4.   }
    5. }
    

如上第3步所示，当odm_r2_project_root开关设置为true时，在ohpm运行时会以工程根目录为起点查找"./test.har"，比如：工程根路径为：D:\path\to\MyProject，在ohpm运行时解析得到test.har的绝对路径为：D:\path\to\MyProject\test.har。

## compability_log_level

ohpm客户端从5.0.1开始新增开关配置'compability_log_level'字段，用于控制在缺少兼容性检测需要的字段时ohpm的处理逻辑。

compability_log_level字段默认赋值为'warn'，可配置的日志等级请见[开关配置项说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpmrc#section139481140114517)。

在执行prepublish、publish命令时，ohpm会检测oh-package.json5文件中是否配置了兼容性检测需要的所有字段（'compatibleSdkVersion', 'compatibleSdkType', 'obfuscated', 'nativeComponents'），详见[模块级oh-package.json5字段说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-oh-package-json5#zh-cn_topic_0000001792256137_oh-packagejson5-%E5%AD%97%E6%AE%B5%E8%AF%B4%E6%98%8E)，下面统称 '兼容性字段'，如果未配置，则会根据日志等级打印提示或报错。

### 开关配置项说明

- close：关闭功能，不主动检测兼容性字段。
- info：检测到未配置的兼容性字段时，打印info日志。
- warn：检测到未配置的兼容性字段时，打印警告日志。
- error：检测到未配置的兼容性字段时，打印报错提示并中断程序。

## enable_unified_lockfile

ohpm客户端从5.1.1开始新增开关配置enable_unified_lockfile字段。启用此特性后，ohpm将自动整合项目中所有子模块的oh-package-lock.json5文件，统一生成至项目根目录的oh-package-lock.json5文件中。

启用enable_unified_lockfile=true后，项目级统一管理lockfile锁文件，针对模块间存在重复依赖的场景，显著减少ohpm install耗时，优化构建流程。

注意

启用enable_unified_lockfile=true后，原分散在各模块下的.hsp依赖安装目录将统一迁移至项目根目录。在流水线上开启此特性时，需搭配配套的hvigor使用。

## enable_boost_extraction_speed

ohpm客户端从5.3.0开始新增开关配置enable_boost_extraction_speed字段。ohpm安装时涉及对.har/.tgz三方包文件的解压和遍历，启用此特性后，将使用高性能方法进行解压和遍历，当工程中存在大文件依赖时，可以显著减少ohpm install耗时。该功能当前处于实验阶段，暂不支持解压包含软链接的三方包文件。

## enable_lock_inner_pkg_version

ohpm客户端从5.3.1开始新增开关配置enable_lock_inner_pkg_version字段。默认为true，若设置为false，在ohpm安装时，不会将依赖内部的.har或.tgz子依赖的版本保存至oh-package-lock.json5，以防oh-package-lock.json5中保存不存在的路径导致二次安装报错。

如下图所示，蓝色箭头标识最终要安装的依赖，安装的依赖D@1.0.0来自依赖B@1.0.0（依赖名称和依赖版本相同的依赖会被定性为相同依赖，最终安装哪个由依赖构建先后顺序决定）, 因B@1.0.0并没有安装，但oh-package-lock.json5中锁定了依赖D的版本，在二次安装时会爆出D的依赖路径不存在错误，此时需要将该开关设置为false。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155954.54164269041472071758723009937932:50001231000000:2800:D11C088AEA9D834FB3BEAA57A9B896886DD2FF18D8FCEA025C3E0FDBC0F5B976.png)

**oh-package-lock.json5示例**

1. 生成library.har，oh-package.json5如下。
    
    1. {
    2.   "name": "library",
    3.   "version": "1.0.0",
    4.   "description": "Please describe the basic information.",
    5.   "author": "",
    6.   "license": "Apache-2.0",
    7.   "dependencies": {
    8.     "inner": "./libs/inner.har"
    9.   },
    10.   "types": "Index.d.ets",
    11.   "artifactType": "obfuscation",
    12.   "compatibleSdkVersion": 21,
    13.   "compatibleSdkType": "HarmonyOS",
    14.   "obfuscated": false
    15. }
    
2. entry依赖library.har，oh-package.json5如下。
    
    1. {
    2.   "name": "entry",
    3.   "version": "1.0.0",
    4.   "description": "Please describe the basic information.",
    5.   "main": "",
    6.   "author": "",
    7.   "license": "",
    8.   "dependencies": {
    9.     "library": "./library.har"
    10.   }
    11. }
    
3. .ohpmrc中配置开关：enable_lock_inner_pkg_version=false，工程任意目录下执行命令：ohpm install --all，此时生成的entry/oh-package-lock.json5中不会锁定内部包inner的版本，如下所示。
    
    1. {
    2.   ......
    3.   "specifiers": {
    4.     "library@library.har": "library@library.har"
    5.   },
    6.   "packages": {
    7.     "library@library.har": {
    8.       "name": "library",
    9.       "version": "1.0.0",
    10.       "resolved": "library.har",
    11.       "registryType": "local",
    12.       "dependencies": {
    13.         "inner": "./libs/inner.har"
    14.       }
    15.     }
    16.   }
    17. }
    
    enable_lock_inner_pkg_version=true时，entry/oh-package-lock.json5结果如下：
    
    18. {
    19.   ......
    20.   "specifiers": {
    21.     "inner@../oh_modules/.ohpm/library@85ursk4cfzbgycewlyxweed+cyyeeixxig5mlazoo+g=/oh_modules/library/libs/inner.har": "inner@../oh_modules/.ohpm/library@c0jkxsxl3amvdd7rr1enrkrejzharxwucdoyc29br+u=/oh_modules/library/libs/inner.har",
    22.     "library@library.har": "library@library.har"
    23.   },
    24.   "packages": {
    25.     "inner@../oh_modules/.ohpm/library@c0jkxsxl3amvdd7rr1enrkrejzharxwucdoyc29br+u=/oh_modules/library/libs/inner.har": {
    26.       "name": "inner",
    27.       "version": "1.0.0",
    28.       "resolved": "../oh_modules/.ohpm/library@c0jkxsxl3amvdd7rr1enrkrejzharxwucdoyc29br+u=/oh_modules/library/libs/inner.har" 
    29.       "registryType": "local"
    30.     },
    31.     "library@library.har": {
    32.       "name": "library",
    33.       "version": "1.0.0",
    34.       "resolved": "library.har"
    35.       "registryType": "local",
    36.       "dependencies": {
    37.         "inner": "./libs/inner.har"
    38.       }
    39.     }
    40.   }
    41. }
    

## case_sensitive_check

ohpm客户端从6.21.0新增开关配置"case_sensitive_check"字段。若设置为true，在执行ohpm相关命令时，如果ohpm检测到工程中文件的配置路径和文件的实际路径存在大小写不一致问题时，则会报错提示开发者修改。该配置项仅在Windows环境下生效。

**检测范围**

- .har包、.tgz包、工程中的module作为依赖时的路径。
- prefix、target_path、parameterFile的命令中配置的目录或路径。
- overrides配置项中的本地依赖路径，overrideDependencyMap配置项涉及的配置文件及文件内的本地依赖路径，parameterFile配置文件及文件内的本地依赖路径。

**示例**

1. 准备本地har包：test.har，该har包内oh-package.json5中name为：test，将其放置在模块entry的libs目录下。
2. entry依赖test.har，则原始依赖路径为：<project_dir>/entry/libs/test.har， entry的oh-package.json5内容如下：
    
    1. {
    2.   "name": "entry",
    3.   "version": "1.0.0",
    4.   "description": "Please describe the basic information.",
    5.   "dependencies": {
    6.     "test": "./Libs/test.har"
    7.   }
    8. }
    
3. 执行ohpm install，ohpm可检测到test.har的实际路径（<project_dir>/entry/libs/test.har）与配置路径（<project_dir>/entry/Libs/test.har）大小写不一致(配置时libs目录名存在大写字母：'L'，与原始目录名不一致)，此时ohpm会报错提示并中断执行。
# oh-package.json5

更新时间: 2025-12-16 15:59

从OHPM 5.0.0版本开始，支持区分工程级与模块级oh-package.json5配置。其中：

- 工程级oh-package.json5文件：位于工程根目录下，主要用来描述全局配置，如：依赖覆盖（overrides）、依赖关系重写（overrideDependencyMap）和参数化配置（parameterFile）等，详情请见：[工程级oh-package.json5 字段说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-oh-package-json5#section02162312018)；
- 模块级oh-package.json5文件：位于工程各个模块的根目录下，用来描述包名、版本、入口文件（类型声明文件）和依赖项等信息，详情请见：[模块级oh-package.json5 字段说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-oh-package-json5#zh-cn_topic_0000001792256137_oh-packagejson5-%E5%AD%97%E6%AE%B5%E8%AF%B4%E6%98%8E)。

开发者可将标准的DevEco Studio工程下的各个模块打成HAR包后，发布到OpenHarmony三方库中心仓；所有发布到仓库的包必须包含模块级oh-package.json5文件，以描述当前包基本信息。

## 工程级oh-package.json5 字段说明

|配置项|字段名称|字段说明|字段要求|字段类型|默认值|备注|
|:--|:--|:--|:--|:--|:--|:--|
|**开发态版本**|modelVersion|开发态版本号|**必选**|字符串|无|开发态版本号。|
|**描述配置**|description|简介|可选|字符串|无|用于描述工程信息的字符串。|
|**依赖配置**|dependencies|生产依赖|可选|对象|{}|用于配置参与编译/运行阶段使用的依赖，声明需要在代码中import的三方库（不建议在工程级oh-package.json5中配置生产依赖）。|
|devDependencies|开发依赖|可选|对象|{}|配置开发态依赖，配置只能参与项目的开发或测试阶段的依赖。如果被依赖的组件最终要与依赖的组件一起发布到目标机器（如手机）上使用，则不能在其中配置。|
|dynamicDependencies|动态依赖|可选|对象|{}|配置项目动态依赖的HSP模块。在开发者需要动态加载HSP的时候配置使用（不建议在工程级oh-package.json5中配置动态依赖）。|
|overrides|依赖覆盖配置|可选|对象|{}|支持将依赖树中的包替换为另一个指定版本，详情见[overrides](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-oh-package-json5#zh-cn_topic_0000001792256137_overrides)。|
|overrideDependencyMap|重写依赖关系|可选|对象|{}|支持将依赖树中包的子依赖替换为配置文件中配置的依赖，详情见[overrideDependencyMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-oh-package-json5#section106151513236)。|
|exclusions|第三方依赖的子依赖排除配置|可选|对象|{}|支持移除第三方依赖（远程依赖、本地文件依赖）中的一个或多个子依赖，详情见[exclusions](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-oh-package-json5#section18586313199)。|
|**其他**|scripts|自定义脚本|可选|对象|{}|维护一个脚本别名到脚本内容的映射表，开发者可以通过ohpm run <脚本别名>来触发对应脚本内容的执行。|
|hooks|钩子|可选|对象|{}|安装或卸载的钩子设置，包含 "preInstall"，"postInstall"，"preUninstall"，"postUninstall"，"preVersion"，"postVersion"，"prePublish"，"postPublish" 字段。仅支持执行当前工程中的 hooks，不支持执行依赖中的 hooks。|
|parameterFile|参数化配置文件路径|可选|字符串|无|标识是否开启参数化。未配置：关闭参数化；已配置：开启参数化。需同时指定参数化配置文件路径，详见[parameterFile](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-oh-package-json5#section122411462820)。|

注意

不建议在工程级依赖中配置非devDependencies的依赖，即一个Hsp/Har模块的非开发态依赖都要在相应模块的dependencies和dynamicDependencies中声明。

## 模块级oh-package.json5字段说明

模块级oh-package.json5文件位于工程各个模块的根目录下，用来描述当前模块被其他模块依赖时的相关信息，包括：作为依赖时的依赖名（name）、作为依赖时的版本号（version）、入口文件（main/types）和子依赖项等信息。

|配置项|字段名称|字段说明|字段要求|字段类型|默认值|备注|
|:--|:--|:--|:--|:--|:--|:--|
|**描述配置**|name|名称|**必选**|字符串|无|该模块作为依赖时的依赖名，用于唯一标识该依赖。<br><br>格式为：@group/packagename或packagename，长度：[1, 128]，全局唯一，即一个应用中，不同依赖的依赖名不能重复。建议name命名时包含组织名称group，便于管理和识别三方依赖。<br><br>name中只有在存在组织名称group时，才能有且仅能有一个'@'符号，有且仅有一个路径分隔符'/'。<br><br>**组织名称group格式：**<br><br>1、仅允许以小写字母开头，可由小写字母、数字、中划线(-)、下划线(_)组成。<br><br>2、禁止以中划线（-）、下划线（_）结尾。<br><br>3、不允许为ArkTS 的保留关键字。<br><br>**packagename格式：**<br><br>1、仅允许以小写字母开头，可由小写字母、数字、点（.）、中划线（-）、下划线（_）组成。<br><br>2、禁止以点（.）、中划线（-）、下划线（_）结尾。<br><br>3、不允许为ArkTS的保留关键字。|
|version|版本号|**必选**|字符串|1.0.0|该模块构建产物（HAR/HSP）的版本号。<br><br>规范：采用X.Y.Z（主版本.次版本.修订号）三段式结构，遵循 [semver](https://semver.org/) 语义化规范，从1.0.0开始。|
|description|简介|可选|字符串|无|用于描述该模块构建产物（HAR/HSP）的信息，有助于被搜索发现。长度范围为0-512字符。|
|keywords|关键字|可选|数组|[]|关键字信息数组，便于搜索使用。例如：["tools", "project"]。|
|author|作者|可选|对象或字符串|无|包含 name 字段（必选）、 email 字段（可选）、url字段（可选），可通过格式对象或字符串格式配置。<br><br>name字段允许使用字母、数字，点（.），中划线（-），下划线（_），空格，中文。<br><br>- 对象格式："author": {"name": "xxx" , "email": "xxx@xxx.com" , "url": "https://xxx.com" }。<br>- 字符串格式："author": "name<xxx@xxx.com>(https://xxx.com)"。|
|homepage|主页链接|可选|字符串|""|通常是项目gitee链接。|
|repository|仓库地址|可选|字符串|""|开源代码仓库地址。在私仓管理界面的系统设置处可定义是否为必填。|
|license|开源协议|**必选**|字符串|"ISC"|当前项目的开源许可证。遵循 [spdx license](https://spdx.org/licenses/) 规范。许可证若为 GPL，repository 建议不为空。|
|**依赖配置**|dependencies|生产依赖|可选|对象|{}|用于配置参与编译/运行阶段使用的依赖，声明需要在代码中import的三方库（参与编译/运行阶段使用的依赖）。|
|devDependencies|开发依赖|可选|对象|{}|用于配置开发态依赖，只能参与项目的开发或测试阶段。如果被依赖的组件最终要与依赖的组件一起发布到目标机器（手机）上使用，则不能在其中配置。|
|dynamicDependencies|动态依赖|可选|对象|{}|用于配置项目动态依赖的HSP模块。在开发者需要动态加载HSP的时候配置使用。|
|**文件配置**|main|入口|**必选**|字符串|无|指定加载的入口文件。|
|types|类型定义|可选|字符串|""|指定类型定义的文件名。当用 typescript 定义新的类型，需要提供给其他开发者使用，则需要指定其声明文件，一般为 .d.ts，.d.ets 文件。|
|**兼容性检测相关配置**|compatibleSdkVersion|SDK版本|可选|字符串|无|三方库开发者使用的SDK版本，构建时由Hvigor自动填充，提供给SDK做兼容性检测。<br><br>在prepublish、publish时，ohpm会对该字段进行检测(非空和长度校验)，并根据.ohpmrc中开关 [compability_log_level](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpmrc#section96369529419)配置的值进行提示或报错处理。<br><br>配置示例参看[兼容性字段配置示例](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-oh-package-json5#section194621247204911)。|
|compatibleSdkType|SDK类型|可选|字符串|无|三方库开发者使用的SDK类型，构建时由Hvigor自动填充，提供给SDK做兼容性检测, 示例值："OpenHarmony"、"HarmonyOS"。<br><br>在prepublish、publish时，ohpm会对该字段进行检测(非空和长度校验)，并根据.ohpmrc中开关 [compability_log_level](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpmrc#section96369529419)配置的值进行提示或报错处理。<br><br>配置示例参看[兼容性字段配置示例](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-oh-package-json5#section194621247204911)。|
|obfuscated|混淆标识|可选|布尔|无|三方库是否开启混淆标识，构建时由Hvigor自动填充，提供给SDK做兼容性检测。<br><br>在prepublish、publish时，ohpm会对该字段进行检测(非空校验)，并根据.ohpmrc中开关 [compability_log_level](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpmrc#section96369529419)配置的值进行提示或报错处理。<br><br>配置示例参看[兼容性字段配置示例](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-oh-package-json5#section194621247204911)。|
|nativeComponents|native so依赖配置|可选|数组|无|三方库使用的so包配置，构建时由Hvigor自动填充，提供给SDK做兼容性检测。<br><br>对于用户自行引入的so依赖(存放于libs目录)，需要用户手动维护该数组，数组单个元素类型为对象，对象内可配置的字段有：name、compatibleSdkVersion、compatibleSdkType。<br><br>在prepublish、publish时，如果包内存在so包，则ohpm会对该字段进行检测，并根据.ohpmrc中开关 [compability_log_level](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpmrc#section96369529419) 配置的值进行提示或报错处理；反之则不检测该字段。<br><br>配置示例参看[兼容性字段配置示例](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-oh-package-json5#section194621247204911)。|
|**其他**|artifactType|类型|可选|字符串|"original"|OpenHarmony包制品类型，有两个选项：original、obfuscation。original：源码，即发布源码(.ts/.ets)；obfuscation：混淆代码，即源码经过混淆之后发布上传。|
|scripts|自定义脚本|可选|对象|{}|维护一个脚本别名到脚本内容的映射表，开发者可以通过ohpm run <脚本别名>来触发对应脚本内容的执行。|
|hooks|钩子|可选|对象|{}|安装或卸载的钩子设置，包含 "preInstall", "postInstall", "preUninstall", "postUninstall","preVersion", "postVersion", "prePublish", "postPublish" 字段。仅支持执行当前工程中的 hooks，不支持执行依赖中的 hooks。|
|category|检查规则白名单|可选|字符串|{}|在私仓管理界面配置后自动生成，白名单为分号隔开的字符串列表，每个列表项必须是一个由大小写字母或下划线组成的字符串，包含在白名单中的配置项，不再做规则检查。|
|packageType|包类型|可选|字符串|InterfaceHar|标识模块是否为HSP包，在新建Shared Library时会自动生成该字段，并默认赋值为"InterfaceHar"；Static Library中没有该字段，表示为普通HAR包。|

注意

**依赖名使用要求：**

1、在oh-package.json5文件中dependencies、devDependencies、dynamicDependencies节点声明本地依赖时，允许配置的依赖名和依赖包的包名（即包内oh-package.json5中配置的name）不一致，但不推荐该用法，在默认情况下ohpm会通过告警日志来提示此类问题。

若希望将告警升级为报错并中断命令执行，可以通过在.ohpmrc中配置[enforce_dependency_key](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpmrc#section920325116547)=true；或在项目级[build-profile.json5](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile-app)文件中将strictMode字段下配置useNormalizedOHMUrl=true。

2、使用[参数化配置](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-oh-package-json5#section122411462820)时，依赖名和依赖包的包名（即包内oh-package.json5中配置的name）必须保持一致，否则会报错并中断命令执行。

3、在oh-package.json5、overrideDependencyMap、parameterFile文件中，不建议使用无效的转义字符（例如：\a、\e、\o等）或Unicode编码（例如：\uxxxx）。

## 兼容性字段配置示例

三方库开发者使用的SDK和当前集成该三方库工程编译时使用的SDK可能存在不一致的情况。因此，ohpm新增了兼容性检测相关配置以帮助SDK做兼容性分析。配置示例如下：

1. {
2.   "name": "library",
3.   "version": "1.0.0",
4.   "description": "Please describe the basic information.",
5.   "main": "Index.ets",
6.   "license": "Apache-2.0",
7.   "dependencies": {
8.     "liblibrary.so": "file:./src/main/cpp/types/liblibrary"
9.   },
10.   "**compatibleSdkVersion**": "12",
11.   "**compatibleSdkType**": "HarmonyOS",
12.   "**obfuscated**": false,
13.   "**nativeComponents**": [
14.     {
15.       "name": "liblibrary.so",
16.       "compatibleSdkVersion": "12",
17.       "compatibleSdkType": "HarmonyOS"
18.     }
19.   ]
20. }

## 创建一个新的oh-package.json5文件

通过命令行创建 oh-package.json5文件，执行如下命令：

1. 导航到包的目录。
    
    1. cd /path/to/package
    
2. 执行初始化命令，并按照问卷填写相关参数。
    
    - 对无命名空间模块，执行以下命令：
        
        1. ohpm init
        
    - 对有命名空间模块，执行以下命令：
        
        1. ohpm init --group group_name
        
3. 若跳过问卷填写，创建默认文件，可在初始化命令行加上配置参数 --yes。
    
    1. ohpm init --yes
    
    默认创建的oh-package.json5 文件示例：
    
    2. {
    3.  "name": "package_name",
    4.  "version": "1.0.0",
    5.  "description": "",
    6.  "main": "index.ts",
    7.  "author": "",
    8.  "license": "ISC",
    9.  "dependencies": {}
    10. }
    

## 依赖配置说明

ohpm 存在 dependencies，devDependencies和dynamicDependencies 三种依赖类型。同时支持具体版本号，范围版本号，tag标签，本地har/tgz文件路径、本地源码目录和使用@module通过模块名指向模块目录（示例："module_key": "@module:module_name"）多种方式引入依赖。当依赖的三方库版本号配置为 * 时，表示当前依赖的包版本为该三方库的最新包版本。

说明

1、从DevEco Studio 6.0.0 Beta1开始支持@module配置方式。

2、@module配置中module_name必须在project/build-profile.json5文件或者project/.hvigor/dependencyMap/dependencyMap.json5（hvigor生成）文件的modules节点下存在。

3、@module配置中，module_key需和"@module:module_name"指向的模块目录下oh-package.json5文件中配置的name一致。

1. dependencies：生产依赖，即参与编译/运行阶段使用的依赖，用来定义生产态HAR/HSP包依赖，声明在代码中被 import的三方库。如果被依赖的组件最终要与依赖的组件一起发布到目标机器（手机）上使用，则必须配置。
2. devDependencies：开发态依赖，只能参与项目的开发或测试阶段的依赖。如果被依赖的组件最终要与依赖的组件一起发布到目标机器（如手机）上使用，则不能配置在该字段中。
3. dynamicDependencies：动态依赖，用来配合[动态import](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-dynamic-import)，表达动态 import 使用的HSP 包依赖。动态依赖不会在加载时就被编译，而是根据条件导入模块或者按需导入模块，具有更高效的依赖加载速度。
4. 依赖配置示例：

5. {
6.   "dependencies": {
7.     // 具体版本号引入，支持符合semver标准的版本号
8.     "specific_version": "1.0.0",

9.     // 范围版本号引入，^引入1.x.x的最新版本，~引入1.0.x的最新版本。范围版本优先选取正式版本，无匹配的正式版本才会选取先行版本
10.     "scope_version": "^1.0.1",

11.     // tag标签引入，示例引入标签为"beta"对应的版本号
12.     "tag_version": "tag:beta",

13.     // 本地文件引入，可引入本地har/tgz文件
14.     "local_file": "file:./xx.har",

15.     // 本地源码引入，可引入本地其他模块的源码，示例直接引入本地的"module1"模块
16.     "local_source_code": "file:../module1"

17.     // 项目存在Foo模块，即build-profile.json5文件或dependencyMap.json5文件中modules节点下存在名称为Foo的模块；该模块Foo的oh-package.json5中name为：foo_test
18.     "foo_test": "@module:Foo"
19.   },
20.   "devDependencies": {
21.     // 支持依赖引入类型同dependencies
22.   },
23.   "dynamicDependencies": {
24.     // 支持依赖引入类型同 dependencies
25.   }
26. }

## overrides

ohpm客户端在1.4.0版本开始支持Override机制，可以在项目级别的oh-package.json5（即项目根目录下的oh-package.json5）文件中添加overrides配置，方便将依赖树中的依赖替换为另一个版本。替换的版本可以是一个具体的版本号或模糊版本、本地存在的HAR包或源码目录、[parameterFile](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-oh-package-json5#section122411462820)配置（示例："foo": "@param:dependencies.foo"），也可以使用@module通过模块名指向模块目录（示例："module_key": "@module:module_name"）。

例如，想要确保foo始终安装1.0.0版本，可以在**项目级**的oh-package.json5中增加如下配置：

说明

1. overrides必须配置在项目级别的oh-package.json5中，配置在模块级别的oh-package.json5中将不会生效。
2. 从DevEco Studio 6.0.0 Beta1开始支持@module配置方式。
3. @module配置中module_name必须在project/build-profile.json5文件或者project/.hvigor/dependencyMap/dependencyMap.json5（hvigor生成）文件的modules节点下存在，否则报错处理。
4. @module配置中，module_key需和"@module:module_name"指向的模块目录下oh-package.json5文件中配置的name一致，否则报错处理。

5. {
6.   "overrides": {
7.     "foo": "1.0.0"
8.   }
9. }

若本地存在foo的源码、HAR包或者@module配置，想确保foo始终使用您本地的版本，可以在**项目级**的oh-package.json5中如下配置：

1. {
2.    "overrides": {
3.       // 项目存在Foo模块，即build-profile.json5文件或dependencyMap.json5文件中modules节点下存在名称为Foo的模块；该模块Foo的oh-package.json5中name为：foo_test
4.       // "foo_test": "@module:Foo"
5.       // 本地存在"foo"的源码目录，如项目根目录下的foo目录
6.       // "foo": "file:./foo" 
7.       // 本地存在"foo"的HAR文件，如项目根目录下的libs目录中的foo.har
8.       "foo": "file:./libs/foo.har"
9.    }
10. }

## exclusions

ohpm客户端在5.3.0版本开始支持exclusions机制，可以在项目级oh-package.json5（即项目根目录下的oh-package.json5）文件中添加exclusions配置，即可实现移除第三方依赖（远程依赖、本地文件依赖）中的一个或多个子依赖。

### 配置说明

- 配置格式
    
    1. // key: value形式配置
    2. "[@group/]libname[@spec]" : ['exclude_sub_libname']
    
    - 配置key部分：[@group/]libname[@spec]，代表需要做子依赖排除的依赖名称及其版本，'[]'代表该内容为可选配置。当依赖没有组织名称时，[@group/]部分可不配置；当不需要精确匹配具体版本号或具体某个本地文件依赖时，[@spec]部分可不配置；spec可以是一个具体的版本号、本地文件路径（支持相对路径和绝对路径，配置为相对路径时指相对于项目根路径）。
    - 配置value部分，['exclude_sub_libname']是一个字符串数组，可配置多个，代表需要被排除的子依赖名称列表。

- 配置示例

1. {
2.   "exclusions": {
3.     "@ohos/lib1@1.0.0": ['@ohos/sub_lib1']      // 排除远程依赖@ohos/lib1的子依赖：@ohos/sub_lib1
4.     "@ohos/lib2@./lib2.har": ['@ohos/sub_lib2'] // 排除本地文件依赖@ohos/lib2的子依赖：@ohos/sub_lib2
5.   }
6. }

- 配置约束
    - exclusions必须配置在项目级别的oh-package.json5中，配置在模块级别的oh-package.json5中将不会生效。
    - exclusions配置只能移除远程依赖、本地文件依赖的子依赖，对源码依赖不生效。
    - exclusions只能移除dependencies、dynamicDependencies下配置的依赖。
    - exclusions中配置的key不能和[overrideDependencyMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-oh-package-json5#section106151513236)中配置的key一致，否则报配置冲突错误并中断程序。
    - 自动解决依赖版本冲突功能开启（.ohpmrc中resolve_conflict=true）后，如果exclusions配置中配置项指定了spec，但spec对应的依赖在版本决策中被移除时，exclusions配置将不会生效；建议该场景下不要配置spec部分。

### 示例

下面演示如何移除远程依赖或本地文件依赖的oh-package.json5中dependencies、dynamicDependencies下配置的依赖。示例中以<project>代表项目根路径进行说明。

1、模块级oh-package.json5内容如下，将安装依赖@ohos/lib1、@ohos/lib2。

1. {
2.   "name": "entry",
3.   "version": "1.0.0",
4.   "description": "Please describe the basic information.",  
5.   "dependencies": {
6.     "@ohos/lib1": "1.0.0" // 远程依赖
7.     "@ohos/lib2": "file:../lib2.har" // 本地文件依赖
8.   }
9. }

10. // @ohos/lib1的oh-package.json5配置
11. {
12.   "name": "@ohos/lib1",
13.   "version": "1.0.0",
14.   "description": "Please describe the basic information.",  
15.   "dependencies": {
16.     "@ohos/lib1_sub1": "1.0.0" // 子依赖1
17.     "@ohos/lib1_sub2": "2.0.0" // 子依赖2
18.   }
19. }

20. // @ohos/lib2的oh-package.json5配置
21. {
22.   "name": "@ohos/lib2",
23.   "version": "1.0.0",
24.   "description": "Please describe the basic information.",  
25.   "dependencies": {
26.     "@ohos/lib2_sub1": "1.0.0" // 子依赖1
27.     "@ohos/lib2_sub2": "2.0.0" // 子依赖2
28.   }
29. }

2、项目级oh-package.json5内容如下，添加exclusions配置，其中lib2.har放置在项目根目录下。

1. {
2.   "modelVersion": "6.0.1",
3.   "description": "Please describe the basic information.",
4.   "exclusions": {
5.     "@ohos/lib1@1.0.0": ['@ohos/lib1_sub1'],  // 排除远程依赖@ohos/lib1的子依赖：@ohos/lib1_sub1
6.     "@ohos/lib2@./lib2.har": ['@ohos/lib2_sub2'] // 排除本地文件依赖@ohos/lib2的子依赖：@ohos/lib2_sub2
7.   }
8. }

3、执行ohpm安装命令。

1. ohpm install --all

4、ohpm安装完成后，在entry目录下执行：ohpm list -d 10，打印依赖结构如下。

1. entry 1.0.0 <project>\entry
2. ├─┬ @ohos/lib1 1.0.0
3. │ └── @ohos/lib1_sub2 1.0.0 // 安装了子依赖@ohos/lib1_sub2,@ohos/lib1_sub1已被排除
4. ├─┬ @ohos/lib2 <project>\lib2.har
5.   └── @ohos/lib2_sub1 1.0.0 // 安装了子依赖@ohos/lib2_sub2,@ohos/lib2_sub1已被排除

## parameterFile

OHPM新增了参数化配置功能。开发者可在项目根目录配置一个参数化文件（json5格式文件），在该文件中维护模块或依赖版本信息，不同模块将根据该文件中的版本进行配置，满足不同构建场景下，开发者快速切换依赖版本的需要。同时，支持通过命令行指定参数化文件，降低流水线场景下模块和依赖版本的变更难度。

OHPM客户端在1.6.0版本开始支持参数化配置。可以在项目级别的oh-package.json5文件（即项目根目录下的oh-package.json5）中添加parameterFile配置，并同时指定parameterFile文件路径。配置规则如下：

- parameterFile文件路径支持配置相对路径，并以项目根目录为起点，如："parameterFile": "./parameterFile.json5"。
- 配置文件内容采用json5格式，支持多层json对象嵌套；
- 参数化key支持的字符与包名一致，请见[模块级oh-package.json5字段说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-oh-package-json5#zh-cn_topic_0000001792256137_oh-packagejson5-%E5%AD%97%E6%AE%B5%E8%AF%B4%E6%98%8E)中name字段要求，大小写敏感；
- 参数化value类型为是"string"或"object"。 value类型为string时，可以是符合[semver规范](https://semver.org/)的版本号，也可以使用本地相对路径（相对于parameterFile文件所在目录）或本地绝对路径。

说明

1. parameterFile字段必须配置在项目级别的oh-package.json5中，否则将不会生效或产生报错提示。
2. parameterFile配置文件位置可以通过命令行选项'-pf <string>' 或 '--parameterFile <string>'指定，但必须先在项目级别oh-package.json5中配置parameterFile字段，否则会报错提示；支持该选项的命令有：install、list、version。
3. parameterFile字段配置后，不允许执行update命令、uninstall命令和指定包名安装（如：'ohpm i <pkg>'）。
4. parameterFile文件路径大小写不敏感，不建议通过大小写来区分不同的配置文件。
5. oh-package.json5中支持参数化的字段有：version、dependencies、devDependencies和dynamicDependencies、overrides，未列举的字段均不支持参数化配置。overrides从DevEco Studio 6.0.0 Beta1开始支持参数化配置。

### 基础配置示例

工程级oh-package.json5示例：

1. {
2.   "modelVersion": "6.0.1",
3.   "description": "Please describe the project information.",
4.    ...
5.   "parameterFile": './parameterFile/parameterFile.json5', // 开启参数化并指定参数化配置文件路径
6.   "overrides": {
7.     "libtest1": "@param:dependencies.libtest1", // 所有依赖名称为：libtest1的版本会被替换为：1.0.1
8.     "libnative": "@param:dependencies.libnative" // 所有依赖名称为：libnative的版本会被替换为：libnative源码依赖路径  
9.   }
10. }

模块级oh-package.json5示例：

1. {
2.   "name": "parameter-test",
3.   "version": "@param:version", //使用时必须以 '@param:' 开头
4.   "description": "test desc.",
5.   "main": "index.ets",
6.   "author": "test author",
7.   "license": "ISC",
8.   "dependencies": {
9.     "libtest1": "@param:dependencies.libtest1"
10.   },
11.   "devDependencies": {
12.     "libtest2": "@param:devDependencies.libtest2"
13.   },
14.   "dynamicDependencies": {
15.     "libtest3": "@param:dynamicDependencies.libtest3"
16.   }
17.  }

parameterFile所指向文件的配置示例：

1. {
2.   "version": "1.0.0",
3.   "dependencies": {
4.     "libtest1": "1.0.1",
5.     "libnative": "../libnative" // 相对于parameterFile配置文件所在目录
6.   },
7.   "devDependencies": {
8.     "libtest2": "*"
9.   },
10.   "dynamicDependencies": {
11.     "libtest3": "latest"
12.   }
13. }

### 一仓多包示例

一个代码仓有多个har/hsp模块，发包时，一般需要开发者手动修改所有模块的版本号后再打包发布，若模块较多，操作繁琐且效率低下，建议使用参数化配置解决该问题，详细示例如下。

**当所有模块版本不一致**：

如下工程结构所示，所有模块的oh-package.json5中version字段均配置参数化版本（'@param:'开头部分），不同模块的版本均不一致，但都由参数化配置文件'parameter.json'全局统一管理；发包前，只需修改'parameter.json'文件中相关模块的版本，再构建所有模块即可；打包构建时，所有模块的参数化版本均会被替换为'parameter.json'中配置的具体版本（如：@param:har1会被替换为：1.0.0）。

1. AppTest
2. └── har1(模块)
3.     └── oh-package.json5
4.         └── "version": "@param:har1"
5. └── har2(模块)
6.     └── oh-package.json5
7.         └── "version": "@param:har2"
8. ... harn(模块)
9.     └── oh-package.json5
10.         └── "version": "@param:harn"
11. └── oh-package.json5 
12.     └── "parameterFile": "./parameter.json"    
13. └── parameter.json(参数化配置文件)
14.     └── "har1": "1.0.0"
15.     └── "har2": "2.0.0"
16.     ...
17.     └── "harn": "n.0.0"

**当所有模块版本一致**：

如下工程结构所示，所有模块均使用同一个参数化版本（@param:module_version），发包前，只需修改'parameter.json'中module_version的值，再构建所有模块即可；打包构建时，所有模块的参数化版本均会被替换为'parameter.json'中module_version对应的版本（如：@param:module_version会被替换为：1.0.0）。

1. AppTest
2. └── har1(模块)
3.     └── oh-package.json5
4.         └── "version": "@param:module_version"
5. └── har2(模块)
6.     └── oh-package.json5
7.         └── "version": "@param:module_version"
8. ... harn(模块)
9.     └── oh-package.json5
10.         └── "version": "@param:module_version"
11. └── oh-package.json5 
12.     └── "parameterFile": "./parameter.json" 
13. └── parameter.json(参数化配置文件)
14.     └── "module_version": "1.0.0"

## overrideDependencyMap

OHPM客户端在1.7.0版本开始支持使用overrideDependencyMap机制重写源码模块或三方库的依赖关系。开发者可在工程级oh-package.json5文件中新增overrideDependencyMap配置，在该配置对象中通过key-value形式配置依赖关系重写文件；其中，key为依赖标识符，value为依赖关系重写文件路径。在依赖安装时， ohpm会将依赖树中的某个依赖节点的所有直接子依赖替换为对应依赖关系重写文件中配置的依赖项，依赖关系重写文件中支持配置的依赖类型为dependencies、devDependencies、dynamicDependencies，通过使用overrideDependencyMap机制，可以满足开发者在不同场景下，动态变更依赖的需求。

同时，支持在.ohpmrc中使用projectPackageJson配置项来覆盖项目根目录下oh-package.json5中的配置，方便开发者快速切换配置，详情见 [ohpmrc](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpmrc)中projectPackageJson配置。

**配置说明**

- 配置格式
    
    "[@group/]libname[@version]" : "config_path"，其中 [@group/]libname[@version] 为依赖标识符key, config_path为配置文件路径value。
    

- 配置示例
    
    1. {
    2.   "overrideDependencyMap": {
    3.   "@group/libname": "dep-test.json5" 
    4.   }
    5. }
    

- 配置约束
    
    - overrideDependencyMap必须配置在工程级oh-package.json5中，配置在模块级oh-package.json5中将不会生效。
    
    - key中@version部分可选，未指定@version时，替换所有名称为@group/libname的依赖的直接子依赖；指定@version时，替换所有名称为@group/libname且版本为version的依赖的直接子依赖，同时，version需符合semver规范，不支持tags标签、范围版本号。
    
    - value是一个json5文件路径，文件内只支持配置：dependencies、devDependencies、dynamicDependencies。
    
    - value对应的文件路径只支持绝对路径，配置为相对路径时，需要手动设置.ohpmrc文件中odm_r2_project_root=true, 此时，相对路径会从项目根目录为起点开始解析。

**overrideDependencyMap场景示例**

- 模块entry下oh-package.json5配置了一个远程包依赖libbase，如下所示：
    
    1. {
    2.   "name": "entry",
    3.   "version": "1.0.0",
    4.   "main": "Index.ets",
    5.   "license": "Apache-2.0",
    6.   "dependencies": {
    7.     "libbase": "1.0.0"
    8.   }
    9. }
    
- 依赖libbase的oh-package.json5内容，存在一个子依赖lib1，如下所示：
    
    1. {
    2.   "name": "libbase",
    3.   "version": "1.0.0",
    4.   "description": "Please describe the basic information.",
    5.   "main": "Index.ets",
    6.   "author": "",
    7.   "license": "Apache-2.0",
    8.   "dependencies": {
    9.     "lib1": "1.0.0" //子依赖
    10.   }
    11. }
    
- 项目根目录oh-package.json5内容，如下所示：
    
    1. {
    2.   "name": "overridedependencymaptest",
    3.   "version": "1.0.0",
    4.   "description": "Please describe the basic information.",
    5.   "overrideDependencyMap": {      
    6.     "libbase": "D:\\overrideDependencyMapTest\\dep-debug.json5" //overrideDependencyMap依赖替换配置，可配置多条
    7.   }
    8. }
    
- 配置文件dep-debug.json5中依赖配置如下所示：
    
    1. {
    2.   "dependencies": { // 详细依赖配置
    3.     "lib1": "2.0.0",
    4.     "log4js": "2.0.0"
    5.   },
    6.   "devDependencies": {
    7.   },
    8.   "dynamicDependencies": {
    9.   }
    10. }
    
- entry模块下执行：ohpm i, 由于entry下依赖了libbase，而libbase在overrideDependencyMap有配置，此时会使用dep-debug.json5文件内的依赖覆盖libbase的dependencies、devDependencies、dynamicDependencies节点，最终，entry模块会安装libbase、lib1、log4js（无overrideDependencyMap配置覆盖时，只会安装：libbase、lib1）。
- entry list结果如下：
    
    1. entry 1.0.0 D:\overrideDependencyMapTest\entry
    2. └── libbase 1.0.0
    3.     └── lib1 2.0.0
    4.     └── log4js 2.0.0
    

## .ohpmrc中projectPackageJson配置

通过在.ohpmrc文件中配置projectPackageJson，可同时实现对overrides、overrideDependencyMap字段配置的效果，替换项目级oh-package.json5文件中相应的配置，方便开发者在不同使用场景下快速切换使用。配置格式及使用约束如下所示：

- 配置格式
    
    projectPackageJson:<project_root>=<config_path>, 其中 projectPackageJson:<project_root> 部分视做key, config_path 部分视做value。配置key指定项目根目录路径（绝对路径），配置value指定json5格式配置文件路径用以覆盖项目级oh-package.json5中的配置。
    
- 配置示例
    
    projectPackageJson:D:\test\TestProject=projectPackageJson.json5
    
- 配置约束
    
    - key必须以 'projectPackageJson:' 开头；project_root表示项目根路径。
    
    - value对应json5文件内只支持配置：overrides、overrideDependencyMap，不支持 parameterFile(编辑器和编译器无法识别)。
    
    - 对同一个project_root，如存在多条projectPackageJson配置路径，仅最后一条会生效。
    
    - value对应的文件路径支持绝对路径和相对路径，配置为相对路径时，从项目根目录为起点开始解析。

**示例**

下面演示在.ohpmrc中配置同一工程的不同环境下的projectPackageJson配置，当配置生效时，会直接覆盖项目级oh-package.json5中对应配置。

- 在项目级或用户级.ohpmrc中增加2条配置，分别对应开发、Release环境，如下所示：
    
    1. registry=http://localhost:8088/repos/ohpm
    2. log_level=debug
    3. strict_ssl=false
    4. projectPackageJson:D:\overrideDependencyMapTest=oh-pkg-debug.json5 //debug环境配置
    5. projectPackageJson:D:\overrideDependencyMapTest=oh-pkg-release.json5 //release环境配置，.ohpmrc中存在同一工程的多条配置时默认按配置先后顺序取最后一条，即当前配置生效
    

- 文件oh-pkg-release.json5配置，新增了一条依赖libbase的配置，如下所示：
    
    1. {
    2.   "overrideDependencyMap": {
    3.     "libbase": "D:\\overrideDependencyMapTest\\dep-release.json5"
    4.   }
    5. }
    
- Release环境下libbase的依赖替换文件dep-release.json5中依赖配置如下所示：
    
    1. {
    2.   "dependencies": {
    3.     "lib1": "1.0.0",
    4.     "lib2": "2.0.0",
    5.     "lib3": "3.0.0"
    6.   }
    7. }
    
- 基于 [overrideDependencyMap场景示例](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-oh-package-json5#section106151513236) 工程，在entry模块下执行：ohpm i，此时，在ohpm运行时中会将项目级oh-package.json5中的配置会变更为：
    
    1. {
    2.   "name": "overridedependencymaptest",
    3.   "version": "1.0.0",
    4.   "description": "Please describe the basic information.",
    5.   "overrideDependencyMap": {
    6.     "libbase": "D:\\overrideDependencyMapTest\\dep-release.json5"
    7.   }
    8. }
    

- 最终安装结果如下：
    
    1. entry 1.0.0 D:\overrideDependencyMapTest\entry
    2. └── libbase 1.0.0
    3.     └── lib1 1.0.0
    4.     └── lib2 2.0.0
    5.     └── lib3 3.0.0
    

## oh-package-lock.json5

oh-package-lock.json5用于锁定所有依赖的版本，以及缓存依赖的元数据信息。不建议开发者手动修改该文件的内容，也不建议开发者使用其他分析工具直接读取该文件的内容。

建议将oh-package-lock.json5文件提交到代码仓库中进行版本管理。优点如下：

- 确保构建可复现： oh-package-lock.json5文件记录了三方包安装时确切的依赖树，其中包括每个依赖的版本、子依赖及其版本等详细信息。将该文件提交到代码仓库，能够确保团队成员、持续集成（CI）服务器或其他任何克隆该项目的用户，在执行ohpm install时可以获得完全一致的依赖版本，从而保证项目的可复现构建。
- 提高安装速度： ohpm在安装依赖时，会优先使用oh-package-lock.json5锁定的版本信息，避免重新解析依赖版本，有效地加快安装过程。
- 安全性： 通过锁定依赖版本，oh-package-lock.json5可以帮助防止因上游依赖更新引入的安全漏洞。当发现依赖存在安全问题时，可以针对性地更新特定依赖版本，并将更新后的oh-package-lock.json5提交到仓库，确保所有使用者都获取到修复后的版本。
- 便于协同工作： 当团队成员在项目中添加、更新或删除依赖时，他们应运行ohpm update以更新oh-package-lock.json5。提交这些变更到仓库，可以让其他成员了解到依赖的变化，并在拉取最新代码后自动获取正确的依赖版本。
-# ohpm config

更新时间: 2025-12-16 15:59

设置ohpm用户级配置项。

## 命令格式

1. ohpm config set <key> <value>
2. ohpm config get <key>
3. ohpm config delete <key>
4. ohpm config list
5. ohpm config encrypt [options]

说明

配置文件中信息以键值对<key> = <value>形式存在。

## 功能描述

ohpm 从命令行和 .ohpmrc 文件中获取其配置设置。有关更多 .ohpmrc 文件信息和可用配置选项，请参阅 [ohpmrc](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpmrc) 章节。

注意

ohpm config 仅支持配置项字段（默认项字段请查阅 [ohpmrc](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpmrc#zh-cn_topic_0000001792216397_%E9%BB%98%E8%AE%A4%E9%85%8D%E7%BD%AE%E9%A1%B9) 章节），且仅支持修改**用户级目录**下的 .ohpmrc 文件。

## 子命令

### set

1. ohpm config set <key> <value>

在用户级目录下 .ohpmrc 文件中，以键值对<key> = <value>形式写入数据。

**示例**

1. 以配置项"log_level"为例，修改其值为debug（可选值：debug、info、warn、error）：
    
    1. ohpm config set log_level debug
    
2. 成功执行后，在用户目录/.ohpm/.ohpmrc文件中将显示log_level=debug。

### get

1. ohpm config get <key>

将从命令行，项目级 .ohpmrc 文件，用户级 .ohpmrc 文件（优先级依次递减）中获取的值进行标准输出。

如果未提供键值，则此命令执行效果与命令 ohpm config list 相同。

**示例1**

1. 以项目级.ohpmrc中log_level=info，用户级.ohpmrc中log_level=debug为例，在工程任意目录下执行如下命令。
    
    1. ohpm config get log_level
    
2. 成功执行后，在控制台打印log_level的值。
    
    1. info
    

**示例2**

1. 基于示例1，将项目级.ohpmrc删除，再次执行get命令。
    
    1. ohpm config get log_level
    
2. 成功执行后，在控制台打印log_level的值。
    
    1. debug
    

**示例3**

1. 未提供<key>值时执行命令ohpm config get。
    
    1. ohpm config get
    
2. 成功执行后，将在控制台打印所有.ohpmrc配置。
    
    1. ; "user" config from C:\Users\username\.ohpm\.ohpmrc
    
    2. registry="http://localhost:8088/repos/ohpm"
    3. strict_ssl = false
    4. log_level = "debug"
    
    5. ; "user" config from C:\Users\username\.ohpm\.ohpmrc
    6. ; node bin location = C:\Program Files\nodejs\node.exe
    7. ; node version = v18.19.1
    8. ; ohpm local prefix = C:\Users\username
    9. ; ohpm version = 5.1.2-rc.2
    10. ; cwd = C:\Users\username
    11. ; HOME = C:\Users\username
    

### list

1. ohpm config list
2. alias: ls

显示所有配置项。

**示例**

1. 执行list命令。
    
    1. ohpm config list 或者 ohpm config ls
    
2. 成功执行后，将在控制台打印所有.ohpmrc配置。
    
    1. ; "user" config from C:\Users\username\.ohpm\.ohpmrc
    
    2. registry="http://localhost:8088/repos/ohpm"
    3. strict_ssl = false
    4. log_level = "debug"
    
    5. ; "user" config from C:\Users\username\.ohpm\.ohpmrc
    6. ; node bin location = C:\Program Files\nodejs\node.exe
    7. ; node version = v18.19.1
    8. ; ohpm local prefix = C:\Users\username
    9. ; ohpm version = 5.1.2-rc.2
    10. ; cwd = C:\Users\username
    11. ; HOME = C:\Users\username
    

### delete

1. ohpm config delete <key>

删除用户级目录下 ohpmrc 文件中指定的键值。

**示例**

1. 用户.ohpmrc中原始内容。
    
    1. registry=http://localhost:8088/repos/ohpm
    2. strict_ssl=false
    3. log_level=debug
    
2. 执行delete命令。
    
    1. ohpm config delete registry
    
3. 成功执行后，.ohpmrc内容如下。
    
    1. strict_ssl=false
    2. log_level=debug
    

### encrypt

1. ohpm config encrypt [options]

使用加密组件加密标准输入的数据，并输出密文到标准输出。

**首次使用**：

- 必须在 config encrypt 命令后面配置 [--crypto_path <string>](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-config#section313318216424) 生成新的加密组件，并用于数据加密。
    
    **示例**
    
    1. 执行 encrypt --crypto_path <string> 命令，指定的路径为空目录。
        
        1. ohpm config encrypt --crypto_path D:\path\to\empty_dir
        
    2. 成功执行后，在指定路径生成新的加密组件，并对用户输入内容进行加密，其中用户输入内容不可见。
        
        1. ohpm INFO: Attempted to create an crypto component at the "D:\path\to\empty_dir" path...
        2. ohpm INFO: The crypto component has been created successfully.
        3. Please enter the password to be encrypted:
        4. ohpm INFO: encrypted result:
        5. security:01:61AE9D3219664B7B785XXXXX:201f713d625daddafcb12198ea9d5121xxxxxx
        
    3. 将生成的加密组件路径配置到 .ohpmrc 文件中，方便后续自动读取加密组件。
        
        1. crypto_path=D:\path\to\empty_dir
        

**非首次使用：**

- 若不指定 [--crypto_path](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-config#section313318216424)，则自动从 .ohpmrc 文件中读取配置（优先级：项目级 > 用户级 .ohpmrc），必须保证路径存在且包含有效加密组件。
- 若报错提示加密组件错误，可重新执行ohpm config encrypt --crypto_path <string> 命令。
- **示例**
    
    1. 执行 encrypt 命令。
        
        1. ohpm config encrypt
        
    2. 成功执行后，对用户输入内容进行加密，其中用户输入内容不可见。
        
        1. Please enter the password to be encrypted:
        2. ohpm INFO: encrypted result:
        3. security:01:61AE9D3219664B7B785XXXXX:201f713d625daddafcb12198ea9d5121xxxxxx
        

**密文使用：**

生成的加密结果可以配置到项目级或用户级 .ohpmrc 文件中，用于[敏感配置项](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpmrc#section18322038185010)。

## Options

### json

- 默认值：false
- 类型： Boolean
- 别名：j

可以在 config list 命令后面配置 -j或者--json 参数，以 json 格式输出所有配置项及默认值。

1. // 示例
2. // 1.执行list命令并以json形式输出
3. ohpm config list -j 或 ohpm config list --json
4. // 2.命令执行结果
5. {
6.   "registry": "http://localhost:8088/repos/ohpm", 
7.   "strict_ssl": false,
8.   "log_level": "info",
9.   ......
10. }

### crypto_path

- 默认值：无
- 类型： string

指定加密组件路径用于数据加密。针对指定路径的不同情况，说明如下：

1. 若指定路径不存在，自动创建目录并生成新加密组件；
2. 若路径为空目录，将自动在目录中生成新加密组件；
3. 若路径已存在有效加密组件，则使用现有组件加密。

4. // 示例1
5. // 1.执行 encrypt --crypto_path <string> 命令，指定的路径为空目录
6. ohpm config encrypt --crypto_path D:\path\to\empty_dir
7. // 2.成功执行后，在指定路径生成新的加密组件，并对用户输入内容进行加密，其中用户输入内容不可见
8. ohpm INFO: Attempted to create an crypto component at the "D:\path\to\empty_dir" path...
9. ohpm INFO: The crypto component has been created successfully.
10. Please enter the password to be encrypted:
11. ohpm INFO: encrypted result:
12. security:01:61AE9D3219664B7B785XXXXX:201f713d625daddafcb12198ea9d5121xxxxxx

13. // 示例2
14. // 1.执行 encrypt --crypto_path <string> 命令，指定的路径为有效的加密组件
15. ohpm config encrypt --crypto_path D:\path\to\crypto_dir
16. // 2.成功执行后，对用户输入内容进行加密，其中用户输入内容不可见
17. Please enter the password to be encrypted:
18. ohpm INFO: encrypted result:
19. security:01:61AE9D3219664B7B785XXXXX:201f713d625daddafcb12198ea9d5121xxxxxx
# ohpm info

更新时间: 2025-12-16 15:59

查询指定三方库的具体信息。

## 命令格式

1. ohpm info [options] [<@group>/]<pkg>[@<version> | @tag:<tag>] [field]

说明

- @group：三方库的命名空间，可选。
- pkg：三方库名称，必选。
- version：三方库的版本号，可选。
- tag：三方库的标签，标签会标记三方库的某个版本号，可选。
- field：从ohpm 6.21.0版本开始，支持查看三方库中元数据的属性，属性包括：keywords、dependencies、tags、versions、license、author、repository、dist、latest，具体请参考[Field](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-info#section1068917464119)。

## 功能描述

用于调用云端查询接口，查看指定包的详细信息，并将结果进行标准输出。

## Options

### registry

- 默认值：""
- 类型：URL

可以在 info 命令后面配置 --registry <registry> 参数，指定仓库地址；如果没有指定，默认从配置中获取仓库地址。

### fetch_timeout

- 默认值：60000
- 类型： Number
- 别名：ft

可以在 info 命令后面配置 --ft <number> 或者 --fetch_timeout <number> 参数，用以设置操作的超时时间，如果没有指定，默认超时时间为60000ms。

### strict_ssl

- 默认值：true
- 类型： Boolean

可以在 info 命令后面配置 --strict_ssl true 参数，校验 https 证书；配置 --strict_ssl false 参数，不校验https证书。

### pageNum

- 默认值：1
- 类型： Number

当field设置为versions时生效，可以在field后面配置 --pageNum <number> 参数，取值范围：[1, 10000]，表示在版本以列表分页展示时的页码数，可与pageSize一起使用。

### pageSize

- 默认值：100
- 类型： Number

当field设置为versions时生效，可以在field后面配置 --pageSize <number> 参数，取值范围：[1, 500]，表示在版本以列表形式分页展示时每页的版本数量，可与pageNum一起使用。

说明

上述选项中配置的registry，fetch_timeout和strict_ssl，仅在执行当前info命令时生效，不会修改项目级或者用户级的配置文件。

## Field

- keywords：查看三方库的关键词。
- dependencies：查看三方库的子依赖配置。
- tags：查看三方库的tag列表。
- versions：查看三方库版本列表，查询结果按照发布时间升序排列，以列表形式进行分页展示。可通过Options中[pageNum](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-info#section12987141924519)和[pageSize](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-info#section7425335114510)设置页码和每页数量，命令配置为versions --pageNum <number> --pageSize <number>。
- license：查看三方库的许可证。
- author：查看三方库的作者， 包括name 字段、 email 、url字段。
- repository：查看三方库的源码地址。
- dist：查看三方库的完整性字符串和.har包/.tgz包的下载地址。
- latest：查看三方库最新发布的版本。

说明

- tags：展示三方库的所有tag列表，不支持在依赖名称后通过@拼接具体version或tag实现过滤，如'ohpm info @ohos/lottie tags'等同于'ohpm info @ohos/lottie@latest tags'、'ohpm info @ohos/lottie tags'等同于'ohpm info @ohos/lottie@1.0.0 tags'。
- versions：分页展示三方库的版本列表，不支持在依赖名称后通过@拼接具体version或tag实现过滤。

## 示例

### 示例1

命令：

1. ohpm info @ohos/lottie --registry https://ohpm.openharmony.cn/ohpm

结果：

1. ➜ ohpm info @ohos/lottie --registry https://ohpm.openharmony.cn/ohpm

2. @ohos/lottie@2.0.10-rc.1 | MIT | deps: none | versions: 15
3. lottie是一个适用于OpenHarmony的动画库，它可以使用Bodymovin解析以json格式导出的Adobe After Effects动画，并在移动设备上进行本地渲染

4. keywords: OpenHarmony, HarmonyOS, Lottie

5. dist
6. .tarball: https://repo.harmonyos.com/ohpm/@ohos/lottie/-/lottie-2.0.10-rc.1.har
7. .integrity: sha512-fjdc1qJeEax+4/wA1eHdjvtLBOFxRGeU4J2F9Q1b+yRYjmZnzL6GCA241Ku5iyzG5j2RUZi6tyBa0rpyQnjhPg==

8. dist-tags:
9. latest: 2.0.10-rc.1

10. published 15 hours ago by ohos_tpc

### 示例2

命令：

1. ohpm info @ohos/imageknife --registry https://ohpm.openharmony.cn/ohpm/ keywords

结果：

1. OpenHarmony, ImageKnife, glide, HarmonyOS

### 示例3

命令：

1. ohpm info @ohos/lottie --registry https://ohpm.openharmony.cn/ohpm versions --pageNum 1 --pageSize 500

结果：

1. current page num: 1, total pages: 88
2. 2.0.0        2.0.1        2.0.10       2.0.10-rc.0  2.0.10-rc.1  2.0.10-rc.2  2.0.10-rc.3  2.0.10-rc.4  2.0.11       
3. 2.0.11-rc.0  2.0.11-rc.1  2.0.11-rc.2  2.0.11-rc.3  2.0.11-rc.4  2.0.11-rc.5  2.0.11-rc.6  2.0.11-rc.7  ......
# ohpm init

更新时间: 2025-12-16 15:59

创建 oh-package.json5 文件。

## 命令格式

1. ohpm init [options]

## 功能描述

在工作目录下，生成一个新的 oh-package.json5 文件，初始化一个 package。

执行命令时，命令行会出现交互界面，可填写一系列关于三方库的基本信息，例如：三方库名称、版本等。ohpm 会根据现有字段、依赖项和所选选项做出合理的猜测，它会保留已设置的任何字段和值，在工作目录下创建一个 oh-package.json5 文件。

## Options

### yes

- 默认值：null
- 类型：null 或 Boolean
- 别名：y

可以在 init 命令后面指定 -y或者--yes 参数，命令行将会完全跳过交互界面，创建默认的 oh-package.json5 文件。

默认内容如下：

1. {
2.     "name": "work_dir",
3.     "version": "1.0.0",
4.     "description": "",
5.     "main": "index.ets",
6.     "author": "",
7.     "license": "ISC",
8.     "dependencies": {}
9.   }

说明

若当前工作目录下不存在 oh-package.json5 文件，则文件中 name 字段默认为当前工作目录名称；若当前工作目录下已存在 oh-package.json5 文件，则新文件中 name 字段复用已存在文件中的 name 字段，并且最后覆盖原有oh-package.json5文件。

### group

- 默认值：当前项目的命名空间 或 ""
- 类型：String
- 别名：g

可以在 init 命令后面配置 -g <group_name> 或者 --group <group_name>参数，创建一个 oh-package.json5 文件，其中 name 字段的命名空间为 @group_name。

## 示例

- 当前工作目录下不存在 oh-package.json5 文件。
    
    在" D:\demo " 路径下，执行如下命令：
    
    1. ohpm init -y
    
    执行结果为：
    
    2. Wrote to D:\demo\oh-package.json5:
    
    3. {
    4.     "name": "demo",
    5.     "version": "1.0.0",
    6.     "description": "",
    7.     "main": "index.ets",
    8.     "author": "",
    9.     "license": "ISC",
    10.     "dependencies": {}
    11. }
    
- 当前工作目录下已存在其中 name 字段为 demo_name 的 oh-package.json5 文件。
    
    在" D:\demo " 路径下，执行如下命令：
    
    1. ohpm init -y
    
    执行结果为：
    
    2. Wrote to D:\demo\oh-package.json5:
    
    3. {
    4.     "name": "demo_name",
    5.     "version": "1.0.0",
    6.     "description": "",
    7.     "main": "index.ets",
    8.     "author": "",
    9.     "license": "ISC",
    10.     "dependencies": {}
    11. }
    
- 创建一个 oh-package.json5 文件，其中参数 name 字段为 "@group_name/demo" ，而不是仅为 "demo"。
    
    1. ohpm init -g group_name
    
    执行结果为：示例中 name 字段自动显示为 @group_name/demo。
    
    1. package name: (@group_name/demo)
    # ohpm install

更新时间: 2025-12-16 15:59

安装三方库。

## 命令格式

1. ohpm install [options] [[<@group>/]<pkg>[@<version> | @tag:<tag>]] ...
2. ohpm install [options] <folder> 
3. ohpm install [options] <har file>
4. alias: i

说明

- @group：三方库的命名空间，可选。
- pkg：三方库名称，可选；当 install 后面没有指定三方库名称时，会根据当前目录下 oh-package.json5 定义的依赖关系进行全量安装。
- version：三方库的版本号，可选。
- tag：三方库的标签，标签会标记三方库的某个版本号，可选。

## 功能描述

用于安装指定组件或 oh-package.json5 文件中所有的依赖。如果存在 oh-package-lock.json5 文件，安装将取决于 oh-package-lock.json5 文件中锁定的版本。

- ohpm install
    
    将依赖项安装到本地 oh_modules 文件夹中，并将所有依赖项作为 dependencies，写入 oh-package.json5 文件。
    
- ohpm install <folder>
    
    安装本地文件夹，则默认会创建一个软链接指向该文件夹。
    
    示例：
    
    1. ohpm install ../folder
    
- ohpm install <har file>
    
    安装压缩包，请注意压缩包的要求：
    
    1. 文件名必须使用 .tar, .tar.gz, .tgz, .har 作为扩展名；
    2. 压缩包里面包含子文件 package；
    3. 子文件夹 package 下面必须包含 oh-package.json5 文件，且配置文件中必须有 name 和 version 字段。
    
    示例：
    
    4. ohpm install ./package.har
    

## Options

### all

- 默认值：true
- 类型：Boolean

可以在 install 命令后面配置 --all 参数，安装您项目下所有模块在其 oh-package.json5 中配置的全部依赖项。

### save-dynamic

- 默认值：false
- 类型：Boolean

可以在 install 命令后面配置 --save-dynamic 参数，安装的三方库信息将会写入 oh-package.json5 文件的 dynamicDependencies 中。

### save-dev

- 默认值：false
- 类型：Boolean

可以在 install 命令后面配置 --save-dev 参数，安装的三方库信息将会写入 oh-package.json5 文件的 devDependencies 中。

### save-prod

- 默认值：true
- 类型：Boolean

可以在 install 命令后面配置 --save-prod 参数，安装的三方库信息将会写入 oh-package.json5 文件的 dependencies 中，这是 ohpm 的默认行为。

### no-save

- 默认值：false
- 类型：Boolean

可以在 install 命令后面配置 --no-save 参数，安装的三方库信息将不会写入 oh-package.json5 文件中。

### prefix

- 默认值：""
- 类型： string

可以在 install 命令后面配置 --prefix <string> 参数，用来指定包的根目录，该目录下必须存在 oh-package.json5 文件。

### parameterFile

- 默认值：无
- 类型： string
- 别名：pf

可以在 install 命令后面配置 --pf <string> 或者 --parameterFile <string> 参数，用来指定参数化配置文件地址。使用该命令前需保证项目级别的oh-package.json5中已配置parameterFile参数。

### registry

- 默认值：""
- 类型：URL

可以在 install 命令后面配置 --registry <registry> 参数，指定仓库地址；如果没有指定，默认从配置中获取仓库地址。

### fetch_timeout

- 默认值：60000
- 类型： Number
- 别名：ft

可以在 install 命令后面配置 --ft <number> 或者 --fetch_timeout <number> 参数，设置操作的超时时间，如果没有指定，默认超时时间为60000ms。

### strict_ssl

- 默认值：true
- 类型： Boolean

可以在 install 命令后面配置 --strict_ssl true 参数，校验 https 证书；配置 --strict_ssl false 参数，不校验 https 证书。

### max_concurrent

- 默认值：50
- 类型： Number
- 别名：mc

可以在 install 命令后面配置 --mc <number> 或者 --max_concurrent <number> 参数，设置最大活动并发请求数（即ohpm操作期间任何时间的最大网络请求数），如果没有指定，默认最大并发请求数为50次。

### retry_times

- 默认值：1
- 类型： Number
- 别名：rt

可以在 install 命令后面配置 --rt <number> 或者 --retry_times <number> 参数，设置操作失败前的最大重试次数，如果没有指定，默认最大重试次数为1次。

### retry_interval

- 默认值：1000
- 类型： Number
- 别名：ri

可以在 install 命令后面配置 --ri <number> 或者 --retry_interval <number> 参数，设置重试失败前的等待时间，如果没有指定，默认等待时间为1000ms。

### experimental-concurrently-safe

- 默认值：true
- 类型：Boolean

可以在 install 命令后面配置 --experimental-concurrently-safe 参数，并发安全地安装依赖。这是一个实验性选项。

### target_path

- 默认值：无
- 类型：string

可以在 install 命令后面配置 --target_path <string> 参数，用来指定在特定目标产物target语境下各模块的依赖配置文件（oh-package.json5）的路径。在执行ohpm install时，ohpm会优先安装<target_path>/<moduleName>/oh-package.json5文件中依赖。详情参见[target_path](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-install#section79331822125611)。

## 示例

安装 lottie 三方库，执行以下命令：

1. ohpm install @ohos/lottie

结果示例：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155955.33570779028853023354462086343206:50001231000000:2800:C22C1AF77A605CA2F1DFCD9C380CF0B79704F886368561D99D005F6B534EBD1E.png "点击放大")

## oh_modules

### ohpm 1.0.0~1.3.0

使用 ohpm 安装时，项目中各 Module 的依赖项被统一安装在 Module 根目录下的 oh_modules 目录中，Module 中所有直接依赖和间接依赖都以平铺的方式存储在 oh_modules 目录下的 .ohpm 目录中，Module 的直接依赖则以软链接的方式添加进 oh_modules 文件夹的根目录中。因此，相同依赖项只会安装一次，从而减少磁盘使用空间，加快安装速度。

### ohpm 1.4.x

ohpm 客户端从 1.4.0 版本开始，同一项目下所有 Module 的依赖都会被统一安装在项目根目录下的 oh_modules 目录中，同时会在项目各 Module 根目录下的 oh_modules 中生成该 Module 的直接依赖的软链接，这些软链接会指向**项目根目录**下 oh_modules 中的 .ohpm 目录下依赖实际存储目录。

## target_path

为了支持在构建过程中针对不同的产物定制不同的依赖，Hvigor会在构建时根据目标产物target为各模块自动生成定制的依赖配置文件（oh-package.json5），开发者可以在ohpm install时使用target_path选项来指定在特定目标产物target语境下各模块的依赖配置文件（oh-package.json5）的路径。

ohpm会优先安装<target_path>/moduleName/oh-package.json5文件中配置的依赖，并在<project_root>/moduleName下生成对应的oh-package-<targetName>-lock.json5文件。当指定target_path时，默认会开启依赖版本冲突自动处理功能，在依赖安装完成后，ohpm还会根据实际安装的依赖版本在<target_path>/resolve-conflict/moduleName目录下生成新的oh-package.json5文件。

target_path目录结构示例：

1. +---default                   // <targetName>默认为default
2. |   |   dependencyMap.json5   // 记录在特定target语境下的各模块依赖配置文件路径
3. |   +---module1               // 在特定target语境下某模块的依赖配置文件的存储目录，与原模块根目录同名
4. |   |       oh-package.json5  // 在特定target语境下某模块依赖配置文件
5. |   +---module2
6. |   |       oh-package.json5
7. |   |   oh-package.json5      // 在特定target语境下生成的工程级依赖配置文件

dependencyMap.json5内容示例：

1. {
2.   targetName: "default",
3.   rootDependency: "./oh-package.json5",
4.   dependencyMap: {
5.        "module1": "./module1/oh-package.json5",
6.        "module2": "./module2/oh-package.json5"
7.   }
8. }

**ohpm install指定target_path时依赖配置优先级说明：**

1、<target_path>/dependencyMap.json5中rootDependency配置的oh-package.json5的优先级高于<project_root>/oh-package.json5。

2、.ohpmrc中projectPackageJson指定的项目级配置文件中overrides、overrideDependencyMap配置优先级同时高于<target_path>/dependencyMap.json5中rootDependency配置的oh-package.json5中对应配置 和 <project_root>/oh-package.json5中对应配置。

3、<target_path>/moduleName/oh-package.json5的优先级高于overrideDependencyMap中的依赖配置文件。

4、overrides中的依赖版本优先级高于<target_path>/moduleName/oh-package.json5中对应的依赖版本。

注意

仅当<target_path>/dependencyMap.json5中targetName的值不为空且不等于'default'时，<project_root>/moduleName目录下生成的lock文件名才会变更为：oh-package-targetName-lock.json5。
# ohpm list

更新时间: 2025-12-16 15:59

列出已安装的三方库。

## 命令格式

1. ohpm list [options] [[<@group>/]<pkg>[@<version>]]
2. alias: ls

说明

- @group：三方库的命名空间，可选。
- pkg：三方库名称，可选。
- version：三方库的版本号，可选。

## 功能描述

以树形结构列出当前项目安装的所有三方库信息，以及它们的依赖关系。

当指定三方库名称时，会列出指定三方库名称的所有父依赖；当未指定三方库名称时，默认只列出所有的直接依赖，可通过添加选项 depth 来指定要打印的依赖层级。

## Options

### depth

- 默认值：0
- 类型：number
- 别名：d

可以在 list 命令后面配置 -d <number> 或者 --depth <number> 参数，设置输出树形结构的最大深度，超过该深度则不进行输出，不配置则取默认值 0，只展示直接依赖。

由于DevEco Studio控制台默认最多输出5000行，对于大工程建议通过 ohpm list -d <number> > fileName.txt 命令，将内容输出到指定文件中。

说明

若输出出现乱码问题，请执行 powershell -Command "(Get-Content 'fileName.txt') -replace ([char]27 + '\[[0-9;]*m'), ''" > result.txt，将内容输出到result.txt文件中。

### json

- 默认值：无
- 别名：j

可以在 list 命令后面配置 -j 或者 --json 参数，以 json 格式输出当前项目安装的所有三方库信息，以及它们的依赖关系。

### prefix

- 默认值：""
- 类型： string

可以在 list 命令后面配置 --prefix <string> 参数，用来指定包的根目录，该目录下必须存在 oh-package.json5 文件。

### parameterFile

- 默认值：无
- 类型： string
- 别名：pf

可以在 list 命令后面配置 --pf <string> 或者 --parameterFile <string> 参数，用来指定参数化配置文件地址。使用该命令前需保证项目级别的oh-package.json5中已配置parameterFile参数。

### recursive

- 默认值：无
- 别名：r

OHPM客户端从5.2.0版本开始，可以在 list 命令后面配置 -r 或者 --recursive 参数，以打印工程所有module安装的三方库信息，以及它们的依赖关系。

### target_path

- 默认值：无
- 类型：string

可以在 list 命令后面配置 --target_path <string> 参数，用来指定在特定目标产物target语境下各模块的依赖配置文件（oh-package.json5）的路径。在执行ohpm list时，ohpm会优先安装<target_path>/<moduleName>/oh-package.json5文件中依赖。详情参见[target_path](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-install#section79331822125611)。

## 示例

- 查看当前项目安装的**所有**三方库及依赖关系。
    
    执行以下命令：
    
    1. ohpm list
    
    结果示例：
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155956.15421448710791828281833909080645:50001231000000:2800:41A8BCB955DF9C5AF048A75C93E526BB928E48AC0A4F9E98A8EC1049C5336C72.png "点击放大")
    
- 查看当前项目安装的**某个**三方库的依赖关系
    
    执行以下命令：
    
    1. ohpm list universalify
    
    结果示例：
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155956.61102428953223231548643292228825:50001231000000:2800:E548853860292A8F9B7A2AD1F0B8C668B791DCC2C23F1717E573359FB36B1181.png)
    
- 查看当前项目所有module安装的**所有**三方库及依赖关系。
    
    执行以下命令：
    
    1. ohpm list -r
    
    结果示例：
    
    2. . D:\xxx\ProjectName
    3. └── @ohos/hypium 1.0.6
    
    4. module1 D:\xxx\ProjectName\module1
    5. ├─┬ lib1 1.0.0
    6. │ ├── lib1_sub1 1.0.0
    7. │ └── lib1_sub2 1.0.0
    8. └─┬ lib2 1.0.0
    9.   ├── lib2_sub1 1.0.0
    10.   └── lib2_sub2 1.0.0
    
    11. module2 D:\xxx\ProjectName\module2
    12. └── @ohos/lib3 1.0.0
    

- 指定target_path选项时，查看当前项目所有module安装的**所有**三方库及依赖关系。
    
    如果target_path目录下新增了module：dynamic，且module1新增了依赖：lib3，执行以下命令：
    
    1. ohpm list -r --target_path xxx/.hvigor/dependencyMap
    
    结果示例：
    
    2. . D:\xxx\ProjectName
    3. └── @ohos/hypium 1.0.6
    
    4. dynamic D:\xxx\ProjectName1\dynamic // target_path引入模块
    5. └── @ohos/lib4 1.0.0
    
    6. module1 D:\xxx\ProjectName\module1
    7. ├─┬ lib1 1.0.0
    8. │ ├── lib1_sub1 1.0.0
    9. │ └── lib1_sub2 1.0.0
    10. └─┬ lib2 1.0.0
    11.   ├── lib2_sub1 1.0.0
    12.   └── lib2_sub2 1.0.0
    13. └── lib3 1.0.0 // target_path新增依赖
    
    14. module2 D:\xxx\ProjectName\module2
    15. └── @ohos/lib3 1.0.0
    # ohpm publish

更新时间: 2025-12-16 15:59

发布一个三方库。

## 命令格式

1. ohpm publish [options] <har_or_tgz_file>

说明

- har_or_tgz_file：压缩包路径，可以是 .har 包格式和由 hsp 模块打包出来的 .tgz 包格式，必选参数。
- ohpm 命令行 1.3.0 之前版本仅支持发布 .har 包，从 1.3.0 版本开始支持发布 .tgz 包。
- ohpm命令行 5.0.1 版本开始支持发布与下载最大300M的.har/.tgz包。

## 功能描述

- 将三方库发布到 OpenHarmony 三方库中心仓，以便可按名称安装它。 发布前，需要完成公钥私钥生成，把公钥上传服务端，并在ohpmrc 文件中配置公仓的发布码和私钥路径。
- 默认情况下，ohpm 将发布到 [OpenHarmony 三方库中心仓](https://ohpm.openharmony.cn/#/cn/home)，但仍可以通过指定不同的 publish_registry 值（详情可查阅 [ohpmrc](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpmrc) 章节 中 publish_registry 描述信息），发布到指定的仓库。
- 如果指定的仓库中已存在三方库名称和版本组合，则发布失败。
- 一旦三方库以给定的名称和版本发布并审核通过后，该特定名称及对应的版本号将被占用，无法再次使用，即使它已被 [ohpm unpublish](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-unpublish) 下架。

注意

- 为了保证.har 和 .tgz 包的编译与运行正常，包中的 oh-package.json5 必须包含该包的所有直接依赖，若有依赖通过项目级别的 oh-package.json5 引入，则相应的依赖也必须写入包中对应的 oh-package.json5 中。
- 请注意debug模式构建的HAR包中含有源码，便于本地调试，请注意代码安全，详细请参考[构建HAR](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-har)。
- 发布包前请务必检查待发布包 oh-package.json5 的配置是否满足要求，具体要求请参考：[oh-package.json5 字段说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-oh-package-json5#zh-cn_topic_0000001792256137_oh-packagejson5-%E5%AD%97%E6%AE%B5%E8%AF%B4%E6%98%8E)

## 发布校验规则

### 三方库校验规则

1. ohpm打包的三方库须以.har和.tgz作为其扩展名；
2. 三方库所有内容须放置在package目录内，且package目录内需包含oh-package.json5配置文件、README.md文件、LICENSE文件和CHANGELOG.md文件，其中oh-package.json5配置文件须包含必选字段（请参阅[oh-package.json5](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-oh-package-json5)文件字段说明）；
    
    说明
    
    README.md文件、LICENSE文件和CHANGELOG.md三个文件在该HAR包发布至[OpenHarmony 三方库中心仓](https://ohpm.openharmony.cn/#/cn/help/publishrequirefile)时必须包含，且不能为空。
    
3. 将package目录压缩为tgz包，并将后缀名改为.har，即可获得三方库的HAR包。

### 开闭源规则

1. 开源
    
    不进行 ArkTS 代码相关编译的，只进行 cpp 代码编译和 OpenHarmony 资源处理，还有模块的部分原始配置文件会被打包。其 oh-package.json5 文件中的 "artifactType" 字段值为 original。
    
2. 闭源
    
    ArkTS 代码会被编译成混淆的 js 和 d.ets 和 d.ts 等声明文件，进行 cpp 代码编译和 OpenHarmony 资源处理，还有模块的部分原始配置文件会被打包。其 oh-package.json5 文件中 "artifactType" 属性值为 obfuscation。此时则检查 oh-package.json5 文件中 "types" 属性中定义的声明文件是否带有扩展名 ".d.ts/.d.ets"，且对应路径下存在该文件。若无则进行报错，且不会发布。
    

## Options

### publish_id

- 默认值：""
- 类型：String

可以在 publish 命令后面配置 --publish_id <id> 参数，指定发布码。

### key_path

- 默认值：""
- 类型：String

可以在 publish 命令后面配置 --key_path <p> 参数，指定ssh私钥路径。

### tag

- 默认值：无
- 类型：String
- 别名：t

可以在 publish 命令后面配置 -t <tag_name>或者 --tag <tag_name> 参数，给将要发布的三方库打上标签。

### publish_registry

- 默认值：""
- 类型：URL

可以在 publish 命令后面配置 --publish_registry <r> 参数，指定发布仓库地址。如果未指定，默认从配置中获取发布仓库地址。

### fetch_timeout

- 默认值：60000
- 类型： Number
- 别名：ft

可以在 publish 命令后面配置 --ft <number>或者 --fetch_timeout <number> 参数，设置操作的超时时间，如果没有指定，默认超时时间为60000ms。

### strict_ssl

- 默认值：true
- 类型： Boolean

可以在 publish 命令后面配置 --strict_ssl true 参数，校验 https 证书；配置 --strict_ssl false 参数，不校验 https 证书。

## 示例

发布工作目录下的三方库，执行以下命令：

1. ohpm publish publish_test.har

结果示例：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155956.05516726053290877534662468837198:50001231000000:2800:DCFD01D595055EFC94315879E835F78E012AC67F05C70B050B7F66D5C66B4C7E.png)

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-list "ohpm list")
# ohpm uninstall

更新时间: 2025-12-16 15:59

卸载三方库。

## 命令格式

1. ohpm uninstall [options] [<@group>/]<pkg> ...
2. alias: un

说明

- @group：三方库的命名空间，可选。
- pkg：三方库名称，必选。

## 功能描述

卸载指定已安装的模块，并将 oh-package.json5 文件中 dependencies、devDependencies 属性里移除指定三方库信息；若没有指定三方库，则不做任何动作。

如无需在 oh-package.json5 文件中 dependencies、devDependencies 属性里移除指定三方库信息，则可配置 --no-save 参数。

## Options

### all

- 默认值：false
- 类型：Boolean

您可以在 uninstall 命令后面配置 --all参数，表示卸载当前模块指定依赖成功后同时安装当前工程下的所有模块的依赖。

### no-save

- 默认值：false
- 类型：Boolean

您可以在 uninstall 命令后面配置 --no-save 参数，卸载的三方库信息不会从 oh-package.json5 文件中删除。

### prefix

- 默认值：""
- 类型： string

可以在 uninstall 命令后面配置 --prefix <string> 参数，用来指定包的根目录，该目录下必须存在 oh-package.json5 文件。

### registry

- 默认值：""
- 类型：URL

可以在 uninstall 命令后面配置 --registry <registry> 参数，当检测到oh-package.json5文件存在未安装的三方包时，卸载命令执行后，会自动从registry指定的仓库中下载并安装该三方包；如果没有指定，默认从配置中获取仓库地址。

### fetch_timeout

- 默认值：60000
- 类型：Number
- 别名：ft

可以在 uninstall 命令后面配置 --ft <number> 或者 --fetch_timeout <number> 参数，设置操作的超时时间，如果没有指定，默认超时时间为60000ms。

### strict_ssl

- 默认值：true
- 类型：Boolean

可以在 uninstall 命令后面配置 --strict_ssl true 参数，校验 https 证书；配置 --strict_ssl false 参数，不校验 https 证书。

### experimental-concurrently-safe

- 默认值：true
- 类型：Boolean

可以在 uninstall 命令后面配置 --experimental-concurrently-safe 参数，并发安全地安装依赖。这是一个实验性选项。

## 示例

从当前工程下卸载**直接**依赖的某个package。

执行以下命令：

1. ohpm uninstall lottie

说明

- ohpm 1.0.0~1.3.0
    - 使用 ohpm 卸载时，如果 json 是直接依赖的三方包，则当前工程 oh_modules 目录下文件夹 lottie 目录被删除，以及 json 对应的间接依赖也可能被删除（若间接依赖的包没有被其他三方包关联引用的情况下）。
    - oh-package.json5 文件中 dependencies 属性删除对应的行（例如："lottie": "2.0.7"）。
- ohpm 1.4.x
    - ohpm 客户端从 1.4.0 版本开始，使用 ohpm 卸载时，项目级 oh_modules 目录下的文件夹 lottie 目录**不会**被删除，模块级 oh_modules 目录下的文件夹 lottie 目录会被删除。
    - oh-package.json5 文件中 dependencies 属性删除对应的行（例如："lottie": "2.0.7"）。
    # ohpm prepublish

更新时间: 2025-12-16 15:59

预发布一个三方库。

## 命令格式

1. ohpm prepublish [options] <har_or_tgz_file>

说明

- har_or_tgz_file：压缩包路径，可以是 .har 包格式和由 hsp 模块打包出来的 .tgz 包格式，必选参数。
- ohpm v1.8.0 版本开始支持prepublish命令。

## 功能描述

- 拥有publish命令的所有内容校验规则，可以在发布前检测待发布的三方库能否通过ohpm客户端校验。
- 只校验待发布三方库内容，不对publish_registry、publish_id、key_path等做校验。
- 包的格式、结构及具体校验规则可参考[publish命令说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-publish)。

## Options

无。

## 示例

预发布工作目录下的三方库，执行以下命令：

1. ohpm prepublish publish_test.har

结果示例：

1. C:\Program Files\Huawei\DevEco Studio\tools\ohpm\bin> ohpm prepublish D:\publish_test.har
2. prepublish publish_test 1.0.0 succeed.
# ohpm uninstall

更新时间: 2025-12-16 15:59

卸载三方库。

## 命令格式

1. ohpm uninstall [options] [<@group>/]<pkg> ...
2. alias: un

说明

- @group：三方库的命名空间，可选。
- pkg：三方库名称，必选。

## 功能描述

卸载指定已安装的模块，并将 oh-package.json5 文件中 dependencies、devDependencies 属性里移除指定三方库信息；若没有指定三方库，则不做任何动作。

如无需在 oh-package.json5 文件中 dependencies、devDependencies 属性里移除指定三方库信息，则可配置 --no-save 参数。

## Options

### all

- 默认值：false
- 类型：Boolean

您可以在 uninstall 命令后面配置 --all参数，表示卸载当前模块指定依赖成功后同时安装当前工程下的所有模块的依赖。

### no-save

- 默认值：false
- 类型：Boolean

您可以在 uninstall 命令后面配置 --no-save 参数，卸载的三方库信息不会从 oh-package.json5 文件中删除。

### prefix

- 默认值：""
- 类型： string

可以在 uninstall 命令后面配置 --prefix <string> 参数，用来指定包的根目录，该目录下必须存在 oh-package.json5 文件。

### registry

- 默认值：""
- 类型：URL

可以在 uninstall 命令后面配置 --registry <registry> 参数，当检测到oh-package.json5文件存在未安装的三方包时，卸载命令执行后，会自动从registry指定的仓库中下载并安装该三方包；如果没有指定，默认从配置中获取仓库地址。

### fetch_timeout

- 默认值：60000
- 类型：Number
- 别名：ft

可以在 uninstall 命令后面配置 --ft <number> 或者 --fetch_timeout <number> 参数，设置操作的超时时间，如果没有指定，默认超时时间为60000ms。

### strict_ssl

- 默认值：true
- 类型：Boolean

可以在 uninstall 命令后面配置 --strict_ssl true 参数，校验 https 证书；配置 --strict_ssl false 参数，不校验 https 证书。

### experimental-concurrently-safe

- 默认值：true
- 类型：Boolean

可以在 uninstall 命令后面配置 --experimental-concurrently-safe 参数，并发安全地安装依赖。这是一个实验性选项。

## 示例

从当前工程下卸载**直接**依赖的某个package。

执行以下命令：

1. ohpm uninstall lottie

说明

- ohpm 1.0.0~1.3.0
    - 使用 ohpm 卸载时，如果 json 是直接依赖的三方包，则当前工程 oh_modules 目录下文件夹 lottie 目录被删除，以及 json 对应的间接依赖也可能被删除（若间接依赖的包没有被其他三方包关联引用的情况下）。
    - oh-package.json5 文件中 dependencies 属性删除对应的行（例如："lottie": "2.0.7"）。
- ohpm 1.4.x
    - ohpm 客户端从 1.4.0 版本开始，使用 ohpm 卸载时，项目级 oh_modules 目录下的文件夹 lottie 目录**不会**被删除，模块级 oh_modules 目录下的文件夹 lottie 目录会被删除。
    - oh-package.json5 文件中 dependencies 属性删除对应的行（例如："lottie": "2.0.7"）。
    - # ohpm prepublish

更新时间: 2025-12-16 15:59

预发布一个三方库。

## 命令格式

1. ohpm prepublish [options] <har_or_tgz_file>

说明

- har_or_tgz_file：压缩包路径，可以是 .har 包格式和由 hsp 模块打包出来的 .tgz 包格式，必选参数。
- ohpm v1.8.0 版本开始支持prepublish命令。

## 功能描述

- 拥有publish命令的所有内容校验规则，可以在发布前检测待发布的三方库能否通过ohpm客户端校验。
- 只校验待发布三方库内容，不对publish_registry、publish_id、key_path等做校验。
- 包的格式、结构及具体校验规则可参考[publish命令说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-publish)。

## Options

无。

## 示例

预发布工作目录下的三方库，执行以下命令：

1. ohpm prepublish publish_test.har

结果示例：

1. C:\Program Files\Huawei\DevEco Studio\tools\ohpm\bin> ohpm prepublish D:\publish_test.har
2. prepublish publish_test 1.0.0 succeed.
# ohpm unpublish

更新时间: 2025-12-16 15:59

下架已发布的三方库。

## 命令格式

1. ohpm unpublish [options] [<@group>]<pkg>[@<version>]

说明

- @group：三方库的命名空间，可选。
- pkg：三方库名称，必选。
- version：三方库的版本号，可选。

## 功能描述

- 从 OpenHarmony 三方库中心仓下架已经发布并审核通过上架的三方库。
- 若不指定版本，则默认下架三方库的所有版本，并且需要加上 -f 配置参数；全部版本均下架后，在 24h 内则不允许重新发布相同名称的三方库。
- 若下架了某个版本，该版本号不允许再次使用，后续发布必须使用新的版本号。
- 若此三方库被其它三方库依赖，则不删除，而是打上 deprecated 的标签；若没有被依赖，则直接删除。

## Options

### force

- 默认值：false
- 类型：Boolean
- 别名：f

强制下架。

### publish_registry

- 默认值：""
- 类型：URL

可以在 unpublish 命令后面配置 --publish_registry <r> 参数，指定发布仓库地址。如果未指定，默认从配置中获取发布仓库地址。

### publish_id

- 默认值：""
- 类型：String

可以在 unpublish 命令后面配置 --publish_id <id> 参数，指定发布码。

### key_path

- 默认值：""
- 类型：String

可以在 unpublish 命令后面配置 --key_path <p> 参数，指定ssh私钥路径。

### fetch_timeout

- 默认值：60000
- 类型： Number
- 别名：ft

可以在 unpublish 命令后面配置 --ft, --fetch_timeout <number> 参数，设置操作的超时时间，如果没有指定，默认超时时间为60000ms。

### strict_ssl

- 默认值：true
- 类型： Boolean

可以在 unpublish 命令后面配置 --strict_ssl true 参数，校验 https 证书；配置 --strict_ssl false 参数，不校验 https 证书。

## 示例

下架已发布的三方库，执行以下命令：

1. ohpm unpublish demo@1.0.0 -f

结果示例：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155956.83531500641522619550322692408680:50001231000000:2800:E58B82B7FE1CF7AC49F3D40DEBB4209EEDBE369E6089B6F94E427D0A9446CE74.png "点击放大")
# ohpm update

更新时间: 2025-12-16 15:59

更新三方库。

## 命令格式

1. ohpm update [options] [[<@group>/]<pkg>] ...
2. alias: up

说明

- @group：三方库的命名空间，可选。
- pkg：三方库名称，可选。

## 功能描述

根据三方库及其依赖版本号的 [semver](https://semver.org/) 规范，将本地安装的三方库更新到最新版本。若未指定三方库名称，则全量更新当前工程的依赖，且会安装缺少的三方库。

## Options

### all

- 默认值：false
- 类型：Boolean

您可以在 update 命令后面配置 --all 参数，表示更新当前模块指定依赖成功后同时安装当前工程下的所有模块的依赖。

### prefix

- 默认值：""
- 类型： string

可以在 update 命令后面配置 --prefix <string> 参数，用来指定包的根目录，该目录下必须存在 oh-package.json5 文件。

### fetch_timeout

- 默认值：60000
- 类型： Number
- 别名：ft

可以在 update 命令后面配置 --ft <number>或者 --fetch_timeout <number> 参数，设置操作的超时时间，如果没有指定，默认超时时间为 60000 ms。

### max_concurrent

- 默认值：50
- 类型： Number
- 别名：mc

可以在 update 命令后面配置 --mc <number> 或者 --max_concurrent <number> 参数，设置最大活动并发请求数（即 ohpm 操作期间任何时间的最大网络请求数），如果没有指定，默认最大并发请求数为 50 次。

### retry_times

- 默认值：1
- 类型： Number
- 别名：rt

可以在 update 命令后面配置 --rt <number> 或者 --retry_times <number> 参数，设置操作失败前的最大重试次数，如果没有指定，默认最大重试次数为 1 次。

### retry_interval

- 默认值：1000
- 类型： Number
- 别名：ri

可以在 update 命令后面配置 --ri <number> 或者 --retry_interval <number> 参数，设置重试失败前的等待时间，如果没有指定，默认等待时间为 1000 ms。

### strict_ssl

- 默认值：true
- 类型： Boolean

可以在 update 命令后面配置 --strict_ssl true 参数，校验 https 证书；配置 --strict_ssl false 参数，不校验 https 证书。

### registry

- 默认值：""
- 类型：URL

可以在 update 命令后面配置 --registry <registry> 参数，指定仓库地址；如果没有指定，默认从配置中获取仓库地址。

### all-modules

- 默认值：""
- 类型：Boolean

可以在 update 命令后面配置 --all-modules 参数，表示同步更新所有模块的依赖关系。

### tag-filter

- 默认值：无
- 类型：Regex

可以在 update 命令后面配置 --tag-filter <regex> 参数，表示更新以tag为规范，只更新tag符合正则表达式的依赖。使用 --tag-filter 参数默认更新所有模块的依赖关系。

### experimental-concurrently-safe

- 默认值：true
- 类型：Boolean

可以在 update 命令后面配置 --experimental-concurrently-safe 参数，并发安全地安装依赖。这是一个实验性选项。

## 示例

若当前三方库是 APP，且它的依赖项为：dep1 ( dep2，...)，dep1 已发布的版本有：

1. {
2.   "dist-tags": { "latest": "1.2.2", "release": "1.2.0" },
3.   "versions": [
4.     "1.2.2",
5.     "1.2.1",
6.     "1.2.0",
7.     "1.1.2",
8.     "1.1.1",
9.     "1.0.0",
10.     "0.4.1",
11.     "0.4.0",
12.     "0.2.0"
13.   ]
14. }

### ^ 依赖项

使用^符号会更新到版本 x.y.z 中 y 和 z 的最新版本。如果 APP 中 oh-package.json5 文件中 dep1 的版本号为：

1. "dependencies": {
2.   "dep1": "^1.1.1"
3. }

ohpm update 则安装 dep1@1.2.2，因为最新版本指向 1.2.2，且1.2.2 满足 ^1.1.1。

### ~ 依赖项

使用~符号会更新到版本 x.y.z 中 z 的最新版本。如果 APP 中 oh-package.json5 文件中 dep1 的版本号为：

1. "dependencies": {
2.   "dep1": "~1.1.1"
3. }

ohpm update 则安装 dep1@1.1.2，尽管最新版本指向 1.2.2，但 1.2.2 不满足 ~1.1.1（版本号须 1.1.1 ≤ version < 1.2.0），所以 ~1.1.1 使用满足最高排序版本，即1.1.2 ，进行更新。

### tag 依赖项

使用 tag 会更新到 tag 对应的版本。如果 APP 中 oh-package.json5 文件中 dep1 的版本号为：

1. "dependencies": {
2.   "dep1": "tag:release"
3. }

如果此时 release 标签对应版本被变更为 1.2.2，ohpm update --tag-filter ^r 则会将 dep1@1.2.0 更新为 dep1@1.2.2，因为 dep1 是通过 release 标签引入，release 符合 --tag-filter 指定的 ^r 正则表达式，所以会重新获取 release 标签对应的版本 1.2.2。

### 低于 1.0.0 版本的 ^ 依赖项

- 如果 APP 中 dep1 依赖版本号低于 1.0.0 且带有 ^，例如：
    
    1. "dependencies": {
    2.   "dep1": "^0.2.0"
    3. }
    
    ohpm update 则安装 dep1@0.2.0，因为没有其他版本满足 ^0.2.0。
    
- 但是 dep1 依赖版本号是 ^0.4.0：
    
    1. "dependencies": {
    2.   "dep1": "^0.4.0"
    3. }
    
    ohpm update 则安装 dep1@0.4.1，因为它是满足 ^0.4.0（版本号须 0.4.0 ≤ version < 0.5.0）的最高排序版本。
    

[ohpm unpublish](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-unpublish "ohpm unpublish")
# ohpm root

更新时间: 2025-12-16 15:59

在标准输出中打印有效的 oh_modules 目录路径信息。

## 命令格式

1. ohpm root

## 功能描述

可以在模块的任意子目录下执行，用于打印命令工作路径下所在包的有效 oh_modules 目录路径信息。

## Options

### prefix

- 默认值：""
- 类型： string

可以在 root 命令后面配置 --prefix <string> 参数，用来指定包的根目录，该目录下必须存在 oh-package.json5 文件，将会打印该根目录中有效的 oh_modules 目录路径信息。

## 示例

项目结构为：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155956.00711962584539611901488633133061:50001231000000:2800:D54BD151D51040CE342E711286AA12FEEC46D5B6F0B61F6C22870447A976448B.png)

在entry模块的src目录下执行：

1. ohpm root

结果示例：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155956.89313403642657432428009265836067:50001231000000:2800:6E26872AE4DA21E50DAEC5E841AC1CF724AE159BB875E613991F679E60AF69FC.png)
# ohpm version

更新时间: 2025-12-16 15:59

管理模块版本。

## 命令格式

1. ohpm version [options] [<newversion> | major | minor | patch]

## 功能描述

在模块目录中运行此命令以获取或升级版本号，同时将数据回写入 oh-package.json5 中。

## 参数说明

### 无参数

当无参数使用ohpm version命令时，则会将当前模块的版本号打印至标准输出中。

### newversion

newversion 参数应为一个合法的语义化版本，命令会将当前模块版本改写为 newversion 并打印在标准输出中。

### major

当参数为 major 时，有以下几种情况：

- 若无先行版本号，则将主版本号递增 1，其他位置为 0；
- 若存在先行版本号：
    - 当次版本号、修订号都为 0 时，则主版本号不变，而将先行版本号删掉。即 1.0.0-beta.1 升级为 1.0.0；
    - 当次版本号、修订号任意一个不为 0 时，则将主版本号递增1，其他位置为 0，并删除先行版本号。即 1.0.1-beta.1 升级为 2.0.0。

### minor

当参数为 minor 时，固定主版本号，变化次版本号与修订号，有以下几种情况：

- 若无先行版本号，则将次版本号递增 1，修订号置为 0；
- 若存在先行版本号:
    - 当修订号为 0 时，则次版本号不变，而将先行版本号删除。即 1.1.0-beta.1 升级为 1.1.0;
    - 当修订号不为 0 时，则将次版本号递增 1，修订号置为 0，同时删除先行版本号，即 1.1.1-beta.1 升级为 1.2.0。

### patch

当参数为 patch 时，固定主版本号与次版本号，变化修订号，有以下几种情况：

- 若无先行版本号，则修订号递增 1。即 1.0.0 升级为 1.0.1；
- 若存在先行版本号，则仅删除先行版本号。即 1.0.0-beta.1 升级为 1.0.0。

## Options

### prefix

- 默认值：""
- 类型： string

可以在 version 命令后面配置 --prefix <string> 参数，用来指定包的根目录，该目录下必须存在 oh-package.json5 文件。

### parameterFile

- 默认值：无
- 类型： string
- 别名：pf

可以在 version 命令后面配置 --pf <string> 或者 --parameterFile <string> 参数，用来指定参数化配置文件地址。使用该命令前需保证项目级别的oh-package.json5中已配置parameterFile参数。

## 示例

当前模块为 entry，版本号为 1.0.0，在当前模块的根目录执行：

1. ohpm version

结果示例：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155957.06574601940096538738267637522435:50001231000000:2800:CE8419472441A1BDB94BF66EDCE7FF420D26DF338ECE62948EC59CF3173D9801.png "点击放大")

接着执行：

1. ohpm version 1.0.1-beta.1

结果示例：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155957.79526205211659260213248484886795:50001231000000:2800:40079C824FD0D9134F0C83F6F7E614FDEFAE20643168D62A77CE1A5275AE46C4.png "点击放大")

接着执行：

1. ohpm version major

结果示例：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155957.18608904654307676308124383548689:50001231000000:2800:4FE67607A1806006520B22CDB3366E336146B272F1C6F88070724B881A0E77AE.png "点击放大")

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-root "ohpm root")
# ohpm cache clean

更新时间: 2025-12-16 15:59

清理 ohpm 缓存文件夹。

## 命令格式

1. ohpm cache clean 

## 功能描述

用于清理 ohpm 缓存文件夹。

## 示例

清理 ohpm 缓存文件夹，可执行以下命令：

1. ohpm cache clean

结果示例：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155957.00336668166523051253326589059327:50001231000000:2800:246EF9EADBAC4422E03267C6A448ACADAABBC093AB064B7F43AC2FD2A0EC394E.png)

### 关于缓存设计的说明

ohpm 将缓存数据存储在配置的 cache 目录下名为 content-v1 的文件夹中，存储所有通过 http 请求获取的 HAR 包数据。包的路径使用包的 sha512 哈希值分割成 3 段，第 1、2 位作为第一级目录，哈希值第 3、4 位作为第二级目录，哈希值第 5 位到结尾的所有字符作为文件名。使用哈希值可以将文件较均匀地分布在各个目录下，分成 3 层目录结构避免一个目录下文件数量过多，可以提升文件索引效率。

### 配置

缓存的配置方式见 [ohpmrc](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpmrc) 。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-version "ohpm version")
# ohpm run

更新时间: 2025-12-16 15:59

执行用户自定义脚本。

## 命令格式

1. ohpm run [options] <script_name> [-- <args...>]

## 功能描述

- 指定运行定义在模块的 oh-package.json5 文件中 scripts 对象内的脚本。
    
    scripts对象内部支持"key":"value"方式配置多个待执行脚本。如以下示例所示，scriptName1、scriptName2、scriptName3为脚本别名（scriptName）；“echo hello”等为脚本内容（scriptContent），后续内容均参考此说明。
    
    oh-package.json5中scripts配置示例：
    
    1. {               
    2.   "scripts": {
    3.     "scriptName1": "echo hello",
    4.     "scriptName2": "ohpm run scriptName1",
    5.     // 标识符"--"后可以通过'-p'或'--p'形式指定参数key, 可以通过' '或'='连接参数值
    6.     "scriptName3": "node test.js -- -paramKey1 paramValue1 -paramKey2=paramValue2 --paramKey3 paramValue3"
    7.   }
    8. }
    
- 脚本内容中可以用ohpm run引用同一个 oh-package.json5 文件中其它脚本别名，如scriptName2；ohpm run 引用关系是一个有向无环图，不支持递归或循环引用。
- 在解析脚本内容出错时，ohpm run命令将直接提示相应错误。比如，脚本内容中引用了一个在同一oh-package.json5文件中不存在的脚本别名；或在执行ohpm run时，发现脚本别名引用关系存在环的情况。

### 传递参数

- ohpm run命令可以通过标识符“--”覆盖被引用脚本的参数或为被引用脚本传递额外的参数，如：
    
    1. ohpm run scriptName3 -- -paramKey1 newValue -paramKey4 paramValue4
    
    该示例表明，脚本scriptName3的参数paramKey1会被替换为newValue, 并新增一个参数paramKey4。
    
- 如果脚本内容为ohpm run scriptName且使用了标识符“--”，则该scriptName对应的脚本内容不能再包含ohpm run相关的描述，避免嵌套引用。

### 支持多命令

支持 && 和 || 两种命令连接符 （&& 和 || 没有优先级区分，命令从左到右执行，不支持用括号来改变各个子命令的优先级），详细请参见下方[示例](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-run#section157898418348)。

### 约束

|约束项|说明|
|:--|:--|
|scriptKey 命名约束|合法的 scriptKey 的名字可以包含字母（包含大小写），数字，ASCII 冒号 :，ASCII下划线 _ ，ASCII链接符 -，首字母必须是小写字母|
|scriptContent 约束|合法的scriptContent不能引用除ohpm run以外的其它ohpm命令|
|scriptContent 中使用 ohpm run 的约束|1、ohpm run 依赖的其它script别名必须在同一 oh-package.json5 中存在<br><br>2、ohpm run 引用关系是一个有向无环图，不支持递归或循环引用|

## Options

### prefix

可以通过 --prefix 指定包的根目录，该目录下必须存在 oh-package.json5 文件。不支持通过这种方式调用依赖包中的脚本别名。

1. ohpm run --prefix <path> <脚本别名>  

## 示例

下列所有示例的scripts配置均来自如下oh-package.json5：

1. {
2.   "name": "example",
3.   "version": "1.0.0",
4.   "description": "this is an example for ohpm run.",
5.   "main": "./src/index.ets",
6.   "author": "oh",
7.   "license": "ISC",
8.   "scripts": {
9.     "testLogic": "ohpm run testFail || ohpm run testSuc && ohpm run testSuc",
10.     "testFail": "test1",
11.     "testSuc": "echo hello"
12.   }
13.   ...
14. }

### 参数传递的使用示例

1. ohpm run script_name -- -arg1=1 --arg2=2 -arg3 3 --arg4 4

运行 script_name 的脚本，并指定脚本中参数arg1，arg2，arg3，arg4，取值分别为1，2，3，4，以上四种参数传递的方法均可生效。

### 成功示例

执行脚本testSuc，如下所示：

1. ohpm run testSuc

执行结果：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155957.64236444235824718913688833530259:50001231000000:2800:77327E5CA76066AD29E8FF02CB0AC8E68087739117A7EED2F68EA36C24D58055.png "点击放大")

### 失败示例

执行脚本testFail，如下所示：

1. ohpm run testFail

执行结果：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155957.29705663138157861129376873329229:50001231000000:2800:FC44FE9B12AD76E41F593121B346D55A4FA361CEC3296D878AE66A3C3F2F20AC.png "点击放大")

### 逻辑符(&&、||)使用示例

执行脚本testLogic，如下所示：

1. ohpm run testLogic

执行结果：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155957.49442953504583244602710594122602:50001231000000:2800:AF2E85A29ADA9DFA64B148856C67A376B270B0BFA3F4076E5410FAA5740A746F.png "点击放大")

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-cache "ohpm cache clean")
# ohpm --version

更新时间: 2025-12-16 15:59

查询 ohpm cli 安装版本。

## 命令格式

1. ohpm -v | --version

## 功能描述

- 打印命令行工具的版本号。
- 可在安装 ohpm 命令行工具之后，对安装版本信息进行校验。

## 示例

查询 ohpm cli 安装版本，可执行以下命令：

1. ohpm -v

结果示例：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155957.47294214166919246236039811844729:50001231000000:2800:60D8862019A3DB29FDCD821863CDD5E19C2189D790EB3C710E2DBBA712090926.png)

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-run "ohpm run")
# ohpm ping

更新时间: 2025-12-16 15:59

ping ohpm 仓库地址。

## 命令格式

1. ohpm ping

## 功能描述

对给定的或者是配置中的仓库地址进行身份验证。如果有效，将会输出相关信息，比如以下内容：

1. ohpm INFO: PING your_registry
2. ohpm INFO: PONG 255ms

否则将会输出错误信息，比如以下内容：

1. ohpm INFO: PING your_registry
2. ohpm ERROR: HttpCode 404, API ping in your_registry - Not Found

## Options

### registry

- 默认值：""
- 类型：URL

可以在 ping 命令后面配置 --registry <registry> 参数，指定仓库地址；如果没有指定，默认从配置中获取仓库地址。

### fetch_timeout

- 默认值：60000
- 类型： Number
- 别名：ft

可以在 ping 命令后面配置 --ft <number> 或者 --fetch_timeout <number> 参数，设置操作的超时时间，如果没有指定，默认超时时间为 60000 ms。

### strict_ssl

- 默认值：true
- 类型：Boolean

可以在 ping 命令后面配置 --strict_ssl true 参数，校验 https 证书；配置 --strict_ssl false 参数，不校验 https 证书。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm--version "ohpm --version")
# ohpm clean

更新时间: 2025-12-16 15:59

清理工程下所有模块的ohpm安装产物。

## 命令格式

1. ohpm clean|cls 

## 功能描述

清理工程下所有模块的oh_modules目录、oh-package-lock.json5文件和oh-package-targetName-lock.json5文件（指定选项--target_path安装时生成），清理完成后会在控制台打印耗时信息。

## Options

### keep-lockfile

- 默认值：false
- 类型： Boolean
- 别名：kl

可以在 clean 命令后面配置--kl或者--keep-lockfile参数，执行清理时会保留oh-package-lock.json5文件和oh-package-targetName-lock.json5文件（指定选项--target_path安装时生成）。

## 注意事项

- clean命令只会清理工程根目录和在build-profile.json5文件中modules节点下配置的模块。
- 当build-profile.json5文件不存在时，当前oh-package.json5文件所在目录即为工程根目录。

## 示例

当前工程为 test，子模块为testModule1，工程结构如下：

1. test 
2. |————testModule1   
3.      |————libs   
4.      |————oh-package.json5 
5. |————build-profile.json5 
6. |————oh-package.json5  

在当前工程的任意子目录执行（以libs目录下执行为例）：

1. ohpm clean 

结果示例：

1. D:\test\testModule1\libs>ohpm clean 
2. ohpm DEBUG: startClean. 
3. ohpm DEBUG: clean all modules under: D:\test 
4. ohpm DEBUG: begin to clean module: D:\test\testModule1 
5. ohpm DEBUG: begin to clean module: D:\test 
6. ohpm DEBUG: clean module: D:\test\testModule1 succeed. 
7. ohpm DEBUG: clean module: D:\test succeed. 
8. clean completed in 0s 67ms
# ohpm dist-tags

更新时间: 2025-12-16 15:59

tag可标记一个三方库的某个版本，在install时可用tag代替版本号安装包。

## 命令格式

1. ohpm dist-tags [subcommand] [<@group>/]<pkg>[@<version>] <tag>
2. alias: dist-tags

说明

- subcommand: 包含list、add、update、remove四个子命令。
- @group: 三方库的命名空间，可选。
- pkg: 三方库名称，必选。
- version: 三方库的版本号，在add、update子命令时必选。
- tag: 标签，在add、update、remove子命令时必选。tag必须以大小写字母或数字开头，只允许包含大小写字母、数字、点号(.)、下划线(_)和中划线(-)，最大长度为60个字符。

## 功能描述

操作tag。分为查看三方库的所有tag，给三方库的某个版本添加tag，修改tag到三方库的另一个版本，删除三方库的某个tag。

说明

"latest"是一个预设的标签，不允许直接通过dist-tags命令来进行修改。该标签自动指向最高的正式版本；若无正式版本，则默认指向最高的先行版本。

以第三方库a为例，假定其版本序列包括"1.0.1-beta"、"1.0.1"和"2.0.1-beta"，在这种情况下，"latest"会自动映射到"1.0.1"，因为它是当前最高的正式版本。

## 子命令

### list

1. ohpm dist-tags list [<@group>/]<pkg>
2. alias: ls

列出指定三方库的所有标签。输出结果中，`latest`标签始终位于首位，其他标签按照字典序排列显示。

### add

1. ohpm dist-tags add [<@group>/]<pkg>[@<version>] <tag>

给某个版本的三方库增加一个标签。若该三方库已存在相同标签，则添加操作将会失败。

### update

1. ohpm dist-tags update [<@group>/]<pkg>[@<version>] <tag>
2. alias: up

更新指定包的某个标签所对应的版本。如果指定的标签不存在，则更新操作将失败。

### remove

1. ohpm dist-tags remove [<@group>/]<pkg> <tag>
2. alias: rm

删除指定包的一个标签。如果该标签并未存在于包中，则删除操作将会失败。

## Options

### publish_id

- 默认值：""
- 类型：String

可以在 dist-tags 命令后面配置 --publish_id <id> 参数，指定发布码。

### key_path

- 默认值：""
- 类型：String

可以在 dist-tags 命令后面配置 --key_path <p> 参数，指定ssh私钥路径。

### registry

- 默认值：无
- 类型：URL

可以在 dist-tags 命令后面配置 --registry <registry> 参数，指定仓库地址；如果没有指定，默认从配置中获取仓库地址。

### publish_registry

- 默认值：""
- 类型：URL

可以在 dist-tags 命令后面配置 --publish_registry <r> 参数，指定发布仓库地址。如果未指定，默认从配置中获取发布仓库地址。

### fetch_timeout

- 默认值：60000
- 类型： Number
- 别名：ft

可以在 dist-tags 命令后面配置 --ft <number>或者 --fetch_timeout <number> 参数，设置操作的超时时间，如果没有指定，默认超时时间为60000ms。

### strict_ssl

- 默认值：true
- 类型： Boolean

可以在 dist-tags 命令后面配置 --strict_ssl true 参数，校验 https 证书；配置 --strict_ssl false 参数，不校验 https 证书。

## 示例

如果想要通过使用tag，在oh-package.json5文件中引入包@ohos/axios的1.0.0版本，步骤如下：

1. 通过ohpm dist-tags的子命令add，对包@ohos/axios的1.0.0版本添加标签名beta。

2. ohpm dist-tags add @ohos/axios@1.0.0 beta

3. 在oh-package.json5文件中，使用标签beta引入包@ohos/axios的1.0.0版本。

4. {
5.   "dependencies": {
6.     // tag标签引入，引入标签为"beta"对应的版本号1.0.0
7.     "@ohos/axios": "tag:beta"
8.   }
9.   ...
10.   ...
11. }
# ohpm convert

更新时间: 2025-12-16 15:59

将npm三方库转换为ohpm三方库。因为语法差异，转换时仅对文件进行格式转换，不修改原npm包的代码逻辑。若HAR包在转换后出现代码不兼容的报错，开发者需修改原npm包的代码做适配。

## 命令格式

1. ohpm convert [[<@group>/]<pkg>[@<version> | @tag:<tag>]] --registry <string> [--publish]
2. ohpm convert <node_modules_path> [--publish]

说明

- @group：三方库的命名空间，可选。
- pkg：三方库名称，必选。
- version：三方库的版本号，可选。
- tag：三方库的标签，标签会标记三方库的某个版本号，可选。

## 功能描述

将指定npm仓库中的某个包或者本地node_modules目录下的包转换成满足ohpm格式要求的HAR包，并保存至当前工作目录，转换后的包将支持上传至ohpm-repo私仓或OpenHarmony三方库中心仓。

- ohpm convert @group/pkg@version --registry <npm仓库地址>
    
    下载指定仓库中的某个包及其所有依赖项，并且将该包及其依赖转换为满足ohpm格式要求的HAR包。
    
- ohpm convert <node_modules_path>
    
    转换本地node_modules中的所有包为满足ohpm格式要求的HAR包，<node_modules_path>必须为npm执行install命令后生成的node_modules目录。
    
    示例：
    
    1. ohpm convert ./xxxx/node_modules
    

说明

ohpm convert命令仅保留npm包中package.json配置文件中的name、version、main、types、license、description、author、keywords、homepage、repository、artifactType、dependencies、devDependencies、dynamicDependencies、overrides、scripts、hooks，module、packageType、typesVersions、exports和jsnext:main字段，具体字段说明请参考[oh-package.json5 字段说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-oh-package-json5#zh-cn_topic_0000001792256137_oh-packagejson5-%E5%AD%97%E6%AE%B5%E8%AF%B4%E6%98%8E)。

## Options

### registry

- 默认值：无
- 类型：URL

可以在convert命令后面配置 --registry <registry> 参数，指定仓库地址。如果指定了--registry，convert命令将从远程仓库地址下载指定的包及其依赖后，进行转换处理。如果没有指定--registry，convert命令将从本地node_modules目录进行转换处理。

### publish

- 默认值：false
- 类型： Boolean

可以在 convert命令后面配置 --publish 参数 ，若指定该参数，执行convert命令前请确认.ohpmrc推包相关配置无误，当所有包转换完成后将根据.ohpmrc中的配置依次进行推包。

## 示例

**转换远程npm三方库中的包**

转换npm三方库中的axios包，执行以下命令：

1. ohpm convert axios --registry https://registry.npmjs.org/

结果示例：

1. PS C:\Users\xxxxx\Desktop> ohpm convert axios --registry https://registry.npmjs.org
2. ...
3. ohpm INFO: > start convert package: asynckit@0.4.0
4. ohpm INFO: > start convert package: axios@1.6.8
5. ohpm INFO: > start convert package: combined-stream@1.0.8
6. ...
7. ohpm INFO: A total of 9 packets are converted successfully.
8. ohpm INFO: Converted packages are saved to the "C:\Users\xxxxx\Desktop\convert_1712127991590" directory.

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155957.69442265737423015372631190128618:50001231000000:2800:4A5193EAFDD7451C7392741D1D636A897016106F80CC7F55E368D124DE25BA44.png "点击放大")

**转换本地node_modules目录中的包**

执行npm install uuid后，转换本地node_modules目录中的包，执行以下命令：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155957.39430447562490500184569883987447:50001231000000:2800:FD6ABEB6FF62A527A8F8AFF5B04B655BD1D23B7A524DCD71442752E9E1F1FA1D.png)

1. ohpm convert C:\Users\xxxxx\Desktop\uuidInstallDir\node_modules

结果示例：

1. PS C:\Users\xxxxx\Desktop> ohpm convert C:\Users\xxxxx\Desktop\uuidInstallDir\node_modules
2. ohpm INFO: > start convert package: uuid
3. ...
4. ohpm INFO: A total of 1 package(s) are converted successfully.
5. ohpm INFO: Converted packages are saved to the "C:\Users\xxxxx\Desktop\convert_1712128912583" directory.
# 搭建流水线

更新时间: 2025-12-16 15:59

除了使用DevEco Studio一键式构建应用/元服务外，还可以使用命令行工具来调用Hvigor任务进行构建。通过命令行的方式构建应用或元服务，可用于构建CI（Continuous Integration）流水线，按照计划时间自动化地构建HAP/APP、签名、安装运行等操作。

通过命令行方式构建应用或元服务，可在Windows、Linux和macOS下调用相应命令来执行，本文将以Linux系统为例进行讲解，包括准备构建环境、构建HAP、签名运行等操作。在调用命令行任务上，Windows/macOS系统与Linux系统没有区别，仅在搭建构建环境上存在差异。

说明

- 如果开发者所使用的电脑处于完全无网络的环境中，搭建构建环境请参考[无网络流水线搭建](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-command-line-building-app#section15767113454814)。
- HarmonyOS SDK已嵌入命令行工具中，无需额外下载配置。
- 请在执行命令行之前，保证当前工程是可信任的，确保安全编译。

## 系统平台要求

- Linux：64位操作系统
    
- GLIBC：2.28或更高版本
    
- 内存：推荐使用16GB及以上，最小8GB
    
- 硬盘：100GB及以上
    

## 预置条件

### 配置JDK

1. 下载JDK，支持JDK 17版本。
2. 在Terminal里，进入JDK软件包目录，执行如下命令，解压已经下载好的安装包，其中jdk-17.0.6_linux-x64_bin.tar.gz为软件包名称，请根据实际配置进行修改。
    
    1. tar -xvf jdk-17.0.6_linux-x64_bin.tar.gz
    
3. 配置JDK环境变量。
    
    1. #jdk
    2. export JAVA_HOME=/opt/jdk-17.0.6_linux-x64_bin
    3. export PATH=$PATH:$JAVA_HOME/bin
    
4. 执行如下命令，检查JDK安装结果。
    
    1. java -version
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155952.28959097490276839221644841142591:50001231000000:2800:12F8FFC39441E797F95CD2355C20644CEE42972E6A9D435F250937BAE010544C.png)
    

### 获取命令行工具

1. [命令行工具获取](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-commandline-get#section21298572437)。其他系统(Windows/macOS)请根据实际情况下载对应版本。
2. 解压该压缩包，在sdk-linux-xxx/commandline目录下找到命令行工具压缩包commandline-tools-linux-xxx.zip。
3. 执行如下命令，解压命令行工具，工具名称请根据实际情况进行修改。
    
    1. unzip commandline-tools-linux-x64-5.0.3.XXX.zip
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155952.50627740461208347669430452762121:50001231000000:2800:97DA8132546E6284E6DFCF923638120E0B926383E69F84F109814BDC8A3C3949.png)
    
    将解压后所在的路径定义为COMMANDLINE_TOOL_DIR，在后续配置Node、hdc、hvigor、ohpm工具环境变量时使用。
    

### 配置Node.js环境变量

命令行工具包含了配套的Node.js，按照以下步骤配置环境变量。

1. 配置Node.js环境变量。
    
    1. # Linux系统
    2. export NODE_HOME=${COMMANDLINE_TOOL_DIR}/command-line-tools/tool/node
    3. export PATH=$PATH:$NODE_HOME/bin
    
    说明
    
    不同系统的Node.js所在路径不同，Windows存放在tool/node目录下，Linux和macOS存放在tool/node/bin目录下。
    
2. 执行如下命令，查询Node.js版本信息，确认配置成功。
    
    1. node -v
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155952.56641571134508410139159116313828:50001231000000:2800:36C7FAF39B9E088DF9FF49065FECE191D63A9683A8428D25A80D83B95819401F.png)
    

说明

建议使用命令行工具中自带的Node.js工具，若另外单独下载配置其他版本的Node.js，请确保不低于v18.0.0版本。

### 配置hdc环境变量

hdc命令行工具是调试HarmonyOS应用/元服务的工具，该工具存放在命令行工具自带的sdk下的toolchains目录中。为方便使用hdc命令行工具，请将其添加到环境变量中。

1. 请先完成[获取命令行工具](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-command-line-building-app#section88316312414)。
2. 添加hdc路径到环境变量，指令如下。
    
    hdc工具存放路径示例：${COMMANDLINE_TOOL_DIR}/command-line-tools/sdk/default/openharmony/toolchains。
    
    1. export HDC_HOME=${COMMANDLINE_TOOL_DIR}/command-line-tools/sdk/default/openharmony/toolchains
    2. export PATH=$PATH:$HDC_HOME
    

### 配置hvigor环境变量

1. 请先完成[获取命令行工具](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-command-line-building-app#section88316312414)。
2. 添加hvigorw路径到PATH环境变量，指令如下。
    
    1. export PATH=${COMMANDLINE_TOOL_DIR}/command-line-tools/bin:$PATH
    
3. 切换到工程根目录，执行如下命令，查询Hvigor版本信息，确认安装成功。
    
    1. hvigorw -v
    

### 配置npm镜像仓库

若您的工程在hvigor/hvigor-config.json5文件中依赖npm三方组件，流水线中则需要配置npm镜像地址，编译时才能正确地下载它。

1. npm config set registry https://repo.huaweicloud.com/repository/npm/
2. npm config set "@ohos:registry" https://repo.harmonyos.com/npm/

### 安装ohpm

1. 请先完成[获取命令行工具](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-command-line-building-app#section88316312414)。
2. 添加ohpm路径到环境变量，指令如下。
    
    1. export PATH=${COMMANDLINE_TOOL_DIR}/command-line-tools/bin:$PATH
    
3. 执行如下命令，查询ohpm版本信息，确认安装成功。
    
    1. ohpm -v
    
4. 配置仓库地址（可指定多个地址，','号分割），指令如下。
    
    1. ohpm config set registry https://ohpm.openharmony.cn/ohpm/
    2. ohpm config set strict_ssl false
    

### 安装libGL1库

在linux系统的构建场景下，使用[纹理压缩](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile-app#section2095319147103)功能需要安装libGL1库。例如Ubuntu/Debian上安装libgl1-mesa-dev，CentOS/RHEL上安装mesa-libGL-devel。

以libgl1-mesa-dev为例，执行以下命令安装，其他系统请替换成实际的包名。

1. apt install -y libgl1-mesa-dev

## 构建应用

### 安装工程及模块依赖

使用命令行进行构建前，需要分别进入工程及各个模块下执行ohpm install命令，安装**工程及各个模块**依赖的三方库。

1. 定义ohpm安装函数，示例如下。
    
    1. # 切换到指定目录$1并执行ohpm install指令
    2. function ohpm_install() {     
    3.     cd $1              # $1：函数第一个参数, 必须是路径     
    4.     ohpm install --all # 安装所有依赖
    5. }
    
2. 定义变量 **PROJECT_PATH**，表示工程目录路径，示例如下。
    
    1. PROJECT_PATH=xxx/xxx/project_name  # 工程路径
    
    注意
    
    工程目录不要存放在隐藏目录下，即工程路径的每一级目录中不要以.开头，例如xxx/.xxx/project，否则构建时可能会将模块中的代码和配置文件等作为资源打包进产物中，不会进行混淆或加密。
    
3. 安装工程及各个模块的三方库依赖，示例如下。
    
    1. # 根据业务情况安装ohpm三方库依赖
    2. ohpm_install "${PROJECT_PATH}"
    3. ...
    

### 执行Hvigor命令进行构建

1. 使用hvigorw命令行工具执行构建命令。
    
    1. # 根据业务情况，执行相应的构建命令, 示例如下
    
    2. # clean工程
    3. hvigorw clean --no-daemon
    
    4. # 构建Hap, 生成产物：${PROJECT_PATH}/{moduleName}/build/{productName}/outputs/{targetName}/xxx.hap
    5. hvigorw assembleHap --mode module -p product=default -p buildMode=debug --no-daemon
    
    6. # 构建Hsp, 生成产物：${PROJECT_PATH}/{moduleName}/build/{productName}/outputs/{targetName}/(xxx.har | xxx.hsp)
    7. hvigorw assembleHsp --mode module -p module=library@default -p product=default --no-daemon
    
    8. # 构建Har, 生成产物：${PROJECT_PATH}/{moduleName}/build/{productName}/outputs/{targetName}/outputs/xxx.har
    9. hvigorw assembleHar --mode module -p module=library1@default -p product=default --no-daemon
    
    10. # 构建App, 生成产物: ${PROJECT_PATH}/build/outputs/{productName}/xxx.app
    11. hvigorw assembleApp --mode project -p product=default -p buildMode=debug --no-daemon
    
    - 如果在非daemon模式下，需要修改node内存配置，可在hvigorw文件中取消第15行的注释，并配置对应的数值。如将node内存配置为10240，示例如下：
        
        1. NODE_OPTS="--max-old-space-size=10240"
        
    - 如果是在daemon模式下，请参考[设置守护进程内存](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-daemon#section327617383145)。
    - 本文使用Linux作为流水线构建环境，Linux环境会对大小写敏感，如果您的代码引用中有大小写错误（例如代码中import funcA from './aaa'，而实际文件为AAA.ets），而且开发环境是Windows或者Mac，那么有可能出现Windows或者Mac环境下编译通过，而Linux环境下编译不通过的现象。通过在项目级的build-profile.json5文件中配置caseSensitiveCheck为true来打开大小写敏感，保持Windows或者Mac环境编译与Linux环境编译结果一致。
        
        1. // build-profile.json5文件
        2. {
        3.     "name": "default",
        4.     "compatibleSdkVersion": "6.0.1(21)",
        5.     "runtimeOS": "HarmonyOS",
        6.     "buildOption": {
        7.       "strictMode": {
        8.     "caseSensitiveCheck" : true
        9.       }
        10.     }
        11. }
        
    
2. 构建命令完成后，工程或模块下build目录中会生成相应的hap/hsp/har/app编译产物。

编译构建常见的任务和扩展参数如下，更多关于Hvigor命令行参数详见：[常用命令](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-commandline#section16300629103)。

**表1** HarmonyOS应用构建常用扩展参数
|选项|说明|
|:--|:--|
|-p buildMode={debug \| release}|采用debug/release模式进行编译构建。<br><br>缺省时：构建Hap/Hsp/Har时为debug模式，构建App时为release模式。<br><br>关于构建模式的详细说明，请参考[指定构建模式](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-compilation-options-customizing-guide#section192461528194916)。针对HAR构建，请参考[构建HAR](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-har)。|
|-p product={ProductName}|指定product进行编译, 编译product下配置的module target。<br><br>缺省时：默认为default。|
|-p module={ModuleName}@{TargetName}|指定模块及target进行编译，可指定多个相同类型的模块进行编译以逗号分割；TargetName不指定时默认为default。<br><br>限制：此参数需要与--mode module参数搭配使用。<br><br>缺省时：执行AssembleHap任务会编译工程下所有模块，默认指定target为default。|
|-p ohos-test-coverage={true \| false}|执行测试框架代码覆盖率插桩编译。|

**表2** HarmonyOS应用编译构建相关任务
|选项|说明|
|:--|:--|
|clean|清理构建产物|
|assembleHap|构建Hap应用|
|assembleApp|构建App应用|
|assembleHsp|构建Hsp包|
|assembleHar|构建Har包|

## 运行应用

### 准备申请签名所需文件

准备好申请签名所需3个文件：密钥（.p12文件）、数字证书（.cer文件）、Profile（.p7b文件）。

**生成密钥和证书请求文件**

使用JDK携带的Keytool工具生成密钥和证书请求文件。

1. 参考[配置JDK](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-command-line-building-app#section195447475220)步骤配置环境变量后，打开命令行终端，执行如下命令，生成密钥库文件。例如，生成的密钥库名称为demo.p12，存储到path目录下。
    
    1. keytool -genkeypair -alias "demo_key" -keyalg EC -sigalg SHA256withECDSA -dname "C=CN,O=HUAWEI,OU=HUAWEI IDE,CN=demo_key"  -keystore /path/demo.p12 -storetype pkcs12 -validity 9125 -storepass 123456Abc -keypass 123456Abc
    
    关于该命令中需要修改的参数说明如下，其余参数不需要修改：
    
    - **alias**：密钥的别名信息，用于标识密钥名称。
    - **dname**：证书基本信息。
        - C：国家/地区代码，如CN。
        - O：组织名称，如HUAWEI。
        - OU：组织单位名称，如HUAWEI IDE。
        - CN：名字与姓氏，建议与别名一致。
    - **keystore**：密钥库文件，请将"/path/demo.p12"修改为实际路径。
    - **validity**：证书有效期，例如设置为9125（25年）。
    - **storepass**：设置密钥库密码，必须由大写字母、小写字母、数字和特殊符号中的两种以上字符的组合，长度至少为8位。请记住该密码，后续签名配置需要使用。
    - **keypass**：设置密钥的密码，请与**storepass**保持一致。
    
2. 执行如下命令，执行后需要输入**storepass**密码，生成**密钥**和**证书请求文件**。
    
    1. keytool -certreq -alias "demo_key" -keystore /path/demo.p12 -storetype pkcs12 -file /path/demo.csr
    
    生成证书请求文件的参数说明如下：
    
    - **alias**：与上一步骤中输入的**alias**保持一致。
    - **keystore**：与上一步骤中输入的**keystore**保持一致。
    - **file**：生成的证书请求文件名称，后缀为.csr，请将"/path/demo.csr"修改为实际路径。
    

**申请调试****数字证书和Profil****e****文件**

生成证书请求文件后，在AppGallery Connect中申请、下载调试数字证书和Profile文件，具体请参考[申请调试证书](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section081822416419)和[申请Profile文件和添加权限信息](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section89479413571)。

### 对HAP/APP进行签名

通过Hvigor打包生成的HAP不会携带签名信息，如果要在真机设备上运行HAP，需要使用签名工具对HAP进行签名。

1. 准备好签名工具hap_sign_tool.jar，在${COMMANDLINE_TOOL_DIR}/command-line-tools/sdk/default/openharmony/toolchains/lib下。
2. 在签名工具目录下，使用如下命令进行签名。详细的签名工具指导请参考[Hap包签名工具](https://gitee.com/openharmony/developtools_hapsigner)。
    
    1. java -jar hap-sign-tool.jar sign-app -keyAlias "demo_key" -signAlg "SHA256withECDSA" -mode "localSign" -appCertFile "/path/demo.cer" -profileFile "/path/demo.p7b" -inFile "/path/hap-unsigned.hap" -keystoreFile "/path/demo.p12" -outFile "/path/hap-signed.hap" -keyPwd "123456Abc" -keystorePwd "123456Abc"
    
    关于该命令中需要修改的参数说明如下，其余参数不需要修改：
    
    - **keyAlias**：密钥别名。
    - **appCertFile**：申请的调试证书文件，格式为.cer。
    - **profileFile**：申请的调试Profile文件，格式为.p7b。
    - **inFile**：通过Hvigor打包生成的未携带签名信息的HAP。
    - **keystoreFile**：密钥库文件，格式为.p12。
    - **outFile**：经过签名后生成的携带签名信息的HAP。
    - **keyPwd**：密钥密码。
    - **keystorePwd**：密钥库密码。
    
    说明
    
    如果要对APP进行签名，只需将**inFile**和**outFile**参数修改为APP包即可。
    

### 运行应用

通过[hdc工具](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/hdc)将HAP推送到真机设备上进行安装，需要注意的是，推送的HAP必须是携带签名信息的，否则会导致HAP安装失败。

推送HAP的命令如下：

1. # 将打包好的hap包推送至设备中
2. hdc file send "{PROJECT_PATH}/entry/build/default/outputs/default/entry-default-signed.hap" "data/local/tmp/entry-default-signed.hap"
3. # 安装hap包
4. hdc shell bm install -p "data/local/tmp/entry-default-signed.hap"
5. # 删除hap包
6. hdc shell rm -rf "data/local/tmp/entry-default-signed.hap"

在设备上运行HAP的命令如下：

1. hdc shell aa start -a EntryAbility -b com.example.myapplication -m entry

## 示例脚本

说明

此脚本无法直接运行，仅供参考，业务要根据自己的情况来进行适配。

1. #!/bin/bash
2. set -ex

3. JAVA_HOME=xxx #指定JDK的安装目录
4. COMMANDLINE_TOOL_DIR=xxx #命令行工具的安装目录

5. #配置hvigor、ohpm环境变量
6. export PATH=${COMMANDLINE_TOOL_DIR}/command-line-tools/bin:$PATH

7. #下载并配置JDK
8. function init_JDK() {
9.   if [ ! -d "${JAVA_HOME}" ]; then 
10.      mkdir "${JAVA_HOME}"
11.   fi
12.   cd ${JAVA_HOME}
13.   wget --no-check-certificate -q "${jdk下载路径}" -O jdk-linux.tar.xz #下载jdk，需要替换jdk下载路径
14.   tar -vxf jdk-linux.tar.xz
15.   JDK_DIR=xxx #jdk压缩包文件里面的目录
16.   cd ${JDK_DIR}
17.   mv -f ./* .[^.]* ../
18.   cd ..
19.   rm -rf JDK_DIR jdk-linux.tar.xz
20.   export JAVA_HOME=${JAVA_HOME}
21.   export PATH=$JAVA_HOME/bin:$PATH
22.   java -version
23. }

24. #配置hdc环境变量
25. function init_hdc() {
26.   export HDC_HOME=${COMMANDLINE_TOOL_DIR}/command-line-tools/sdk/default/openharmony/toolchains #设置hdc工具的环境变量，hdc工具在toolchains所在路径下
27.   export PATH=$HDC_HOME:$PATH
28. }

29. # 安装ohpm, 若镜像中已存在ohpm，则无需重新安装
30. function init_ohpm() {
31.     ohpm -v
32.     # 配置ohpm仓库地址
33.     ohpm config set registry https://ohpm.openharmony.cn/ohpm/
34. }

35. # 初始化相关路径
36. PROJECT_PATH=xxx  # 工程目录
37. # 进入package目录安装依赖
38. function ohpm_install {
39.     cd $1
40.     ohpm install
41. }
42. # 环境适配
43. function buildHAP() {
44.     # 根据业务情况安装ohpm三方库依赖
45.     ohpm_install "${PROJECT_PATH}"
46.     ohpm_install "${PROJECT_PATH}/entry"
47.     ohpm_install "${PROJECT_PATH}/xxx"
48.     # 根据业务情况，采用对应的构建命令，可以参考DevEco Studio构建日志中的命令
49.     cd ${PROJECT_PATH}
50.     hvigorw clean --no-daemon
51.     hvigorw assembleHap --mode module -p product=default -p debuggable=false --no-daemon # 流水线构建命令建议末尾加上--no-daemon
52. }
53. function install_hap() {
54.     hdc file send "${PROJECT_PATH}/entry/build/default/outputs/default/entry-default-signed.hap" "data/local/tmp/entry-default-signed.hap"
55.     hdc shell bm install -p "data/local/tmp/entry-default-signed.hap" 
56.     hdc shell rm -rf "data/local/tmp/entry-default-signed.hap"
57.     hdc shell aa start -a MainAbility -b com.example.myapplication -m entry
58. }

59. # 使用ohpm发布har
60. function upload_har {
61.   ohpm publish pkg.har
62. }

63. function main {
64.   local startTime=$(date '+%s')
65.   init_JDK
66.   init_hdc
67.   init_ohpm
68.   buildHAP
69.   install_hap
70.   upload_har
71.   local endTime=$(date '+%s')
72.   local elapsedTime=$(expr $endTime - $startTime)
73.   echo "build success in ${elapsedTime}s..."
74. }
75. main

## 无网络流水线搭建

如果开发者使用的电脑处于完全无网络的环境中，可参考以下步骤搭建流水线环境。

### 安装pnpm插件

1. 请在可访问网络的电脑上创建一个空文件夹，在文件夹中创建一个package.json文件，在文件中填写如下内容：
    
    1. {
    2.   "dependencies": {
    3.     "pnpm": "8.13.1"
    4.   }
    5. }
    
2. 先配置[环境变量](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-environment-config#zh-cn_topic_0000001056725590_li358362302311)，再打开[命令行工具](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-commandline-get)，在文件夹下执行 npm install 命令，会生成node_modules文件夹。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155953.79428875367283508318784712510636:50001231000000:2800:DD42D18E6949C55498C12885FEDE8EF6018BAEB80535703FA212C3FB715D2DCD.png)
    
3. 将node_modules文件夹和package.json文件拷贝到无网络电脑的C:\Users\_用户名目录_\.hvigor\wrapper\tools下（若当前无该目录，请手动创建）。
4. 在无网络电脑上执行如下命令，设置npm离线模式：
    
    1. npm config set offline true
    

### 安装npm依赖插件

1. 请在可访问网络的电脑上创建一个空文件夹，在文件夹中创建一个package.json文件，配置npm依赖，示例如下：
    
    1. {
    2.   "dependencies": {
    3.     "ajv": "latest"
    4.   }
    5. }
    
2. 打开[命令行工具](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-commandline-get)，在文件夹下执行 npm install 命令，会生成node_modules文件夹。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155953.44628166159745137365591144483849:50001231000000:2800:4BB61F3E649215B2F3AB221A44AF18B74724E95DA450D852050D0FC514EA402A.png)
    
3. 将node_modules文件夹拷贝到无网络电脑的工程根目录下。

### 安装ohpm依赖插件

请参考[安装三方库](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-no-network#section208435578175)。

### 安装libGL1库

在linux系统的构建场景下，使用[纹理压缩](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile-app#section2095319147103)功能需要安装libGL1库。

请在可访问网络的电脑上下载libGL1库，例如Ubuntu/Debian下载libgl1-mesa-dev，CentOS/RHEL下载mesa-libGL-devel，并将安装包拷贝到无网络电脑中进行安装。
# HarmonyOS 开发者测试服务概述

更新时间: 2025-12-16 16:56

本章节介绍HarmonyOS 开发者测试服务的所有环节，包括代码静态检查、单元测试、应用和元服务体检、UI测试、专项测试、上架预检测试、用户测试、应用性能监测服务和持续集成与交付（CI/CD）。

## 代码静态检查

[代码静态检查](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-code-check)是在不运行程序的情况下，通过分析代码的语法、结构、逻辑等静态特性来发现潜在问题的方法，能够帮助开发者在代码开发阶段确保代码质量。

## 单元测试

HarmonyOS 的[单元测试](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ut)基于测试框架执行。框架由核心模块和扩展模块组成：核心模块提供测试运行所需的基础接口和执行逻辑，并通过插件化机制向外提供接入能力和运行时上下文；扩展模块在核心能力之上补充常用功能，例如用例超时、筛选、数据驱动和压力测试等，并以插件形式接入核心模块。

## 应用与元服务体检

完成 HarmonyOS 应用/元服务开发后，开发者可以使用[应用与元服务体检](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-app-analyzer)工具进行开发自测试，快速发现应用/元服务在特定场景下性能、功耗、安全、稳定性、功能等方面的兼容性问题，并且通过工具提供的诊断建议快速定位到故障代码，从而快速进行修复。

## UI测试

通过简洁易用的API提供查找和操作界面控件能力，支持开发者编写基于界面操作的自动化测试脚本。

## 专项测试

[专项测试](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/test-service)包括兼容性、稳定性、安全、性能、功耗、UX等，开发者可以结合各维度的应用质量建议，通过提供的多种专项测试工具来保障应用质量。如果需要对指定代码段进行性能测试，开发者可以使用 DevEco Studio [白盒性能测试框架](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/perftest-guideline)。

## 上架预检测试

[上架预检测试](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/publish-testing)可以按照应用市场上架应用/元服务的标准进行测试，为开发者的 HarmonyOS 应用/元服务上架提供质量保证。检测结果可用于应用市场上架审核，提升上架审核通过率。

## 用户测试

HarmonyOS 应用正式上架之前，开发者可以邀请特定的内外部测试用户提前体验，收集测试用户的反馈意见以优化应用体验。

根据不同的体验测试阶段，开发者可以结合体验测试的目标用户群，自主选择或搭配使用三种用户测试方法：

如果开发者需要在开发团队内进行内部测试，可以选择[内部测试](https://developer.huawei.com/consumer/cn/doc/app/agc-help-internal-test-0000002270709477)。

如果开发者需要在特定用户群组来测试，可以选择[邀请测试](https://developer.huawei.com/consumer/cn/doc/app/agc-help-invite-test-0000002270829393)。

如果开发者需要面向全网公开招募部分用户测试，可以选择[公开测试](https://developer.huawei.com/consumer/cn/doc/app/agc-help-public-test-0000002287814841)。

## 应用性能监测服务

HarmonyOS 应用/元服务上架后，开发者可能会关注其在真实海量设备上运行的性能和稳定性，使用[应用性能监测服务](https://developer.huawei.com/consumer/cn/doc/app/agc-help-apms-0000002235870062)（英文简称APMS），一旦线上用户遇到卡顿或崩溃，开发者能第一时间收到预警，查看性能问题监测看板，并根据问题发生时的堆栈等信息快速分析，持续保障用户体验。

## 持续集成与交付（CI/CD）

使用 [CI/CD](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-command-line-building-app) [流水线](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-command-line-building-app)，开发者可以通过命令行集成华为官方的测试工具。通过 DevEco Studio 的命令行工具调用 Hvigor任务进行 HAP/APP 构建、签名、安装运行等操作。
# 单元测试框架使用指导

更新时间: 2025-12-15 15:40

## 概述

单元测试框架（JsUnit），是自动化测试框架基础底座，提供测试脚本识别、调度、执行和结果汇总的能力。开发者可在测试脚本中调用UI测试框架和白盒性能测试框架接口编写测试用例。

本指南介绍单元测试框架的主要功能、实现原理和开发步骤。

## 框架能力全景

单元测试框架支持的功能特性如下。

|特性|功能说明|
|:--|:--|
|[基础流程能力](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/unittest-guidelines#%E5%9F%BA%E7%A1%80%E6%B5%81%E7%A8%8B%E8%83%BD%E5%8A%9B)|支持测试用例识别调度及异步执行测试用例。|
|[断言能力](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/unittest-guidelines#%E6%96%AD%E8%A8%80%E8%83%BD%E5%8A%9B)|判断用例实际结果值与预期值是否相符。|
|[Mock能力](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/unittest-guidelines#mock%E8%83%BD%E5%8A%9B)|支持函数级Mock能力，对定义的函数进行Mock并修改函数的行为，使其返回指定的值或者执行指定操作。|
|[数据驱动能力](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/unittest-guidelines#%E6%95%B0%E6%8D%AE%E9%A9%B1%E5%8A%A8)|提供数据驱动能力，支持复用同一个测试脚本，使用不同输入数据驱动测试脚本执行。|
|[专项能力](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/unittest-guidelines#%E5%91%BD%E4%BB%A4%E8%A1%8C%E6%89%A7%E8%A1%8C%E6%B5%8B%E8%AF%95%E8%84%9A%E6%9C%AC)|支持测试套与用例筛选、随机执行、压力测试、超时设置、遇错即停模式和跳过执行模式。|

**图1.单元测试框架主要功能**

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251215154028.38820509581157420686104592632085:50001231000000:2800:BF01EFD73A4149EF27DF7327FABEDE97A7CDAC19F0A8B621A1A7E4A3C60AEF74.png)

## 单元测试框架发布方式

单元测试框架以ohpm包独立发布，版本信息详见[服务组件官网](https://ohpm.openharmony.cn/#/cn/detail/@ohos%2Fhypium)。开发者下载DevEco Studio后，在应用工程中的[oh-package.json5](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-oh-package-json5)文件中devDependencies节点中配置版本号即可使用对应版本框架功能。

**配置示例**

1. "devDependencies": {
2.     "@ohos/hypium": "1.0.24"
3.   }

## 基于ArkTS编写和执行测试脚本

### 搭建环境

测试脚本基于DevEco Studio编写，请下载[DevEco Studio](https://developer.huawei.com/consumer/cn/download/)并完成[hdc配置](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/hdc#%E7%8E%AF%E5%A2%83%E5%87%86%E5%A4%87)。

### 新建测试脚本

参考[DevEco Studio指导](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-instrument-test#section36049271219)创建ArkTS测试用例。

### 编写单元测试脚本

一个完整的测试脚本需要包含以下基本元素：

1. 依赖导包，以便使用单元测试框架提供的接口，以及其他测试脚本中需要依赖使用的接口。
2. 测试代码编写，编写测试用例的相关测试逻辑。
3. 断言接口调用，设置测试代码中的检查点，用于检查用例是否符合预期。

下面提供一个简单示例，测试场景：启动被测试页面，检查设备当前显示的页面是否为预期启动的页面。

1. import { describe, it, expect, Level, Size, TestType } from '@ohos/hypium';
2. import { abilityDelegatorRegistry } from '@kit.TestKit';
3. import { UIAbility, Want } from '@kit.AbilityKit';

4. const delegator = abilityDelegatorRegistry.getAbilityDelegator();
5. function sleep(time: number) {
6.   return new Promise<void>((resolve: Function) => setTimeout(resolve, time));
7. }
8. export default function abilityTest() {
9.   describe('ActsAbilityTest', () =>{
10.   // 测试套名称为ActsAbilityTest
11.     // 可根据此处设置的用例类型、用例规模、用例级别进行用例筛选
12.     it('testExample',TestType.FUNCTION | Size.MEDIUMTEST | Level.LEVEL1, async (done: Function) => {
13.     // 测试用例名称为testExample
14.       console.info("unitTest: TestExample begin");
15.       await sleep(500);
16.       const bundleName = abilityDelegatorRegistry.getArguments().bundleName;
17.       // 启动被测试Ability
18.       const want: Want = {
19.         bundleName: bundleName,
20.         abilityName: 'EntryAbility'
21.       }
22.       await delegator.startAbility(want);
23.       await sleep(500);
24.       // 获取设备上前台显示的页面并断言检查
25.       const ability: UIAbility = await delegator.getCurrentTopAbility();
26.       console.info("get top ability");
27.       expect(ability.context.abilityInfo.name).assertEqual('EntryAbility');
28.       done();
29.     })
30.   })
31. }

### DevEco Studio执行测试脚本

连接目标测试设备（如手机），在DevEco Studio页面点击对应按钮执行测试脚本，当前支持以下四种方式：

1. 测试包级别执行，即执行测试包内的全部用例。
2. 测试类级别执行，即执行*.ets文件里的所有测试用例。
3. 测试套级别执行，即执行describe接口中定义的全部测试用例。
4. 测试用例级别执行，即执行指定it接口也就是单条测试用例。

下面给出测试类级别即测试文件执行示例，其他请查考[运行模式](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-instrument-test#section1574003717165)。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251215154028.59325654367998691924803057351590:50001231000000:2800:EEAFB64C0EF7A8872920B02E93820E3468F3689B043E71C0A6FBF5955E0BCF5C.png)

- 查看测试结果

测试执行后可直接在DevEco Studio中查看测试结果。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251215154028.49363914226522662024878809588169:50001231000000:2800:7D88D15E69D6A0F8EC160BF4554623F802CF6B0B13593E0BD8971FF7110BC5E1.png)

- 查看测试用例覆盖率

执行测试用例后可以查看测试用例覆盖率，具体操作请参考[覆盖率统计模式](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-instrument-test#section1989615417457)章节内的内容。

### 命令行执行测试脚本

脚本执行需连接硬件设备，开发者安装测试包到连接设备上，在命令行窗口中通过执行aa test命令并设置执行参数，触发执行测试用例。

- aa test工具命令列表

以下是单元测试过程中的常用命令，其他aa test命令及含义说明参考[命令指南说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/aa-tool)。

|参数|参数说明|示例|
|:--|:--|:--|
|--bundleName/-b|指定应用Bundle名称。|- b com.test.example|
|--packageName/-p|指定应用模块名，适用于FA模型应用。|- p com.test.example.entry|
|--moduleName/-m|指定应用模块名，适用于Stage模型应用。|-m entry|
|-s|特定参数，以<key, value>键值对方式传入。框架支持通过-s参数键值配置多种用例执行方式，-s的参数及对应含义参见下表。|- s unittest /ets/testrunner/OpenHarmonyTestRunner|

|参数|参数含义及取值|示例|
|:--|:--|:--|
|unittest|用例执行所使用OpenHarmonyTestRunner对象，取值可为OpenHarmonyTestRunner或用户自定义runner名称。|-s unittest OpenHarmonyTestRunner|
|class|筛选执行方式，即指定要执行的测试套或测试用例。取值为describeName，describeName#itName，其中describeName为测试套名称、itName为测试用例名称。|-s class attributeTest#testAttributeIt|
|notClass|排除执行方式，即指定不需要执行的测试套或测试用例。取值为describeName，describeName#itName，其中describeName为测试套名称、itName为测试用例名称。|-s notClass attributeTest#testAttributeIt|
|itName|筛选执行方式， 指定要执行的测试用例。取值为itName。|-s itName testAttributeIt|
|timeout|设置测试用例执行的超时时间。取值为正整数（单位ms），默认值：5000。|-s timeout 15000|
|breakOnError|遇错即停方式，设置是否在用例失败时立即停止测试。取值为true（停止）/false（继续），默认为false。<br><br>**说明**：从@ohos/hypium 1.0.6版本开始支持。|-s breakOnError true|
|random|随机执行方式，设置为true时随机顺序执行测试用例。取值为true（设置）/false（不设置），默认为false。<br><br>**说明**：从@ohos/hypium 1.0.3版本开始支持。|-s random true|
|testType|筛选执行方式，指定筛选执行的用例类型。取值为function，performance，power，reliability，security，global，compatibility，user，standard，safety，resilience。|-s testType function|
|level|筛选执行方式，指定筛选执行的用例级别。取值为0，1，2，3，4。|-s level 0|
|size|筛选执行方式，指定筛选执行的用例规模。取值为small，medium，large。|-s size small|
|stress|压力执行方式，指定执行用例的执行次数，设置后框架按照设置次数重复执行。取值为正整数。<br><br>**说明**：从@ohos/hypium 1.0.5版本开始支持。|-s stress 1000|
|skipMessage|控制显示待执行的测试用例信息全集中，是否包含被设置跳过执行的测试套和用例的信息。取值为true（不显示相关信息）/false（显示相关信息），默认为false。<br><br>**说明**：从@ohos/hypium 1.0.17版本开始支持。|-s skipMessage true|
|runSkipped|跳过执行方式，指定要执行的跳过测试套&跳过用例。取值为all，skipped，describeName#itName。<br><br>**说明**：从@ohos/hypium 1.0.17版本开始支持。|-s runSkipped all|

- 执行测试脚本

说明

下文参数配置和命令示例均基于Stage模型。

执行命令参数需基于@ohos/hypium框架发布版本，且测试应用包需集成该版本，否则命令参数无法响应，具体配置方式参考[发布方式](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/unittest-guidelines#%E5%8D%95%E5%85%83%E6%B5%8B%E8%AF%95%E6%A1%86%E6%9E%B6%E5%8F%91%E5%B8%83%E6%96%B9%E5%BC%8F)。

**示例代码1**：执行所有测试用例

1.  hdc shell aa test -b xxx -m xxx -s unittest OpenHarmonyTestRunner

**示例代码2**：执行指定的describe测试套用例，指定多个需用逗号隔开

1.   hdc shell aa test -b xxx -m xxx -s unittest OpenHarmonyTestRunner -s class s1,s2

**示例代码3**：执行指定测试套中指定的用例，指定多个需用逗号隔开

1.   hdc shell aa test -b xxx -m xxx -s unittest OpenHarmonyTestRunner -s class testStop#stop_1,testStop1#stop_0

**示例代码4**：执行除指定配置外的所有用例，设置不执行多个测试套需用逗号隔开

1.   hdc shell aa test -b xxx -m xxx -s unittest OpenHarmonyTestRunner -s notClass testStop

**示例代码5**：执行指定it名称的所有用例，指定多个需用逗号隔开

1.   hdc shell aa test -b xxx -m xxx -s unittest OpenHarmonyTestRunner -s itName stop_0

**示例代码6**：用例执行超时时长配置

1.   hdc shell aa test -b xxx -m xxx -s unittest OpenHarmonyTestRunner -s timeout 15000

**示例代码7**：用例以遇错即停模式执行用例

1.   hdc shell aa test -b xxx -m xxx -s unittest OpenHarmonyTestRunner -s breakOnError true

**示例代码8**：执行测试类型匹配的测试用例

1.   hdc shell aa test -b xxx -m xxx -s unittest OpenHarmonyTestRunner -s testType function

**示例代码9**：执行测试级别匹配的测试用例

1.   hdc shell aa test -b xxx -m xxx -s unittest OpenHarmonyTestRunner -s level 0

**示例代码10**：执行测试规模匹配的测试用例

1.   hdc shell aa test -b xxx -m xxx -s unittest OpenHarmonyTestRunner -s size small

**示例代码11**：执行测试用例指定次数

1.   hdc shell aa test -b xxx -m xxx -s unittest OpenHarmonyTestRunner -s stress 1000

- 查看测试结果

1. 在命令行模式执行过程中，框架会打印如下日志信息。
    
    1. OHOS_REPORT_STATUS: class=ActsAbilityTest
    2. OHOS_REPORT_STATUS: current=1
    3. OHOS_REPORT_STATUS: id=JS
    4. OHOS_REPORT_STATUS: numtests=447
    5. OHOS_REPORT_STATUS: stream=
    6. OHOS_REPORT_STATUS: test=testExample
    7. OHOS_REPORT_STATUS_CODE: 1
    
    8. OHOS_REPORT_STATUS: class=ActsAbilityTest
    9. OHOS_REPORT_STATUS: current=1
    10. OHOS_REPORT_STATUS: id=JS
    11. OHOS_REPORT_STATUS: numtests=447
    12. OHOS_REPORT_STATUS: stream=
    13. OHOS_REPORT_STATUS: test=testExample
    14. OHOS_REPORT_STATUS_CODE: 0
    15. OHOS_REPORT_STATUS: consuming=4
    
    |日志输出字段|日志输出字段含义|
    |:--|:--|
    |OHOS_REPORT_SUM|当前执行的测试套中用例总数。|
    |OHOS_REPORT_STATUS: class|当前执行用例所属测试套名称。|
    |OHOS_REPORT_STATUS: id|当前用例执行语言，默认JS。|
    |OHOS_REPORT_STATUS: numtests|当前测试包中测试用例总数。|
    |OHOS_REPORT_STATUS: stream|当前用例发生错误时，记录错误信息。|
    |OHOS_REPORT_STATUS: test|当前用例执行的it name。|
    |OHOS_REPORT_STATUS_CODE|当前用例执行状态。1表示用例开始执行，0表示用例执行通过，-1表示用例执行报错，-2表示用例执行失败。|
    |OHOS_REPORT_STATUS: consuming|当前用例执行消耗的时长（ms）。|
    
2. 命令行执行完成后，框架会打印如下相关日志信息。
    
    1. OHOS_REPORT_RESULT: stream=Tests run: 447, Failure: 0, Error: 1, Pass: 201, Ignore: 245
    2. OHOS_REPORT_CODE: 0
    
    3. OHOS_REPORT_RESULT: breakOnError model, Stopping whole test suite if one specific test case failed or error
    4. OHOS_REPORT_STATUS: taskconsuming=16029
    
    |日志输出字段|日志输出字段含义|
    |:--|:--|
    |run|当前测试包用例总数。|
    |Failure|当前测试失败用例数量。|
    |Error|当前执行用例发生错误用例数量。|
    |Pass|当前执行用例通过用例数量。|
    |Ignore|当前未执行用例数量。|
    |taskconsuming|执行当前测试用例总耗时（ms）。|
    
    说明
    
    当按照遇错即停方式执行时，用例发生错误时，注意查看Ignore字段以及错误中断时的提示信息。
    

## 单元测试框架能力使用说明

### 基础流程能力

单元测试框架提供执行测试脚本所需的基础流程接口，开发者需要实现相关接口，框架侧在运行时通过基础流程接口识别测试用例，调度执行并汇总测试结果。当前支持的基础流程接口如下表所示：

|接口名|功能说明|
|:--|:--|
|describe|定义一个测试套，测试套中可以定义多个测试用例函数，但不支持异步函数。|
|it|定义一条测试用例。|
|beforeAll|在测试套内定义一个预置条件，在所有测试用例开始前执行且仅执行一次。|
|beforeEach|在测试套内定义一个预置条件，在每条测试用例开始前执行，执行次数与it定义的测试用例数一致。|
|afterEach|在测试套内定义一个单元清理条件，在每条测试用例结束后执行，执行次数与it定义的测试用例数一致。|
|afterAll|在测试套内定义一个清理条件，在所有测试用例结束后执行且仅执行一次。|
|beforeItSpecified|在测试套内定义一个单元预置条件，仅在指定测试用例开始前执行。<br><br>**说明**：从@ohos/hypium 1.0.15版本开始支持。|
|afterItSpecified|在测试套内定义一个单元清理条件，仅在指定测试用例结束后执行。<br><br>**说明**：从@ohos/hypium 1.0.15版本开始支持。|
|expect|支持bool类型判断等多种断言能力。|
|xdescribe|定义一个跳过的测试套，测试套中可以定义多个测试用例函数，但不支持异步函数。<br><br>**说明**：从@ohos/hypium 1.0.17版本开始支持。|
|xit|定义一条跳过的测试用例。<br><br>**说明**：从@ohos/hypium 1.0.17版本开始支持。|

**示例代码1**：beforeAll/beforeEach/afterEach/afterAll使用示例

1. import { describe, beforeAll, beforeEach, afterEach, afterAll, it, expect, Level } from '@ohos/hypium';

2. export default function exampleTest() {

3.   describe('ExampleTest', () =>{
4.     let testNumA : number = 1;
5.     let testNumB : number = 1;

6.     beforeAll(() => {
7.       testNumA++;
8.     })

9.     beforeEach(() => {
10.       testNumA++;
11.       testNumB++;
12.     })

13.     afterEach(() => {
14.       testNumA++;
15.     })

16.     afterAll(() => {
17.       expect(testNumA).assertEqual(5);
18.     })

19.     it('testExampleA',Level.LEVEL1, async (done: Function) => {
20.       console.info("unitTest: testExampleA begin");
21.       expect(testNumA).assertEqual(3);
22.       expect(testNumB).assertEqual(2);
23.       done();
24.     })

25.     it('testExampleB',Level.LEVEL1, async (done: Function) => {
26.       console.info("unitTest: testExampleB begin");
27.       expect(testNumA).assertEqual(5);
28.       expect(testNumB).assertEqual(3);
29.       done();
30.     })
31.   })
32. }

**示例代码2**：beforeItSpecified/afterItSpecified使用示例，从1.0.15版本开始支持

1. import { describe, beforeItSpecified, afterItSpecified, it, expect, Level } from '@ohos/hypium';

2. export default function exampleTest() {

3.   describe('ExampleTest', () =>{
4.    let testNumA : number = 1;
5.    let testNumB : number = 1;

6.    beforeItSpecified(['testExampleB'], () => {
7.       testNumB++;
8.     })
9.    afterItSpecified(['testExampleA'], () => {
10.       testNumA++;
11.     })

12.     it('testExampleA',Level.LEVEL1, async (done: Function) => {
13.       console.info("unitTest: testExampleA begin");
14.       expect(testNumA).assertEqual(1);
15.       expect(testNumB).assertEqual(1);
16.       done();
17.     })

18.     it('testExampleB',Level.LEVEL1, async (done: Function) => {
19.       console.info("unitTest: testExampleB begin");
20.       expect(testNumA).assertEqual(2);
21.       expect(testNumB).assertEqual(2);
22.       done();
23.     })
24.   })
25. }

**示例代码3**：xit使用示例，从1.0.17版本开始支持

1. import { describe, xit, it, Level } from '@ohos/hypium';

2. export default function describeExampleTest() {

3.   describe('ExampleTest', () =>{
4.     xit('testExampleA',Level.LEVEL1, async (done: Function) => {
5.       console.info("unitTest: testExampleA begin");
6.       done();
7.     })

8.     it('testExampleB',Level.LEVEL1, async (done: Function) => {
9.       console.info("unitTest: testExampleB begin");
10.       done();
11.     })
12.   })
13. }

### 断言能力

单元测试框架提供了丰富的断言接口，供开发者在不同测试场景下使用，详细接口可查看下表。

|接口名|功能说明|
|:--|:--|
|assertClose|检验实际值和预期值之间的数值差异是否在指定的允许误差范围内。|
|assertContain|检验实际值中是否包含预期值。|
|assertEqual|检验实际值是否等于预期值。|
|assertFail|抛出一个错误。|
|assertFalse|检验实际值是否是false。|
|assertTrue|检验实际值是否是true。|
|assertInstanceOf|检验实际值是否是预期类型，支持基础类型。|
|assertLarger|检验实际值是否大于预期值。|
|assertLargerOrEqual|检验实际值是否大于或等于预期值。|
|assertLess|检验实际值是否小于预期值。|
|assertLessOrEqual|检验实际值是否小于或等于预期值。|
|assertNull|检验实际值是否是null。|
|assertThrowError|检验实际值抛出Error内容是否为预期的异常类型。|
|assertUndefined|检验实际值是否是undefined。|
|assertNaN|检验实际值是否是NaN。<br><br>**说明**：从@ohos/hypium 1.0.4版本开始支持。|
|assertNegUnlimited|检验实际值是否等于Number.NEGATIVE_INFINITY。<br><br>**说明**：从@ohos/hypium 1.0.4版本开始支持。|
|assertPosUnlimited|检验实际值是否等于Number.POSITIVE_INFINITY。<br><br>**说明**：从@ohos/hypium 1.0.4版本开始支持。|
|assertDeepEquals|检验实际值和预期值是否完全相等。<br><br>**说明**：从@ohos/hypium 1.0.4版本开始支持。|
|assertPromiseIsPending|检验Promise是否处于Pending状态。<br><br>**说明**：从@ohos/hypium 1.0.4版本开始支持。|
|assertPromiseIsRejected|检验Promise是否处于Rejected状态。<br><br>**说明**：从@ohos/hypium 1.0.4版本开始支持。|
|assertPromiseIsRejectedWith|检验Promise是否处于Rejected状态，并且比较执行的结果值。<br><br>**说明**：从@ohos/hypium 1.0.4版本开始支持。|
|assertPromiseIsRejectedWithError|检验Promise是否处于Rejected状态并包含异常，比较异常类型和异常信息。<br><br>**说明**：从@ohos/hypium 1.0.4版本开始支持。|
|assertPromiseIsResolved|检验Promise是否处于Resolved状态。<br><br>**说明**：从@ohos/hypium 1.0.4版本开始支持。|
|assertPromiseIsResolvedWith|检验Promise是否处于Resolved状态并比较结果值。<br><br>**说明**：从@ohos/hypium 1.0.4版本开始支持。|
|not|断言取反，支持上述所有断言功能。<br><br>**说明**：从@ohos/hypium 1.0.4版本开始支持。|

**示例代码**：

1. import { describe, it, expect, Level } from '@ohos/hypium';

2. export default function exampleTest() {
3.   describe('ExampleTest', () =>{
4.     it('assertCloseTest', Level.LEVEL1, () => {
5.       let a: number = 100;
6.       let b: number = 0.1;
7.       expect(a).assertClose(99, b);
8.     })

9.     it('assertContain_1', Level.LEVEL1, () => {
10.       let a = "abc";
11.       expect(a).assertContain('b');
12.     })

13.     it('assertContain_2', Level.LEVEL1, () => {
14.       let a = [1, 2, 3];
15.       expect(a).assertContain(1);
16.     })

17.     it('assertEqualTest', Level.LEVEL1, () => {
18.       expect(3).assertEqual(3);
19.     })

20.     it('assertFailTest', Level.LEVEL1, () => {
21.       expect().assertFail(); // 用例失败
22.     })

23.     it('assertFalseTest', Level.LEVEL1, () => {
24.       expect(false).assertFalse();
25.     })

26.     it('assertTrueTest', Level.LEVEL1, () => {
27.       expect(true).assertTrue();
28.     })

29.     it('assertInstanceOfTest', Level.LEVEL1, () => {
30.       let a: string = 'strTest';
31.       expect(a).assertInstanceOf('String');
32.     })

33.     it('assertLargerTest', Level.LEVEL1, () => {
34.       expect(3).assertLarger(2);
35.     })

36.     it('assertLessTest', Level.LEVEL1, () => {
37.       expect(2).assertLess(3);
38.     })

39.     it('assertNullTest', Level.LEVEL1, () => {
40.       expect(null).assertNull();
41.     })

42.     it('assertThrowErrorTest', Level.LEVEL1, () => {
43.       expect(() => {
44.         throw new Error('test');
45.       }).assertThrowError('test');
46.     })

47.     it('assertUndefinedTest', Level.LEVEL1, () => {
48.       expect(undefined).assertUndefined();
49.     })

50.     it('assertLargerOrEqualTest', Level.LEVEL1, () => {
51.       expect(3).assertLargerOrEqual(3);
52.     })

53.     it('assertLessOrEqualTest', Level.LEVEL1, () => {
54.       expect(3).assertLessOrEqual(3);
55.     })

56.     it('assertNaNTest', Level.LEVEL1, () => {
57.       expect(Number.NaN).assertNaN(); // true
58.     })

59.     it('assertNegUnlimitedTest', Level.LEVEL1, () => {
60.       expect(Number.NEGATIVE_INFINITY).assertNegUnlimited(); // true
61.     })

62.     it('assertPosUnlimitedTest', Level.LEVEL1, () => {
63.       expect(Number.POSITIVE_INFINITY).assertPosUnlimited(); // true
64.     })

65.     it('deepEquals_null_true', Level.LEVEL1, () => {
66.       expect(null).assertDeepEquals(null);
67.     })

68.     it('deepEquals_array_not_have_true', Level.LEVEL1, () => {
69.       const a: Array<number> = [];
70.       const b: Array<number> = [];
71.       expect(a).assertDeepEquals(b);
72.     })

73.     it('deepEquals_map_equal_length_success', Level.LEVEL1, () => {
74.       const a: Map<number, number> = new Map();
75.       const b: Map<number, number> = new Map();
76.       a.set(1, 100);
77.       a.set(2, 200);
78.       b.set(1, 100);
79.       b.set(2, 200);
80.       expect(a).assertDeepEquals(b);
81.     })

82.     it("deepEquals_obj_success_1", Level.LEVEL1, () => {
83.       const a: SampleTest = {x: 1};
84.       const b: SampleTest = {x: 1};
85.       expect(a).assertDeepEquals(b);
86.     })

87.     it("deepEquals_regExp_success_0", Level.LEVEL1, () => {
88.       const a: RegExp = new RegExp("/test/");
89.       const b: RegExp = new RegExp("/test/");
90.       expect(a).assertDeepEquals(b);
91.     })

92.     it('assertPromiseIsPendingTest', Level.LEVEL1, async () => {
93.       let p: Promise<void> = new Promise<void>(() => {});
94.       await expect(p).assertPromiseIsPending();
95.     })

96.     it('assertPromiseIsRejectedTest', Level.LEVEL1, async () => {
97.       let info: PromiseInfo = {res: "no"};
98.       let p: Promise<PromiseInfo> = Promise.reject(info);
99.       await expect(p).assertPromiseIsRejected();
100.     })

101.     it('assertPromiseIsRejectedWithTest', Level.LEVEL1, async () => {
102.       let info: PromiseInfo = {res: "reject value"};
103.       let p: Promise<PromiseInfo> = Promise.reject(info);
104.       await expect(p).assertPromiseIsRejectedWith(info);
105.     })

106.     it('assertPromiseIsRejectedWithErrorTest', Level.LEVEL1, async () => {
107.       let p1: Promise<TypeError> = Promise.reject(new TypeError('number'));
108.       await expect(p1).assertPromiseIsRejectedWithError(TypeError);
109.     })

110.     it('assertPromiseIsResolvedTest', Level.LEVEL1, async () => {
111.       let info: PromiseInfo = {res: "result value"};
112.       let p: Promise<PromiseInfo> = Promise.resolve(info);
113.       await expect(p).assertPromiseIsResolved();
114.     })

115.     it('assertPromiseIsResolvedWithTest', Level.LEVEL1, async () => {
116.       let info: PromiseInfo = {res: "result value"};
117.       let p: Promise<PromiseInfo> = Promise.resolve(info);
118.       await expect(p).assertPromiseIsResolvedWith(info);
119.     })

120.     it("test_message", Level.LEVEL1, () => {
121.       expect(1).message('1 is not equal 2!').assertEqual(2); // fail
122.     })
123.   })
124. }

125. interface SampleTest {
126.   x: number;
127. }

128. interface PromiseInfo {
129.   res: string;
130. }

### Mock能力

从@ohos/hypium 1.0.1版本开始，单元测试框架支持Mock能力。配置方式参考上文[发布方式](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/unittest-guidelines#%E5%8D%95%E5%85%83%E6%B5%8B%E8%AF%95%E6%A1%86%E6%9E%B6%E5%8F%91%E5%B8%83%E6%96%B9%E5%BC%8F)。

说明

仅支持Mock应用工程中自定义对象，不支持Mock系统API对象。如需Mock系统API，请参考[系统模块Mock指南](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-test-mock#section8353132513310)。

不支持Mock对象的私有函数。

**基础类**

MockKit是Mock的基础类，用于指定需要Mock的实例和函数。

|接口名|功能说明|
|:--|:--|
|mockFunc|Mock某个类实例中的函数，支持使用异步函数。|
|verify|验证函数在对应参数下的执行行为是否符合预期，返回一个VerificationMode类。|
|ignoreMock|使用ignoreMock可以还原实例中被Mock后的函数，对被Mock后的函数有效。|
|clear|用例执行完毕后，对被Mock对象实例进行还原处理（还原之后对象恢复被Mock之前的功能）。|
|clearAll|用例执行完毕后，进行数据和内存清理，不会还原实例中被Mock后的函数。|

**VerificationMode**

VerificationMode用于验证被Mock函数的被调用次数，需同verify函数结合使用。

|接口名|功能说明|
|:--|:--|
|times|验证函数被调用过的次数符合预期。|
|once|验证函数被调用过一次。|
|atLeast|验证函数最少被调用的次数符合预期。|
|atMost|验证函数最多被调用的次数符合预期。|
|never|验证函数从未被调用过。|

**when**

when是一个函数，用于设置函数期望被Mock的值。

|接口名|功能说明|
|:--|:--|
|when|对传入后函数做检查，检查是否被Mock并标记过，返回一个内置函数，函数执行后返回一个类用于设置Mock值。|

使用when函数之后，需使用如下函数设置函数被Mock后的返回值。

|接口名|功能说明|
|:--|:--|
|afterReturn|设定一个自定义的期望返回值，比如某个字符串或者一个Promise。|
|afterReturnNothing|设定预期没有返回值，即undefined。|
|afterAction|设定预期返回一个函数执行的操作。|
|afterThrow|设定预期抛出异常，并指定异常描述信息。|

**ArgumentMatchers相关接口**

ArgumentMatchers用于用户自定义函数参数，当开发者想基于某类规则设定预期返回值时，可以使用。它以枚举值或函数的形式提供给开发者使用。

|枚举名|功能说明|
|:--|:--|
|any|设定用户传任何类型参数（undefined和null除外），执行的结果返回所设置的预期值，使用ArgumentMatchers.any方式调用。|
|anyString|设定用户传任何字符串参数，执行的结果都是预期的值，使用ArgumentMatchers.anyString方式调用。|
|anyBoolean|设定用户传任何boolean类型参数，执行的结果都是预期的值，使用ArgumentMatchers.anyBoolean方式调用。|
|anyFunction|设定用户传任何function类型参数，执行的结果都是预期的值，使用ArgumentMatchers.anyFunction方式调用。|
|anyNumber|设定用户传任何数字类型参数，执行的结果都是预期的值，使用ArgumentMatchers.anyNumber方式调用。|
|anyObj|设定用户传任何对象类型参数，执行的结果都是预期的值，使用ArgumentMatchers.anyObj方式调用。|

|接口名|功能说明|
|:--|:--|
|matchRegexs|设定用户传任何符合正则表达式验证的参数，执行的结果都是预期的值，使用ArgumentMatchers.matchRegexs(Regex)方式调用。|

说明

使用Mock能力时必须导入Mock能力模块： MockKit，when，开发者可根据实际需求导入对应模块。

例如：import { describe, expect, it, MockKit, when} from '@ohos/hypium'

**示例代码1**：使用afterReturn/afterReturnNothing设置预期返回值

1. import { describe, expect, it, MockKit, when } from '@ohos/hypium';

2. class ClassName {
3.   constructor() {
4.   }

5.   method_1(arg: string) {
6.     return '888888';
7.   }

8.   method_2(arg: string) {
9.     return '999999';
10.   }
11. }
12. export default function afterReturnTest() {
13.   describe('afterReturnTest', () => {
14.     it('afterReturnTest', 0, () => {
15.       console.info("it1 begin");
16.       // 创建一个Mock能力的对象MockKit
17.       let mocker: MockKit = new MockKit();
18.       // 初始化ClassName的对象claser，作为被Mock的对象实例
19.       let claser: ClassName = new ClassName();
20.       // 进行Mock操作，对ClassName类的method_1函数进行Mock
21.       let mockfunc: Function = mocker.mockFunc(claser, claser.method_1);
22.       // 期望claser.method_1函数被Mock后, 以'testA'为入参时调用函数返回结果'1',以'testB''为入参时调用函数返回结果undefined
23.       when(mockfunc)('testA').afterReturn('1');
24.       when(mockfunc)('testB').afterReturnNothing();
25.       // 对Mock后的函数进行断言，看是否符合预期。分别传入参数'testA'和'testB'时，应该返回自定义的预期结果1和undefined
26.       expect(claser.method_1('testA')).assertEqual('1'); // 断言执行通过
27.       expect(claser.method_1('testB')).assertUndefined(); // 断言执行通过
28.     })
29.   })
30. }

**示例代码2**：使用ArgumentMatchers设定参数类型为any即接受任何参数（undefined和null除外）

1. import { describe, expect, it, MockKit, when, ArgumentMatchers } from '@ohos/hypium';

2. class ClassName {
3.   constructor() {
4.   }

5.   method_1(arg: string) {
6.     return '888888';
7.   }

8.   method_2(arg: string) {
9.     return '999999';
10.   }
11. }
12. export default function argumentMatchersAnyTest() {
13.   describe('argumentMatchersAnyTest', () => {
14.     it('testMockfunc', 0, () => {
15.       console.info("it1 begin");
16.       // 创建一个Mock能力的对象MockKit
17.       let mocker: MockKit = new MockKit();
18.       // 初始化ClassName的对象claser
19.       let claser: ClassName = new ClassName();
20.       // 进行Mock操作，对ClassName类的method_1函数进行Mock
21.       let mockfunc: Function = mocker.mockFunc(claser, claser.method_1);
22.       // 期望claser.method_1函数被Mock后, 参数为任一类型在被调用时均返回结果'1'
23.       when(mockfunc)(ArgumentMatchers.any).afterReturn('1');
24.       // 传入不同参数验证是否符合预期
25.       expect(claser.method_1('test')).assertEqual('1'); // 断言执行通过
26.       expect(claser.method_1("123")).assertEqual('1');// 断言执行通过
27.       expect(claser.method_1("true")).assertEqual('1');// 断言执行通过
28.     })
29.   })
30. }

**示例代码3**：使用ArgumentMatchers设定参数类型为String

1. import { describe, expect, it, MockKit, when, ArgumentMatchers } from '@ohos/hypium';

2. class ClassName {
3.   constructor() {
4.   }

5.   method_1(arg: string) {
6.     return '888888';
7.   }

8.   method_2(arg: string) {
9.     return '999999';
10.   }
11. }
12. export default function argumentMatchersTest() {
13.   describe('argumentMatchersTest', () => {
14.     it('testMockfunc', 0, () => {
15.       console.info("it1 begin");
16.       // 创建一个Mock能力的对象MockKit
17.       let mocker: MockKit = new MockKit();
18.       // 初始化ClassName的对象claser
19.       let claser: ClassName = new ClassName();
20.       // 进行Mock操作,对ClassName类的method_1函数进行Mock
21.       let mockfunc: Function = mocker.mockFunc(claser, claser.method_1);
22.       // 期望claser.method_1函数被Mock后, 以任何string类型为参数调用函数时返回结果'1'
23.       when(mockfunc)(ArgumentMatchers.anyString).afterReturn('1');
24.       // 传入不同string类型参数，验证是否符合预期
25.       expect(claser.method_1('test')).assertEqual('1'); // 断言执行通过
26.       expect(claser.method_1('abc')).assertEqual('1'); // 断言执行通过
27.     })
28.   })
29. }

**示例代码4**：使用ArgumentMatchers设定参数类型为matchRegexs（Regex）即正则表达式

1. import { describe, expect, it, MockKit, when, ArgumentMatchers } from '@ohos/hypium';

2. class ClassName {
3.   constructor() {
4.   }

5.   method_1(arg: string) {
6.     return '888888';
7.   }

8.   method_2(arg: string) {
9.     return '999999';
10.   }
11. }
12. export default function matchRegexsTest() {
13.   describe('matchRegexsTest', () => {
14.     it('testMockfunc', 0, () => {
15.       console.info("it1 begin");
16.       // 创建一个Mock能力的对象MockKit
17.       let mocker: MockKit = new MockKit();
18.       // 初始化ClassName的对象claser
19.       let claser: ClassName = new ClassName();
20.       // 进行Mock操作，对ClassName类的method_1函数进行Mock
21.       let mockfunc: Function = mocker.mockFunc(claser, claser.method_1);
22.       // 期望claser.method_1函数被Mock后, 以"test"为入参调用函数时返回结果'1'
23.       when(mockfunc)(ArgumentMatchers.matchRegexs(new RegExp("test"))).afterReturn('1');
24.       // 传入test参数后验证是否符合预期
25.       expect(claser.method_1('test')).assertEqual('1'); // 断言执行通过
26.     })
27.   })
28. }

**示例代码5**：使用verify函数验证被Mock函数在对应参数下的执行行为是否符合预期

1. import { describe, it, MockKit } from '@ohos/hypium';

2. class ClassName {
3.   constructor() {
4.   }

5.   method_1(...arg: string[]) {
6.     return '888888';
7.   }

8.   method_2(...arg: string[]) {
9.     return '999999';
10.   }
11. }
12. export default function verifyTest() {
13.   describe('verifyTest', () => {
14.     it('testMockfunc', 0, () => {
15.       console.info("it1 begin");
16.       // 创建一个Mock能力的对象MockKit
17.       let mocker: MockKit = new MockKit();
18.       // 初始化ClassName的对象claser
19.       let claser: ClassName = new ClassName();
20.       // 进行Mock操作，对ClassName类的method_1和method_2两个函数进行Mock
21.       mocker.mockFunc(claser, claser.method_1);
22.       mocker.mockFunc(claser, claser.method_2);
23.       // 函数调用
24.       claser.method_1('abc', 'ppp');
25.       claser.method_1('abc');
26.       claser.method_1('xyz');
27.       claser.method_1();
28.       claser.method_1('abc', 'xxx', 'yyy');
29.       claser.method_1();
30.       claser.method_2('111');
31.       claser.method_2('111', '222');
32.       // 对Mock后的两个函数进行验证，验证method_2,参数仅为'111'时执行过一次
33.       mocker.verify('method_2',['111']).once(); // 断言执行通过
34.     })
35.   })
36. }

**示例代码6**：使用ignoreMock函数还原指定被Mock函数实现

1. import { describe, expect, it, MockKit, when, ArgumentMatchers } from '@ohos/hypium';

2. class ClassName {
3.   constructor() {
4.   }

5.   method_1(...arg: number[]) {
6.     return '888888';
7.   }

8.   method_2(...arg: number[]) {
9.     return '999999';
10.   }
11. }
12. export default function ignoreMockTest() {
13.   describe('ignoreMockTest', () => {
14.     it('testMockfunc', 0, () => {
15.       console.info("it1 begin");
16.       // 创建一个Mock能力的对象MockKit
17.       let mocker: MockKit = new MockKit();
18.       // 初始化ClassName的对象claser
19.       let claser: ClassName = new ClassName();
20.       // 进行Mock操作，对ClassName类的method_1和method_2两个函数进行Mock
21.       let func_1: Function = mocker.mockFunc(claser, claser.method_1);
22.       let func_2: Function = mocker.mockFunc(claser, claser.method_2);
23.       // 期望claser.method_1函数被Mock后, 以number类型为入参时调用函数返回结果'4'
24.       when(func_1)(ArgumentMatchers.anyNumber).afterReturn('4');
25.       // 期望claser.method_2函数被Mock后, 以number类型为入参时调用函数返回结果'5'
26.       when(func_2)(ArgumentMatchers.anyNumber).afterReturn('5');
27.       // 函数调用
28.       expect(claser.method_1(123)).assertEqual("4");
29.       expect(claser.method_2(456)).assertEqual("5");
30.       // 现在对Mock后的两个函数的其中一个函数method_1进行还原处理
31.       mocker.ignoreMock(claser, claser.method_1);
32.       // 调用claser.method_1函数
33.       expect(claser.method_1(123)).assertEqual('888888');// 断言执行通过
34.     })
35.   })
36. }

**示例代码7**：使用clear函数还原类中所有被Mock函数原有实现

1. import { describe, expect, it, MockKit, when, ArgumentMatchers } from '@ohos/hypium';

2. class ClassName {
3.   constructor() {
4.   }

5.   method_1(...arg: number[]) {
6.     return '888888';
7.   }

8.   method_2(...arg: number[]) {
9.     return '999999';
10.   }
11. }
12. export default function clearTest() {
13.   describe('clearTest', () => {
14.     it('testMockfunc', 0, () => {
15.       console.info("it1 begin");
16.       // 创建一个Mock能力的对象MockKit
17.       let mocker: MockKit = new MockKit();
18.       // 初始化ClassName的对象claser
19.       let claser: ClassName = new ClassName();
20.       // 进行Mock操作，对ClassName类的method_1和method_2两个函数进行Mock
21.       let func_1: Function = mocker.mockFunc(claser, claser.method_1);
22.       let func_2: Function = mocker.mockFunc(claser, claser.method_2);
23.       // 期望claser.method_1函数被Mock后, 以任何number类型为参数调用函数时返回结果'4'
24.       when(func_1)(ArgumentMatchers.anyNumber).afterReturn('4');
25.       // 期望claser.method_2函数被Mock后, 以任何number类型为参数调用函数时返回结果'5'
26.       when(func_2)(ArgumentMatchers.anyNumber).afterReturn('5');
27.       // 函数调用
28.       expect(claser.method_1(123)).assertEqual('4');
29.       expect(claser.method_2(123)).assertEqual('5');
30.       // 还原obj上所有的Mock能力
31.       mocker.clear(claser);
32.       // 调用claser.method_1,claser.method_2函数，测试结果
33.       expect(claser.method_1(123)).assertEqual('888888');// 断言执行通过
34.       expect(claser.method_2(123)).assertEqual('999999');// 断言执行通过
35.     })
36.   })
37. }

**示例代码8**：使用afterThrow函数抛出指定异常信息

1. import { describe, expect, it, MockKit, when } from '@ohos/hypium';

2. class ClassName {
3.   constructor() {
4.   }

5.   method_1(arg: string) {
6.     return '888888';
7.   }
8. }
9. export default function afterThrowTest() {
10.   describe('afterThrowTest', () => {
11.     it('testMockfunc', 0, () => {
12.       console.info("it1 begin");
13.       // 创建一个Mock能力的对象MockKit
14.       let mocker: MockKit = new MockKit();
15.       // 初始化ClassName的对象claser
16.       let claser: ClassName = new ClassName();
17.       // 进行Mock操作,对ClassName类的method_1函数进行Mock
18.       let mockfunc: Function = mocker.mockFunc(claser, claser.method_1);
19.       // 期望claser.method_1函数被Mock后, 以'test'为参数调用函数时抛出error xxx异常
20.       when(mockfunc)('test').afterThrow('error xxx');
21.       // 执行Mock后的函数，捕捉异常并使用assertEqual对比msg否符合预期
22.       try {
23.         claser.method_1('test');
24.       } catch (e) {
25.         expect(e).assertEqual('error xxx'); // 断言执行通过
26.       }
27.     })
28.   })
29. }

**示例代码9**：Mock异步返回Promise对象

1. import { describe, expect, it, MockKit, when } from '@ohos/hypium';

2. class ClassName {
3.   constructor() {
4.   }

5.   async method_1(arg: string) {
6.     return new Promise<string>((resolve: Function, reject: Function) => {
7.       setTimeout(() => {
8.         console.log('执行');
9.         resolve('数据传递');
10.       }, 2000);
11.     });
12.   }
13. }
14. export default function mockPromiseTest() {
15.   describe('mockPromiseTest', () => {
16.     it('testMockfunc', 0, async (done: Function) => {
17.       console.info("it1 begin");
18.       // 创建一个Mock能力的对象MockKit
19.       let mocker: MockKit = new MockKit();
20.       // 初始化ClassName的对象claser
21.       let claser: ClassName = new ClassName();
22.       // 进行Mock操作对ClassName类的method_1函数进行Mock
23.       let mockfunc: Function = mocker.mockFunc(claser, claser.method_1);
24.       // 期望claser.method_1函数被Mock后, 以'test'为参数调用函数时返回一个Promise对象
25.       when(mockfunc)('test').afterReturn(new Promise<string>((resolve: Function, reject: Function) => {
26.         console.log("do something");
27.         resolve('success something');
28.       }));
29.       // 执行Mock后的函数，即对定义的Promise进行后续执行
30.       let result = await claser.method_1('test');
31.       expect(result).assertEqual("success something");// 断言执行通过
32.       done();
33.     })
34.   })
35. }

**示例代码10**：使用times/atLeast函数验证被Mock函数调用次数

1. import { describe, it, MockKit, when } from '@ohos/hypium'

2. class ClassName {
3.   constructor() {
4.   }

5.   method_1(...arg: string[]) {
6.     return '888888';
7.   }
8. }
9. export default function verifyTimesTest() {
10.   describe('verifyTimesTest', () => {
11.     it('test_verify_times', 0, () => {
12.       // 创建一个Mock能力的对象MockKit
13.       let mocker: MockKit = new MockKit();
14.       // 初始化ClassName的对象claser
15.       let claser: ClassName = new ClassName();
16.       // 进行Mock操作对ClassName类的method_1函数进行Mock
17.       let func_1: Function = mocker.mockFunc(claser, claser.method_1);
18.       // 期望被Mock后的函数返回结果'4'
19.       when(func_1)('123').afterReturn('4');
20.       // 函数调用
21.       claser.method_1('123', 'ppp');
22.       claser.method_1('abc');
23.       claser.method_1('xyz');
24.       claser.method_1();
25.       claser.method_1('abc', 'xxx', 'yyy');
26.       claser.method_1('abc');
27.       claser.method_1();
28.       // 验证函数method_1且参数为'abc'时，执行过的次数是否为2
29.       mocker.verify('method_1', ['abc']).times(2);// 断言执行通过
30.        // 验证函数method_1且参数为空时，是否至少执行过2次
31.       mocker.verify('method_1', []).atLeast(2);// 断言执行通过
32.     })
33.   })
34. }

**示例代码11**：Mock静态函数（从@ohos/hypium 1.0.16版本开始支持）

1. import { describe, it, expect, MockKit, when, ArgumentMatchers } from '@ohos/hypium';

2. class ClassName {
3.   constructor() {
4.   }

5.   static method_1() {
6.     return 'ClassName_method_1_call';
7.   }
8. }

9. export default function staticTest() {
10.   describe('staticTest', () => {
11.     it('staticTest_001', 0, () => {
12.       let really_result = ClassName.method_1();
13.       expect(really_result).assertEqual('ClassName_method_1_call');
14.       // 创建MockKit对象
15.       let mocker: MockKit = new MockKit();
16.       // Mock类ClassName对象的某个函数method_1
17.       let func_1: Function = mocker.mockFunc(ClassName, ClassName.method_1);
18.       // 期望被mock后的函数返回结果'mock_data'
19.       when(func_1)(ArgumentMatchers.any).afterReturn('mock_data');
20.       let mock_result = ClassName.method_1();
21.       expect(mock_result).assertEqual('mock_data');// 断言执行通过
22.       // 清除Mock能力
23.       mocker.clear(ClassName);
24.       let really_result1 = ClassName.method_1();
25.       expect(really_result1).assertEqual('ClassName_method_1_call');// 断言执行通过
26.     })
27.   })
28. }

### 数据驱动

单元测试框架的数据驱动能力从[@ohos/hypium 1.0.2版本](https://ohpm.openharmony.cn/#/cn/detail/@ohos%2Fhypium)开始支持。开发者可以复用测试用例代码，通过数据配置文件配置输入数据和预期结果数据，在用例实现中获取数据进行相应实现和断言处理，减少冗余测试代码。

数据驱动能力可以根据测试数据配置来驱动测试用例的执行次数和每次执行时传入的参数，使用时依赖data.json配置文件，文件内容如下：

说明

data.json与测试用例*.test.js或*.test.ets文件同目录。

data.json文件中的参数配置名称需同测试用例中定义参数名称保持一致。

1. {
2.   "suites": [{
3.     "describe": ["AbilityTest"],
4.     "stress": 2,
5.     "params": {
6.       "suiteParams1": "suiteParams001",
7.       "suiteParams2": "suiteParams002"
8.     },
9.     "items": [{
10.       "it": "testDataDriverAsync",
11.       "stress": 2,
12.       "params": [{
13.         "name": "tom",
14.         "value": 5
15.       }, {
16.         "name": "jerry",
17.         "value": 4
18.       }]
19.     }, {
20.       "it": "testDataDriver",
21.       "stress": 3
22.     }]
23.   }]
24. }

配置参数说明：

|配置项名称|功能|必填|
|:--|:--|:--|
|"suite"|测试套配置。|是|
|"describe"|测试套名称。|是|
|"items"|测试用例。|是|
|"it"|测试用例名称。|是|
|"params"|测试套/测试用例可传入使用的参数。|否|
|"stress"|测试套/测试用例指定执行次数。|否|

**示例代码**

Stage模型在测试工程中的TestAbility目录下TestAbility.ets文件中导入data.json（FA模型在测试工程中的TestAbility目录下的app.js或app.ets文件中导入data.json），并在文件中的Hypium.hypiumTest()函数执行前设置参数数据，参考下面示例代码。

1. import { abilityDelegatorRegistry } from '@kit.TestKit';
2. import { Hypium } from '@ohos/hypium';
3. import testsuite from '../test/List.test';//导入测试用例集合文件
4. import data from '../test/data.json';//导入参数数据文件

5. ...
6. let abilityDelegator = abilityDelegatorRegistry.getAbilityDelegator();
7. let abilityDelegatorArguments = abilityDelegatorRegistry.getArguments();
8. Hypium.setData(data);//设置参数数据
9. Hypium.hypiumTest(abilityDelegator, abilityDelegatorArguments, testsuite);
10. ...

11.  import { describe, it } from '@ohos/hypium';

12.  export default function abilityTest() {
13.   describe('AbilityTest', () => {
14.     it('testDataDriverAsync', 0, async (done: Function, data: ParmObj) => {
15.       console.info('name: ' + data.name);
16.       console.info('value: ' + data.value);
17.       done();
18.     });

19.     it('testDataDriver', 0, () => {
20.       console.info('stress test');
21.     })
22.   })
23. }
24.  interface ParmObj {
25.    name: string,
26.    value: string
27.  }

说明

若要使用数据驱动传入参数功能，测试用例it的func必须传入两个参数：done和data，且入参顺序不可调整。若不使用数据驱动传入参数功能，func可以不传参或仅传入done。

### 专项能力

专项能力提供脚本执行配置能力，包括筛选执行、压力执行、随机执行等，通过命令行方式执行，具体用法请参考[命令行执行测试脚本](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/unittest-guidelines#%E5%91%BD%E4%BB%A4%E8%A1%8C%E6%89%A7%E8%A1%8C%E6%B5%8B%E8%AF%95%E8%84%9A%E6%9C%AC)章节介绍。

## 单元测试框架常见问题

**用例中增加的打印日志在用例结果之后才打印**

**问题描述**

用例中新增的日志打印信息未在执行过程中出现，而是在执行结束之后才显示。

**可能原因**

此类情况仅在用例调用异步接口时出现。为确保日志正确捕获执行过程，用例中所有日志信息必须在用例执行结束前打印。

**解决方法**

当被调用的异步接口数量超过两个时，建议将接口调用封装成Promise方式调用。

**执行用例时报用例超时错误**

**问题描述**

用例执行结束，控制台提示execute time XXms错误，即用例执行超时。

**可能原因**

1. 用例执行异步接口时，如果未调用done函数，会导致用例无法正常结束，最终超时。
2. 用例调用函数耗时过长，超过用例执行设置的超时时间（默认5000ms）。
3. 用例调用函数时断言失败抛出异常，导致用例执行超时终止。

**解决方法**

1. 检查用例代码逻辑，确保断言失败时能走到done函数，完成用例执行。
2. 可在DevEco Studio的Run/Debug Configurations中修改用例执行超时参数，避免执行超时。
3. 检查用例代码逻辑，确保断言通过。
# UI测试框架使用指导

更新时间: 2025-11-20 20:14

## 概述

UI测试框架（UITest）为开发者提供UI界面查找和模拟操作能力，可覆盖UI自动化测试的关键场景，包括界面控件精准查找、UI交互操作（如点击、滑动、文本输入等）、外设行为模拟（如键盘输入、鼠标操作、触控板手势、手写笔动作等），助力开发者开发高效可靠的界面自动化测试用例。

## 功能全景

UITest支持采用ArkTS API与命令行两种方式，为界面自动化测试提供灵活高效的技术支撑，其中：

**ArkTS脚本开发能力：**

提供简洁易用的API接口，满足各类测试场景需求，支持点击、双击、长按、滑动等常用UI交互操作，助力开发者快速开发基于界面交互逻辑的自动化测试脚本。

**命令行测试能力：**

支持通过命令行直接实现多元化测试操作，包括获取当前界面截图、获取控件树、录制界面操作流程、便捷注入UI模拟事件等。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201414.78845495239846142199842242284404:50001231000000:2800:26D8802368510A1F613D6D54B3C65BAE240940C9A8BDE878B7D260938379ADC7.png)

UITest分为客户端和服务端。

**· 客户端：**

包含跨语言通信层、IPC模块等，主要功能为对外导出API，为UI测试框架启动提供入口。客户端由测试应用加载，运行在应用进程。其中，跨语言通信层主要进行接口导出、JSON序列化对象处理、上层ArkTS接口与底层C++接口的转换、参数解析和校验。此外，由于本模块涉及C++层对ArkTS层回调函数的调用，跨语言通信层同时负责ArkTS回调函数的管理和调用。

**· 服务端：**

以独立进程运行，通过IPC与客户端进行通信。服务端启动后，通过广播与客户端建立连接，通过IPC通信确保连接不断开。服务端监听客户端进程状态，实现按需启停。服务端负责UI测试框架核心逻辑的处理，主要分为以下两部分：

1. 框架运行通用能力：进行IPC消息处理、进程管理、C++接口和错误码的管理，包括接口调用监听等。
2. UI测试能力：解析无障碍节点构建页面控件树、控件匹配查找、操作事件构造、多模事件注入、UI事件监听、屏幕显示控制等。

## 使用ArkTS接口进行UI测试

本章节介绍UI测试框架ArkTS API的具体使用方法。

UI测试是在[单元测试](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/unittest-guidelines)基础上进行UITest接口调用，接口的详细定义与参数说明可参考[API文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-uitest)。

### UI测试示例

下面提供一个UI测试的简单示例，介绍如何在单元测试脚本基础上进行UI测试的增量开发，具体实现功能如下：

1. 调用[程序框架服务](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inner-application-abilitydelegator)能力，启动目标被测应用，并确认应用运行状态。
2. 调用UI测试框架能力，页面中执行点击操作。
3. 通过[添加断言](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/unittest-guidelines#%E6%96%AD%E8%A8%80%E8%83%BD%E5%8A%9B)，验证操作后当前页面的实际变化是否与预期结果一致。

开发步骤如下:

1. 在main > ets > pages文件夹下编写Index.ets页面代码，作为被测示例demo。
    
    1. @Entry
    2. @Component
    3. struct Index {
    4.     @State message: string = 'Hello World';
    5.     @State text: string = '';
    6.     build() {
    7.     Row() {
    8.         Column() {
    9.         Text(this.message)
    10.             .fontSize(50)
    11.             .fontWeight(FontWeight.Bold)
    12.         Text("Next")
    13.             .fontSize(50)
    14.             .margin({top:20})
    15.             .fontWeight(FontWeight.Bold)          
    16.             .onClick((event?: ClickEvent) => {
    17.                 if(event){
    18.                     this.text = "after click";
    19.                 }
    20.             })
    21.         .width('100%')
    22.         Text(this.text).margin(15)
    23.         }
    24.     }
    25.     .height('100%')
    26.     }
    27. }
    
2. 在ohosTest > ets > test文件夹下新建uitest.test.ets文件，并编写具体测试代码。
    
    1. import { describe, it, expect, Level } from '@ohos/hypium';
    2. // 导入测试依赖kit
    3. import { abilityDelegatorRegistry, Driver, ON } from '@kit.TestKit';
    4. import { UIAbility, Want } from '@kit.AbilityKit';
    
    5. const delegator: abilityDelegatorRegistry.AbilityDelegator = abilityDelegatorRegistry.getAbilityDelegator();
    6. export default function abilityTest() {
    7.   describe('ActsAbilityTest', () => {
    8.     it('testUiExample',Level.LEVEL3, async (done: Function) => {
    9.       console.info("uitest: TestUiExample begin");        
    10.       // 初始化Driver对象
    11.       const driver = Driver.create();
    12.       const bundleName = abilityDelegatorRegistry.getArguments().bundleName;
    13.       // 指定被测应用包名、ability名，请开发者替换为被测应用包名和ability名
    14.       const want: Want = {
    15.           bundleName: bundleName,
    16.           abilityName: 'EntryAbility'
    17.       }
    18.       // 拉起被测应用
    19.       await delegator.startAbility(want);
    20.       // 等待应用拉起完成
    21.       await driver.waitForIdle(4000,5000);
    22.       // 确认当前应用顶部Ability为指定的ability
    23.       const ability: UIAbility = await delegator.getCurrentTopAbility();
    24.       console.info("get top ability");
    25.       expect(ability.context.abilityInfo.name).assertEqual('EntryAbility');
    
    26.       // 依据指定文本“Next”查找目标控件
    27.       const next = await driver.findComponent(ON.text('Next'));
    28.       // 点击目标控件
    29.       await next.click();
    30.       await driver.waitForIdle(4000,5000);
    31.       // 通过断言文本为“after click”的控件存在，确认操作后页面变化符合预期
    32.       await driver.assertComponentExist(ON.text('after click'));
    33.       await driver.pressBack();
    34.       done();
    35.     })
    36.   })
    37. }
    

### 控件查找与操作

UITest支持[依据多种属性构造匹配器](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-uitest#on9)进行控件查找；支持查找当前页面符合匹配条件的单个或多个目标控件，并返回控件对象；支持在滚动组件内部进行滚动查找目标控件；支持[对控件对象进行操作或获取控件的属性信息](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-uitest#component9)。

如下给出控件查找与操作的示例，下面代码执行前请参考UI测试示例，实现对应的Index.ets页面代码。

1. // ohosTest/ets/test/uitest.test.ets
2. import { describe, it, TestType, Size, Level } from '@ohos/hypium';
3. // 导入测试依赖kit
4. import { Driver, Component, ON, On } from '@kit.TestKit';

5. export default function abilityTest() {
6.   describe('componentOperationTest', () => {
7.     /**
8.      * 查找类型为'Button'的控件，并进行控件点击操作
9.      */
10.     it("componentSearchAndOperation", TestType.FUNCTION, async () => {
11.       let driver: Driver = Driver.create();
12.       let button: Component = await driver.findComponent(ON.type('Button'));
13.       await button.click();
14.     })

15.     /**
16.      * 利用相对位置查找控件，查找'Scroll'类型控件中文本内容为'123'的控件
17.      */
18.     it("relativePositioncomponentSearch", TestType.FUNCTION, async () => {
19.       let driver: Driver = Driver.create();
20.       let on: On = ON.text('123').within(ON.type('Scroll'));
21.       let items: Array<Component> = await driver.findComponents(on);
22.     })

23.     /**
24.      * 查找类型为'Image'的控件，并进行对其进行双指放大操作
25.      */
26.     it("componentPinch", TestType.FUNCTION, async () => {
27.       let driver: Driver = Driver.create();
28.       let image: Component = await driver.findComponent(ON.type('Image'));
29.       await image.pinchOut(1.5);
30.     })
31.   })
32. }

### 模拟触摸屏手指操作

UITest支持模拟包括点击、双击、长按、滑动、拖拽、多指操作等事件。

如下给出触摸屏坐标级的手指操作模拟的示例，下面代码执行前请参考UI测试示例，实现对应的Index.ets页面代码。

1. // ohosTest/ets/test/uitest.test.ets
2. import { describe, it, TestType, Size, Level } from '@ohos/hypium';
3. // 导入测试依赖kit
4. import { Driver, PointerMatrix, UiDirection } from '@kit.TestKit';

5. export default function abilityTest() {
6.   describe('screenOperationTest', () => {
7.     /**
8.      * 基于坐标的触摸屏手指操作
9.      */
10.     it("touchScreenOperation", TestType.FUNCTION, async () => {
11.       let driver: Driver = Driver.create();
12.       // 单击
13.       await driver.click(100,100);
14.       // 指定屏幕id进行单击
15.       await driver.clickAt({ x: 100, y: 100, displayId: 0 });
16.       // 滑动
17.       await driver.swipe(100, 100, 200, 200, 600);
18.       // 指定屏幕id进行滑动
19.       await driver.swipeBetween({x: 100, y: 100, displayId: 0}, {x: 1000, y: 1000, displayId: 0}, 800);
20.       // 抛滑
21.       await driver.fling({x: 100, y: 100},{x: 200, y: 200}, 5, 600);
22.       // 指定方向的抛滑
23.       await driver.fling(UiDirection.DOWN, 10000);
24.       // 拖拽
25.       await driver.drag(100, 100, 200, 200, 600);
26.       // 指定屏幕id和拖拽移动前的长按时间
27.       await driver.dragBetween( {x: 100, y: 100, displayId: 0}, {x: 1000, y: 1000, displayId: 0}, 800, 1500); 
28.       // 多指操作，指定使用两根手指，每根手指基于两个坐标点滑动
29.       let pointers: PointerMatrix = PointerMatrix.create(2, 2);
30.       pointers.setPoint(0, 0, {x: 100, y: 100});
31.       pointers.setPoint(0, 1, {x: 200, y: 100});
32.       pointers.setPoint(1, 0, {x: 100, y: 200});
33.       pointers.setPoint(1, 1, {x: 200, y: 200});
34.       await driver.injectMultiPointerAction(pointers);
35.     })
36.   })
37. }

### 页面加载等待

在与页面进行交互后，可通过在指定时间内等待某控件的出现或等待页面空闲来判断页面跳转是否完成。

如下给出页面加载等待的示例，下面代码执行前请参考UI测试示例，实现对应的Index.ets页面代码。

1. // ohosTest/ets/test/uitest.test.ets
2. import { describe, it, Level, TestType, Size } from '@ohos/hypium';
3. // 导入测试依赖kit
4. import { abilityDelegatorRegistry, Driver, ON } from '@kit.TestKit';

5. const delegator: abilityDelegatorRegistry.AbilityDelegator = abilityDelegatorRegistry.getAbilityDelegator();
6. // 指定被测应用包名、ability名，请开发者替换为被测应用包名和ability名
7. const bundleName: string = 'com.uitestScene.acts'
8. const abilityName: string = 'com.uitestScene.acts.MainAbility'
9. export default function abilityTest() {
10.   describe('ActsAbilityTest', () => {
11.     it('testWaitForComponent_static', TestType.FUNCTION | Size.MEDIUMTEST | Level.LEVEL3, async (): Promise<void> => {
12.       let driver = Driver.create();
13.       // 拉起目标应用      
14.       await delegator.executeShellCommand(`aa start -b ${bundleName} -a ${abilityName}`).then(result => {
15.         console.info(`UITestCase, start abilityFinished: ${result}`)
16.       }).catch((err: Error) => {
17.           console.error(`UITestCase, start abilityFailed: ${err}`)
18.       })
19.       // 通过等待目标应用首页上的指定控件出现，判断应用拉起完成
20.       let button = await driver.waitForComponent(ON.text('StartAbility Success!'), 1000);
21.     })
22.   })
23. }

### 模拟文本输入

UITest支持向指定坐标点或指定控件输入文本内容，同时支持[指定输入方式](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-uitest#inputtextmode20)：输入文本时是否以复制粘贴方式输入、是否以追加的方式进行输入。

如下给出文本输入的示例，包括基于控件的文本输入和基于坐标的文本输入两种方式。下面代码执行前请参考UI测试示例，实现对应的Index.ets页面代码。

1. // ohosTest/ets/test/uitest.test.ets
2. import { describe, it, TestType, Size, Level } from '@ohos/hypium';
3. // 导入测试依赖kit
4. import { Driver, ON } from '@kit.TestKit';

5. export default function abilityTest() {
6.   describe('inputTextTest', () => {
7.     /**
8.      * 基于控件的文本输入，调用接口会默认清空文本框中内容后输入指定文本
9.      * 当输入文本中不包含中文、特殊字符，且文本长度不超过200字符时默认为逐字键入
10.      */
11.     it('componentInputText', TestType.FUNCTION, async () => {
12.       let driver = Driver.create();
13.       let input = await driver.findComponent(ON.type('TextInput'));
14.       await input.inputText('abc');
15.     })
16.     /**
17.      * 基于控件的文本输入，指定以复制粘贴方式注入输入指定文本
18.      * 指定以追加方式输入，即在输入文本签不清空原有内容
19.      */
20.     it('componentInputTextAddition', TestType.FUNCTION, async () => {
21.       let driver = Driver.create();
22.       let input = await driver.findComponent(ON.type('TextInput'));
23.       await input.inputText('abc', {paste: true, addition: true});
24.     })

25.     /**
26.      * 基于坐标的文本输入，点击指定位置使输入框获焦，并在光标处输入指定文本
27.      * 当输入文本中不包含中文、特殊字符，且文本长度不超过200字符时默认为逐字键入
28.      */
29.     it('pointInputText', TestType.FUNCTION | Size.MEDIUMTEST | Level.LEVEL3, async () => {
30.       let driver = Driver.create()
31.       let input = await driver.findComponent(ON.type('TextInput'))
32.       let center = await input.getBoundsCenter()
33.       await driver.inputText(center, 'abc')
34.     })

35.     /**
36.      * 基于坐标的文本输入，指定以复制粘贴方式注入输入指定文本
37.      * 指定以追加方式输入，即点击指定位置使输入框获焦后将光标移动至原有文本末尾后输入
38.      */
39.     it('pointInputTextAddition', TestType.FUNCTION | Size.MEDIUMTEST | Level.LEVEL3, async () => {
40.       let driver = Driver.create()
41.       let input = await driver.findComponent(ON.type('TextInput'))
42.       let center = await input.getBoundsCenter()
43.       await driver.inputText(center, '123', {paste: true, addition: true})
44.     })

45.     /**
46.      * 基于坐标的文本输入，指定以复制粘贴方式注入输入指定文本
47.      * 指定以追加方式输入，即点击指定位置使输入框获焦后将光标移动至原有文本末尾后输入
48.      * 当输入内容包含中文或特殊字符时，仅支持以复制粘贴方式输入文本，'paste'字段不生效
49.      */
50.     it('pointInputTextChinese', TestType.FUNCTION | Size.MEDIUMTEST | Level.LEVEL3, async () => {
51.       let driver = Driver.create()
52.       let input = await driver.findComponent(ON.type('TextInput'))
53.       let center = await input.getBoundsCenter()
54.       await driver.inputText(center, '你好', {paste: false, addition: true})
55.     })
56.   })
57. }

### 截图

说明

1. 指定截图文件保存路径，路径需为当前应用的[沙箱路径](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-sandbox-directory)。
2. 测试HAP的[APL等级级别](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-permission-mgmt-overview#%E6%9D%83%E9%99%90%E6%9C%BA%E5%88%B6%E4%B8%AD%E7%9A%84%E5%9F%BA%E6%9C%AC%E6%A6%82%E5%BF%B5)为normal，对应要求使用用户级加密区的应用沙箱路径。且需指定将文件保存在应用在本设备上存放持久化数据的子目录。

如下给出屏幕截图的示例，指定屏幕id和截取屏幕区域，并将截图保存到指定路径下。下面代码执行前请参考UI测试示例，实现对应的Index.ets页面代码。多屏场景下，期望对指定屏幕做截图操作时，可以调用display模块的接口[获取Display对象](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/screenproperty-guideline#%E8%8E%B7%E5%8F%96display%E5%AF%B9%E8%B1%A1)，实现[屏幕相关属性获取](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/screenproperty-guideline#%E8%8E%B7%E5%8F%96%E5%B1%8F%E5%B9%95%E7%9B%B8%E5%85%B3%E5%B1%9E%E6%80%A7)。

1. // ohosTest/ets/test/uitest.test.ets
2. import { describe, it, TestType, Size, Level } from '@ohos/hypium';
3. // 导入测试依赖kit
4. import { Driver } from '@kit.TestKit';
5. import { display } from '@kit.ArkUI';

6. export default function abilityTest() {
7.   describe('screenCaptureTest', () => {
8.     /**
9.      * 截取指定区域的屏幕，并保存到指定路径
10.      */
11.     it('screenCapture', TestType.FUNCTION, async () => {
12.       let driver = Driver.create();
13.       // 应用沙箱路径，el2为用户级加密区，base为应用在本设备上存放持久化数据的子目录
14.       // 请开发者使用时替换为实际的路径
15.       let savePath = '/data/storage/el2/base/cache/1.png';
16.       let res = await driver.screenCapture(savePath, {left: 0, top: 0, right: 100, bottom: 100});
17.     })

18.     /**
19.      * 截取指定屏幕id的屏幕全屏，并保存到指定路径
20.      */
21.     it('screenCapWithId', TestType.FUNCTION | Size.MEDIUMTEST | Level.LEVEL3, async () => {
22.       let driver = Driver.create();
23.       // 获取默认屏幕对象
24.       let disPlay = display.getDefaultDisplaySync();
25.       let savePath = '/data/storage/el2/base/cache/1.png'
26.       let res = await driver.screenCap(savePath, disPlay.id);// 获取默认屏幕ID属性
27.     })
28.   })
29. }

### UI事件监听

如下给出UI界面事件的监听的示例，设置监听回调函数，监听toast、dialog等控件的出现，等待事件发生后进行下一步操作。下面代码执行前请参考UI测试示例，实现对应的Index.ets页面代码。

1. // ohosTest/ets/test/uitest.test.ets
2. import { describe, it, TestType, Size, Level } from '@ohos/hypium';
3. // 导入测试依赖kit
4. import { Driver, UIElementInfo } from '@kit.TestKit';

5. export default function abilityTest() {
6.   describe('observerTest', () => {
7.     // 监听Toast控件出现
8.     it("toastObserver", TestType.FUNCTION, async () => {
9.       let driver = Driver.create();
10.       let observer = driver.createUIEventObserver();
11.       let callback = (uiElementInfo : UIElementInfo) => {
12.         let bundleName = uiElementInfo.bundleName;
13.         let text = uiElementInfo.text;
14.         let type = uiElementInfo.type;
15.       }
16.       observer.once('toastShow', callback);
17.     })
18.   })
19. }

### 模拟键鼠操作

如下给出键鼠模拟操作，包括键盘按键、组合键输入操作的示例，包括鼠标点击、移动、拖拽操作和键鼠组合操作等。下面代码执行前请参考UI测试示例，实现对应的Index.ets页面代码。

1. // ohosTest/ets/test/uitest.test.ets
2. import { describe, it, TestType, Size, Level } from '@ohos/hypium';
3. // 导入测试依赖kit
4. import { Driver, MouseButton } from '@kit.TestKit';
5. import { KeyCode } from '@ohos.multimodalInput.keyCode';

6. export default function abilityTest() {
7.   describe('KeyboardMouseTest', () => {
8.     // 模拟键盘按键输入、组合键输入
9.     it('keyBoardOperation', TestType.FUNCTION | Size.MEDIUMTEST | Level.LEVEL3, async () => {
10.       let driver = Driver.create();
11.       // 键盘按键输入（注入返回键）
12.       await driver.triggerKey(KeyCode.KEYCODE_BACK);
13.       // 键盘组合键输入（注入保存组合键）
14.       await driver.triggerCombineKeys(KeyCode.KEYCODE_CTRL_LEFT,  KeyCode.KEYCODE_S);
15.     })

16.     // 模拟鼠标左键单击、鼠标移动、鼠标拖拽操作
17.     it('mouseOperation', TestType.FUNCTION | Size.MEDIUMTEST | Level.LEVEL3, async () => {
18.       let driver = Driver.create();
19.       // 鼠标左键单击
20.       await driver.mouseClick({x: 100, y: 100}, MouseButton.MOUSE_BUTTON_LEFT); 
21.       // 鼠标移动
22.       await driver.mouseMoveTo({x: 100, y: 100});
23.       // 鼠标拖拽
24.       await driver.mouseDrag({x: 100, y: 100}, {x: 200, y: 200}, 600);
25.     })

26.     // 模拟键盘、鼠标组合操作
27.     it('combinedOperation', TestType.FUNCTION | Size.MEDIUMTEST | Level.LEVEL3, async () => {
28.       let driver = Driver.create();
29.       // 按下左CTRL键，同时鼠标滚轮滚动
30.       await driver.mouseScroll({x:100, y:100}, true, 30, KeyCode.KEYCODE_CTRL_LEFT);
31.       // 按下左CTRL键，同时鼠标左键长按
32.       await driver.mouseLongClick({x:100, y:100}, MouseButton.MOUSE_BUTTON_LEFT, KeyCode.KEYCODE_CTRL_LEFT);
33.     })
34.   })
35. }

### 窗口查找与操作

如下给出窗口查找和操作的示例，根据窗口属性查找窗口，并进行窗口最小化等操作。下面代码执行前请参考UI测试示例，实现对应的Index.ets页面代码。

1. // ohosTest/ets/test/uitest.test.ets
2. import { describe, it, TestType, expect } from '@ohos/hypium';
3. // 导入测试依赖kit
4. import { Driver } from '@kit.TestKit';
5. const DeviceErrorCode = 17000005;

6. export default function abilityTest() {
7.   describe('windowOperationTest', () => {
8.     // 根据指定条件查找活跃窗口，并对其进行窗口最小化操作
9.     it("windowSearchAndOperation", TestType.FUNCTION, async () => {
10.       let driver = Driver.create();
11.       try {
12.         let window = await driver.findWindow({active: true});
13.         await window.minimize();
14.       } catch (error) {
15.         // 在不支持窗口操作的设备上调用minimize接口操作窗口时，将抛出17000005错误码
16.         console.log(`$ windowSearchAndOperation error is: ${JSON.stringify(error)}`);
17.         expect(error.code).assertEqual(DeviceErrorCode);
18.       }
19.     })
20.   })
21. }

### 模拟触摸板操作

如下给出触摸板模拟操作的示例，触摸板三指上滑返回桌面，三指下滑恢复应用窗口。下面代码执行前请参考UI测试示例，实现对应的Index.ets页面代码。

1. // ohosTest/ets/test/uitest.test.ets
2. import { describe, it, TestType, Size, Level, expect } from '@ohos/hypium';
3. // 导入测试依赖kit
4. import { Driver, UiDirection } from '@kit.TestKit';
5. const DeviceErrorCode = 17000005;

6. export default function abilityTest() {
7.   describe('touchPadOperationTest', () => {
8.     // PC/2in1场景，模拟触摸板三指上滑（界面返回桌面），三指下滑（界面恢复窗口）操作
9.     it('touchPadOperation', TestType.FUNCTION | Size.MEDIUMTEST | Level.LEVEL3, async () => {
10.       let driver = Driver.create();
11.       try {
12.         // 触摸板三指上滑返回桌面。
13.         await driver.touchPadMultiFingerSwipe(3, UiDirection.UP);
14.         // 触摸板三指下滑恢复窗口
15.         await driver.touchPadMultiFingerSwipe(3, UiDirection.DOWN);
16.       } catch (error) {
17.         // 在不支持触摸板操作的设备上调用时，将抛出17000005错误码
18.         console.log(`$ windowSearchAndOperation error is: ${JSON.stringify(error)}`);
19.         expect(error.code).assertEqual(DeviceErrorCode);
20.       }
21.     })
22.   })
23. }

### 模拟手写笔操作

如下给出手写笔模拟操作，包括点击、滑动等操作的示例，支持设置操作时的压力值大小。下面代码执行前请参考UI测试示例，实现对应的Index.ets页面代码。

1. // ohosTest/ets/test/uitest.test.ets
2. import { describe, it, TestType, Size, Level } from '@ohos/hypium';
3. // 导入测试依赖kit
4. import { Driver } from '@kit.TestKit';

5. export default function abilityTest() {
6.   describe('penOperationTest', () => {
7.     // 模拟手写笔单击、双击、长按、滑动操作
8.     it('penOperation', TestType.FUNCTION | Size.MEDIUMTEST | Level.LEVEL3, async () => {
9.       let driver = Driver.create();
10.       // 手写笔单击
11.       await driver.penClick({x: 100, y: 100});
12.       // 手写笔双击
13.       await driver.penDoubleClick({x: 100, y: 100});
14.       // 手写笔长按
15.       await driver.penLongClick({x: 100, y: 100}, 0.5);
16.       // 手写笔滑动
17.       await driver.penSwipe({x: 100, y: 100}, {x: 100, y: 500}, 600, 0.5);
18.     })
19.   })
20. }

### 模拟表冠操作

如下给出表冠模拟操作的示例，包括表冠的顺/逆时针旋转。下面代码执行前请参考UI测试示例，实现对应的Index.ets页面代码。

1. // ohosTest/ets/test/uitest.test.ets
2. import { describe, it, TestType, Size, Level, expect } from '@ohos/hypium';
3. // 导入测试依赖kit
4. import { Driver } from '@kit.TestKit';
5. const CapabilityCode = 801;

6. export default function abilityTest() {
7.   describe('crownRotateTest', () => {
8.     // 手表场景，模拟表冠顺/逆时针旋转
9.     it('crownRotate', TestType.FUNCTION | Size.MEDIUMTEST | Level.LEVEL3, async () => {
10.       let driver = Driver.create();
11.       try {
12.         // 顺时针旋转50格，旋转速度为30格/秒
13.         await driver.crownRotate(50, 30);
14.         // 逆时针旋转20格，旋转速度为30格/秒
15.         await driver.crownRotate(-20, 30);
16.       } catch (error) {
17.         // driver.crownRotate接口仅在智能表设备上生效，其他设备调用时将抛出801错误码
18.         console.log(`$ testCrownRotate error is: ${JSON.stringify(error)}`);
19.         expect(error.code).assertEqual(CapabilityCode);
20.       }
21.     })
22.   })
23. }

### 屏幕显示操作

如下给出屏幕显示操作的示例，包括获取屏幕大小、分辨率等属性和屏幕唤醒、屏幕旋转等操作。下面代码执行前请参考UI测试示例，实现对应的Index.ets页面代码。

1. // ohosTest/ets/test/uitest.test.ets
2. import { describe, it, TestType, Size, Level } from '@ohos/hypium';
3. // 导入测试依赖kit
4. import { Driver, Point } from '@kit.TestKit';

5. export default function abilityTest() {
6.   describe('crownRotateTest', () => {
7.     // 屏幕属性获取和屏幕操作
8.     it('displayOperation', TestType.FUNCTION | Size.MEDIUMTEST | Level.LEVEL3, async () => {
9.       let driver = Driver.create();
10.       // 获取屏幕大小
11.       let size: Point = await driver.getDisplaySize();
12.       // 获取屏幕清晰度
13.       let density: Point = await driver.getDisplayDensity();
14.       // 唤醒屏幕
15.       await driver.wakeUpDisplay();
16.       // 屏幕顺时针旋转90度
17.       await driver.setDisplayRotation(DisplayRotation.ROTATION_90);
18.     })
19.   })
20. }

## 基于命令行进行UI测试

在开发阶段，如果需要快速执行截图、界面操作录制、UI模拟操作注入、控件树获取等测试相关操作，可借助命令行实现，提升测试效率。

### 环境要求

根据hdc命令行工具指导，完成[环境准备](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/hdc#%E7%8E%AF%E5%A2%83%E5%87%86%E5%A4%87)。确保设备已成功连接，并执行hdc shell。

### 命令列表

|命令|参数|说明|
|:--|:--|:--|
|help|-|显示UITest工具能够支持的命令信息。|
|screenCap|[-p] [-d]|截图。<br><br>各参数代表的含义请参考[获取截图](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/uitest-guidelines#%E8%8E%B7%E5%8F%96%E6%88%AA%E5%9B%BE)。|
|dumpLayout|[-p] <-i \| -a \| -b \| -w \| -m \| -d>|获取控件树。<br><br>各参数代表的含义请参考[获取控件树](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/uitest-guidelines#%E8%8E%B7%E5%8F%96%E6%8E%A7%E4%BB%B6%E6%A0%91)。|
|uiRecord|<record \| read>|录制界面操作。<br><br>**record** ：开始录制，将当前界面操作记录到'/data/local/tmp/record.csv'，结束录制操作使用Ctrl+C结束录制。<br><br>**read** ：读取并且打印录制数据。<br><br>各参数代表的含义请参考[录制界面操作](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/uitest-guidelines#%E5%BD%95%E5%88%B6%E7%95%8C%E9%9D%A2%E6%93%8D%E4%BD%9C)。|
|uiInput|<help \| click \| doubleClick \| longClick \| fling \| swipe \| drag \| dircFling \| inputText \| keyEvent \| text>|注入UI模拟操作。<br><br>各参数代表的含义请参考[注入UI模拟操作](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/uitest-guidelines#%E6%B3%A8%E5%85%A5ui%E6%A8%A1%E6%8B%9F%E6%93%8D%E4%BD%9C)。|
|--version|-|获取当前UITest工具版本信息。|
|start-daemon|-|拉起UITest测试进程。|

### 获取截图

|参数|二级参数|说明|
|:--|:--|:--|
|-p|<savePath>|指定存储路径和文件名，只支持存放在'/data/local/tmp/'下。默认存储路径：'/data/local/tmp'，文件名：'时间戳 + .png'。|
|-d|<displayId>|多屏场景下，获取指定ID屏幕下的截图。<br><br>**说明：** 从API version 20开始支持该命令。|

1. # 存储路径：/data/local/tmp，文件名：时间戳 + .png。
2. hdc shell uitest screenCap
3. # 指定存储路径和文件名，存放在/data/local/tmp/下。
4. hdc shell uitest screenCap -p /data/local/tmp/1.png

### 获取控件树

|参数|二级参数|说明|
|:--|:--|:--|
|-p|<savePath>|指定存储路径和文件名，只支持存放在'/data/local/tmp/'下。默认存储路径：'/data/local/tmp'，文件名：'时间戳 + .json'。|
|-i|-|不过滤不可见控件，也不做窗口合并。|
|-a|-|保存控件的BackgroundColor、Content、FontColor、FontSize、extraAttrs属性数据。<br><br>**说明** ：默认不保存上述属性数据， **-a和-i不可同时使用。**|
|-b|<bundleName>|获取指定包名对应目标窗口的控件树信息。|
|-w|<windowId>|获取指定ID目标窗口的控件树信息。<br><br>**说明:**<br><br>可通过hidumper工具[获取应用窗口信息](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/hidumper#%E8%8E%B7%E5%8F%96%E5%BA%94%E7%94%A8%E7%AA%97%E5%8F%A3%E4%BF%A1%E6%81%AF), 包含应用对应窗口的id。|
|-m|<true\|false>|指定在获取控件树信息时是否合并窗口信息。true表示合并窗口信息，false表示不合并窗口信息，不设置时默认为true。|
|-d|<displayId>|多屏场景下，获取指定ID屏幕下的控件树。<br><br>**说明：**<br><br>1. 从API version 20开始支持该命令。<br><br>2. 可通过hidumper工具[获取应用窗口信息](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/hidumper#%E8%8E%B7%E5%8F%96%E5%BA%94%E7%94%A8%E7%AA%97%E5%8F%A3%E4%BF%A1%E6%81%AF)，包含应用对应窗口的DisplayId。|

1. # 指定存储路径和文件名，存放在/data/local/tmp/下。
2. hdc shell uitest dumpLayout -p /data/local/tmp/1.json

### 录制界面操作

说明

录制过程中，需等待当前操作的识别结果在命令行输出后，再进行下一步操作。

**参数列表**

|参数|二级参数|说明|
|:--|:--|:--|
|-W|<true/false>|录制过程中是否保存操作坐标对应的控件信息到/data/local/tmp/record.csv文件中。true表示保存控件信息，false表示仅记录坐标信息，不设置时默认为true。<br><br>**说明：** 从API version 20开始支持该命令。|
|-l|-|在每次操作后保存当前布局信息，文件保存路径：/data/local/tmp/layout_录制启动时间戳_操作序号.json。<br><br>**说明：** 从API version 20开始支持该命令。|
|-c|<true/false>|是否将录制到的操作事件信息打印到控制台，true表示打印，false表示打印，不设置时默认为true。<br><br>**说明：** 从API version 20开始支持该命令。|

1. # 将当前界面操作记录到/data/local/tmp/record.csv，结束录制操作使用Ctrl+C结束录制。
2. hdc shell uitest uiRecord record
3. # 录制时仅记录操作的坐标，不匹配目标控件。
4. hdc shell uitest uiRecord record -W false
5. # 每次操作后，保存页面布局，文件保存路径：/data/local/tmp/layout_录制启动时间戳_操作序号.json。
6. hdc shell uitest uiRecord record -l
7. # 录制到的操作事件信息不打印到控制台。
8. hdc shell uitest uiRecord record -c false
9. # 读取并打印录制数据。
10. hdc shell uitest uiRecord read

录制数据中字段及含义如下。

1. {
2.   "ABILITY": "com.ohos.launcher.MainAbility", // 被操作应用对应的Ability名称
3.   "BUNDLE": "com.ohos.launcher", // 被操作应用对应的包名
4.   "CENTER_X": "", // 预留字段，暂未使用
5.   "CENTER_Y": "", // 预留字段，暂未使用
6.   "EVENT_TYPE": "pointer", // 操作类型
7.   "LENGTH": "0", // 总体步长
8.   "OP_TYPE": "click", //事件类型，当前支持点击、双击、长按、拖拽、滑动、抛滑动作录制
9.   "VELO": "0.000000", // 离手速度
10.   "direction.X": "0.000000",// 总体移动X方向
11.   "direction.Y": "0.000000", // 总体移动Y方向
12.   "duration": 33885000.0, // 手势操作持续时间
13.   "fingerList": [{
14.     "LENGTH": "0", // 总体步长
15.     "MAX_VEL": "40000", // 最大速度
16.     "VELO": "0.000000", // 离手速度
17.     "W1_BOUNDS": "{"bottom":361,"left":37,"right":118,"top":280}", // 起点控件边界
18.     "W1_HIER": "ROOT,3,0,0,0,0,0,0,0,0,5,0,0,0,0,0,0,0", // 起点控件页面层级
19.     "W1_ID": "", // 起点控件id
20.     "W1_Text": "", // 起点控件text
21.     "W1_Type": "Image", // 起点控件类型
22.     "W2_BOUNDS": "{"bottom":361,"left":37,"right":118,"top":280}", // 终点控件边界
23.     "W2_HIER": "ROOT,3,0,0,0,0,0,0,0,0,5,0,0,0,0,0,0,0", // 终点控件页面层级
24.     "W2_ID": "", // 终点控件id
25.     "W2_Text": "", // 终点控件text
26.     "W2_Type": "Image", // 终点控件类型
27.     "X2_POSI": "47", // 终点X
28.     "X_POSI": "47", // 起点X
29.     "Y2_POSI": "301", // 终点Y
30.     "Y_POSI": "301", // 起点Y
31.     "direction.X": "0.000000", // X方向移动量
32.     "direction.Y": "0.000000" // Y方向移动量
33.   }],
34.   "fingerNumber": "1" //手指数量
35. }

### 注入UI模拟操作

|参数|说明|
|:--|:--|
|help|uiInput命令相关帮助信息。|
|click|模拟单击操作。具体请参考下方**uiInput-click/doubleClick/longClick使用示例**。|
|doubleClick|模拟双击操作。具体请参考下方**uiInput click/doubleClick/longClick使用示例**。|
|longClick|模拟长按操作。具体请参考下方**uiInput click/doubleClick/longClick使用示例**。|
|fling|模拟快滑操作，即操作结束后页面存在惯性滚动。具体请参考下方**uiInput fling使用示例**。|
|swipe|模拟慢滑操作。具体请参考下方**uiInput swipe/drag使用示例**。|
|drag|模拟拖拽操作。具体请参考下方**uiInput swipe/drag使用示例**。|
|dircFling|模拟指定方向滑动操作。具体请参考下方**uiInput dircFling使用示例**。|
|inputText|指定坐标点，模拟输入框输入文本操作。具体请参考下方**uiInput inputText使用示例**。|
|text|无需指定坐标点，在当前获焦处，模拟输入框输入文本操作。具体请参考下方**uiInput text使用示例**。<br><br>**说明：** 从API version 18开始支持该命令。|
|keyEvent|模拟实体按键事件（如：键盘，电源键，返回上一级，返回桌面等），以及组合按键操作。具体请参考下方**uiInput keyEvent使用示例**。|

- uiInput-click/doubleClick/longClick使用示例

|参数|必填|说明|
|:--|:--|:--|
|point_x|是|点击x坐标点。|
|point_y|是|点击y坐标点。|

1. # 执行单击事件。
2. hdc shell uitest uiInput click 100 100

3. # 执行双击事件。
4. hdc shell uitest uiInput doubleClick 100 100

5. # 执行长按事件。
6. hdc shell uitest uiInput longClick 100 100

- uiInput fling使用示例

|参数|必填|说明|
|:--|:--|:--|
|from_x|是|滑动起点x坐标。|
|from_y|是|滑动起点y坐标。|
|to_x|是|滑动终点x坐标。|
|to_y|是|滑动终点y坐标。|
|swipeVelocityPps_|否|滑动速度，单位：px/s，取值范围：200-40000。<br><br>默认值：600。取值超出限定范围时，取默认值。|
|stepLength_|否|滑动步长，单位：px。默认值：滑动距离/50。<br><br>**说明：**<br><br>滑动距离根据入参给出的滑动起止坐标点计算得出。<br><br>**为实现更好的模拟效果，推荐参数缺省/使用默认值。**|

1. # 执行快滑操作，stepLength_缺省。
2. hdc shell uitest uiInput fling 10 10 200 200 500 

- uiInput swipe/drag使用示例

|参数|必填|说明|
|:--|:--|:--|
|from_x|是|滑动起点x坐标。|
|from_y|是|滑动起点y坐标。|
|to_x|是|滑动终点x坐标。|
|to_y|是|滑动终点y坐标。|
|swipeVelocityPps_|否|滑动速度，单位：px/s，取值范围：200-40000。<br><br>默认值：600。取值超出限定范围时，取默认值。|

1. # 执行慢滑操作。
2. hdc shell uitest uiInput swipe 10 10 200 200 500

3. # 执行拖拽操作。 
4. hdc shell uitest uiInput drag 10 10 100 100 500 

- uiInput dircFling使用示例

|参数|必填|说明|
|:--|:--|:--|
|direction|否|滑动方向，取值范围：[0,1,2,3]，默认值为0。<br><br>0代表向左滑动，1代表向右滑动，2代表向上滑动，3代表向下滑动。|
|swipeVelocityPps_|否|滑动速度，单位：px/s，取值范围：200-40000。<br><br>**默认值**: 600。取值超出限定范围时，取默认值。|
|stepLength|否|滑动步长，单位：px。<br><br>**默认值**： 如果滑动方向为0、1，默认值为屏幕宽度/200； 如果滑动方向为2、3，默认值为屏幕高度/200。为更好的模拟效果，推荐参数缺省/使用默认值。|

1. # 执行左滑操作。
2. hdc shell uitest uiInput dircFling 0 500
3. # 执行向右滑动操作。
4. hdc shell uitest uiInput dircFling 1 600
5. # 执行向上滑动操作。
6. hdc shell uitest uiInput dircFling 2 
7. # 执行向下滑动操作。
8. hdc shell uitest uiInput dircFling 3

- uiInput inputText使用示例

|参数|必填|说明|
|:--|:--|:--|
|point_x|是|输入框x坐标点。|
|point_y|是|输入框y坐标点。|
|text|是|输入文本内容。|

1. # 执行输入框输入操作。
2. hdc shell uitest uiInput inputText 100 100 hello 

- uiInput text使用示例

|参数|必填|说明|
|:--|:--|:--|
|text|是|输入文本内容。|

1. # 无需输入坐标点，在当前获焦处，执行输入框输入操作。若当前获焦处不支持文本输入，则无实际效果。
2. hdc shell uitest uiInput text hello

- uiInput keyEvent使用示例

|参数|必填|说明|
|:--|:--|:--|
|keyID1|是|实体按键对应ID，取值范围：Back、Home、Power、或[KeyCode键码值](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-keycode#keycode)。<br><br>当取值为Back、Home或Power时，不支持输入组合键。<br><br>当前注入大写锁定键（KeyCode=2074）无效，请使用组合键实现大写字母输入。如“按键shift+按键V”输入大写字母V。|
|keyID2|否|实体按键对应ID，取值范围：[KeyCode键码值](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-keycode#keycode)，默认值为空。|
|keyID3|否|实体按键对应ID，取值范围：[KeyCode键码值](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-keycode#keycode)，默认值为空。|

1. # 返回主页。
2. hdc shell uitest uiInput keyEvent Home
3. # 返回。
4. hdc shell uitest uiInput keyEvent Back
5. # 组合键粘贴。
6. hdc shell uitest uiInput keyEvent 2072 2038
7. # 输入小写字母v。
8. hdc shell uitest uiInput keyEvent 2038
9. # 输入大写字母V。
10. hdc shell uitest uiInput keyEvent 2047 2038

### 获取版本信息

1. hdc shell uitest --version

### 拉起UITest测试进程

说明

仅元能力aa test拉起的测试HAP才能调用Uitest的能力，且测试HAP的[APL等级级别](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-permission-mgmt-overview#%E6%9D%83%E9%99%90%E6%9C%BA%E5%88%B6%E4%B8%AD%E7%9A%84%E5%9F%BA%E6%9C%AC%E6%A6%82%E5%BF%B5)需为normal。

1. hdc shell uitest start-daemon

## 常见问题

### 失败日志有“uitest-api does not allow calling concurrently”错误信息

**问题描述**

UI测试用例执行失败，查看hilog日志发现日志中有“uitest-api does not allow calling concurrently”错误信息。

**可能原因**

1. 用例中UI测试框架提供异步接口没有增加await语法糖调用。
2. 多进程执行UI测试用例，导致拉起多个UITest进程，框架不支持多进程调用。

**解决方法**

1. 检查用例实现，异步接口增加await语法糖调用。
2. 避免多进程执行UI测试用例。

### 失败日志有“does not exist on current UI! Check if the UI has changed after you got the widget object”错误信息

**问题描述**

UI测试用例执行失败，查看hilog日志发现日志中有“does not exist on current UI! Check if the UI has changed after you got the widget object”错误信息。

**可能原因**

在用例中代码查找到目标控件后，设备界面发生了变化，导致查找到的控件丢失，无法进行下一步的模拟操作。

**解决方法**

重新执行UI测试用例，确保进行模拟操作时控件在界面中存在。

### 失败日志有“Cannot connect to AAMS, RET_ERR_CONNECTION_EXIST”错误信息

**问题描述**

UI测试用例执行失败，查看hilog日志发现日志中有“Cannot connect to AAMS, RET_ERR_CONNECTION_EXIST”错误信息。

**可能原因**

在用例执行的同时使用了其他依赖UI测试框架运行的测试工具。

**解决方法**

关闭依赖UI测试框架运行的测试工具或重启设备。
# 白盒性能测试框架使用指导

更新时间: 2025-11-20 20:14

## 简介

白盒性能测试框架（PerfTest），提供了针对指定代码段运行时的白盒性能测试能力，用于度量指定应用进程的性能表现。框架通过多轮迭代执行机制和环境复位机制实现自动化测试，支持耗时、CPU使用率等基础数据和启动时延、滑动帧率等场景化性能数据的采集和度量。使用PerfTest接口的性能测试脚本需基于单元测试框架进行开发。

从API version 20开始，支持白盒性能测试能力。

## 实现原理

PerfTest功能设计图如下所示：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201420.08235822268208420505628151000796:50001231000000:2800:3D056E236C2083D3E124E348E9869DFE0BDCA6349E4C233F36A0A353C750D920.png)

PerfTest对外提供ArkTS API，包括性能测试策略设置、性能测试执行、测试结果获取等能力。具体请参考[API文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-perftest)。

跨语言通信层负责上层ArkTS接口与底层C++接口的转换，包括参数校验、JSON序列化对象处理和异常处理等。作为PerfTest的客户端，它提供启动入口和功能调用接口。该层由测试应用加载运行，通过IPC与服务端通信实现功能调用和生命周期管理。此外，该层还负责管理C++层对ArkTS回调函数的调用。

PerfTest服务端负责白盒性能测试框架的主要功能处理，包含以下两部分：

- 框架运行通用能力：管理C++接口和错误码，包括接口调用、参数解析、异常处理等。PerfTest服务端以独立进程运行，通过IPC与客户端通信，监听客户端生命周期，实现进程保活和按需启停。
    
- 白盒性能测试能力：主要负责测试任务调度和性能数据采集工作。根据用户定义的测试策略，实现测试代码段运行、性能数据采集、数据处理和存储的自动化性能测试流程。当前支持采集的性能指标包括：耗时、CPU、内存、应用启动时延、页面切换时延、列表滑动帧率等。
    

## 开发步骤

使用PerfTest接口进行白盒性能测试流程如下图所示：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201420.62351256972883955922534336185361:50001231000000:2800:DEF670D79F6274CD3B52F83850D40BEAC501BA9C42D416A64C3FBFA0338BE756.png)

1. 定义性能测试策略，明确测试指标列表、被测代码段、环境复位代码段、被测应用包名、测试迭代次数、代码段单次执行超时时间等，后续白盒性能测试中将依照此策略执行测试。
    
2. 创建测试任务，配置测试策略并准备测试环境。
    
3. 启动测试，将根据测试迭代次数执行多轮测试。每轮测试采集被测代码段执行期间的性能数据，并执行环境复位代码段恢复环境。完成后进行数据处理和保存。
    
4. 获取测量数据值，结果存储在对象中，支持获取每轮测试详细数据和最大值、最小值、平均值等统计数据。
    
5. 销毁创建的对象，释放内存占用。
    

下面以采集指定代码段执行期间的耗时、CPU使用率为例，介绍详细代码开发步骤。

### 定义测试策略

1. 定义测试性能指标列表
    
    定义所需测试的性能指标列表metrics，类型为Array<PerfMetric>，其中[PerfMetric](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-perftest#perfmetric)为框架支持采集的性能指标枚举。
    
    1. let metrics: Array<PerfMetric> = [ PerfMetric.DURATION, PerfMetric.CPU_USAGE ];
    
2. 定义被测代码段和环境复位代码段
    
    被测代码段actionCode是一个类型为Callback<Callback<boolean>>的回调函数，框架在测试期间会自动调用此回调函数，并采集性能数据。执行结束时需调用入参Callback<boolean>函数通知框架执行完成，否则会导致代码段执行超时。例如测试Utils.CalculateTest方法性能时，通过调用finish(true)通知框架代码段执行完成。
    
    1. let actionCode: Callback<Callback<boolean>> = async (finish: Callback<boolean>) => {
    2.     Utils.CalculateTest();
    3.     finish(true);
    4. };
    
    此外，框架支持定义环境复位代码段resetCode，用于在单次测试后进行环境复位，类型和使用方法与actionCode相同。resetCode会在actionCode执行完成后执行，但执行期间不会采集应用性能数据。
    
    1. let resetCode: Callback<Callback<boolean>> = async (finish: Callback<boolean>) => {
    2.     Utils.Reset();
    3.     finish(true);
    4. };
    
3. 构造测试策略对象
    
    除以上步骤定义的属性外，框架还支持定义其他测试策略，从而帮助开发者进行更加精确的自动化性能测试。所有测试策略通过[PerfTestStrategy](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-perftest#perfteststrategy)对象定义和保存，性能测试期间会依据此策略执行并采集数据。
    
    1. let perfTestStrategy: PerfTestStrategy = {
    2.     metrics: metrics,   // 步骤1中定义
    3.     actionCode: actionCode,   // 步骤2中定义
    4.     resetCode: resetCode,   // 步骤2中定义
    5.     bundleName: "com.example.test", // 定义被测应用包名
    6.     iterations: 10,  // 定义测试迭代次数
    7.     timeout: 20000  // 定义代码段单次执行超时时间，单位ms
    8. };
    

### 创建测试任务和启动测试

使用[PerfTest.create()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-perftest#create)创建测试任务时，传入上文定义的PerfTestStrategy对象。然后调用[PerfTest.run()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-perftest#run)异步接口启动测试。测试会自动迭代执行被测代码段并采集性能数据。使用await语法糖同步等待执行完成后再进行后续操作。

1. let perfTest: PerfTest = PerfTest.create(perfTestStrategy);
2. await perfTest.run();

### 获取测试结果

性能测试运行完成后，调用[PerfTest.getMeasureResult()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-perftest#getmeasureresult)获取各个指标的测试结果。结果存储在[PerfMeasureResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-perftest#perfmeasureresult)对象中。若测试未完成或指标未定义，则抛出错误码。

1. let res1: PerfMeasureResult = perfTest.getMeasureResult(PerfMetric.DURATION);
2. let res2: PerfMeasureResult = perfTest.getMeasureResult(PerfMetric.CPU_USAGE);

### 销毁创建的对象

性能测试完成后，若无需继续使用PerfTest对象，可以调用[PerfTest.destroy()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-perftest#destroy)销毁对象以释放内存。

1. perfTest.destroy();

## 完整示例

### 基础性能数据采集示例

下面以测试应用内指定逻辑执行时的基础性能数据为例，应用内定义了一个名为'Utils.CalculateTest()'的方法，性能测试时执行此方法，并采集执行期间的耗时和应用CPU占用率。

1. 在 main > ets > utils 文件夹下新增 Utils.ets 文件，在文件中编写自定义的函数。
    
    1. export class Utils {
    2.   static num: number = 0
    3.   public static CalculateTest() {
    4.     for (let index = 0; index < 10000; index++) {
    5.       Utils.num++;
    6.     }
    7.   }
    8.   public static Reset() {
    9.     Utils.num = 0
    10.   }
    11. }
    
2. 在 ohosTest > ets > test 文件夹下 PerfTest.test.ets 文件中编写具体测试代码。
    
    1. import { describe, it, expect, Level } from '@ohos/hypium';
    2. import { PerfMetric, PerfTest, PerfTestStrategy, PerfMeasureResult } from '@kit.TestKit';
    3. import { Utils } from '../../../main/ets/utils/Utils'
    
    4. export default function PerfTestTest() {
    5.   describe('PerfTestTest', () => {
    6.     it('testExample1', 0, async (done: Function) => {
    7.       let metrics: Array<PerfMetric> = [ PerfMetric.DURATION, PerfMetric.CPU_USAGE ]; // 定义待测指标
    8.       let actionCode: Callback<Callback<boolean>> = async (finish: Callback<boolean>) => {  // 定义被测代码段
    9.         Utils.CalculateTest();
    10.         finish(true);
    11.       };
    12.       let resetCode: Callback<Callback<boolean>> = async (finish: Callback<boolean>) => {  // 定义环境复位代码段
    13.         Utils.Reset();
    14.         finish(true);
    15.       };
    16.       let perfTestStrategy: PerfTestStrategy = {  // 定义测试策略
    17.         metrics: metrics,
    18.         actionCode: actionCode,
    19.         resetCode: resetCode,
    20.         bundleName: "com.example.test", // 定义被测应用包名，请开发者替换为实际包名
    21.         iterations: 10,  // 定义测试迭代次数
    22.         timeout: 20000  // 定义代码段单次执行超时时间
    23.       };
    24.       try {
    25.         let perfTest: PerfTest = PerfTest.create(perfTestStrategy); // 创建测试任务对象PerfTest
    26.         await perfTest.run(); // 执行测试，异步函数需使用await同步等待完成
    27.         let res1: PerfMeasureResult = perfTest.getMeasureResult(PerfMetric.DURATION); // 获取耗时指标的测试结果
    28.         let res2: PerfMeasureResult = perfTest.getMeasureResult(PerfMetric.CPU_USAGE); // 获取CPU使用率指标的测试结果
    29.         perfTest.destroy(); // 销毁PerfTest对象
    30.         expect(res1.average).assertLessOrEqual(1000); // 断言性能测试结果
    31.         expect(res2.average).assertLessOrEqual(30); // 断言性能测试结果
    32.       } catch (error) {
    33.         console.error(`Failed to execute perftest. Cause:${JSON.stringify(error)}`);
    34.         expect(false).assertTrue()
    35.       }
    36.       done()
    37.     })
    38.   })
    39. }
    

### 场景化性能数据采集示例

下面以测试应用内列表滑动的帧率为例，实现如下功能：打开指定应用，使用UI测试框架接口查找类型为'Scroll'的可滚动组件，并进行滑动操作，采集期间的列表滑动帧率数据。

1. 在 main > ets > pages 文件夹下编写 Index.ets 页面代码，作为被测示例demo。
    
    1. @Entry
    2. @Component
    3. struct ListPage {
    4.   scroller: Scroller = new Scroller()
    5.   private arr: number[] = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
    6.   build() {
    7.     Row() {
    8.       Column() {
    9.         Scroll(this.scroller) {
    10.           Column() {
    11.             ForEach(this.arr, (item: number) => {
    12.               Text(item.toString())
    13.                 .width('90%')
    14.                 .height('40%')
    15.                 .fontSize(80)
    16.                 .textAlign(TextAlign.Center)
    17.                 .margin({ top: 10 })
    18.             }, (item: string) => item)
    19.           }
    20.         }
    21.         .width('100%')
    22.         .height('100%')
    23.         .scrollable(ScrollDirection.Vertical)
    24.         .scrollBar(BarState.On)
    25.         .scrollBarColor(Color.Gray)
    26.       }
    27.       .width('100%')
    28.     }
    29.     .height('100%')
    30.   }
    31. }
    
2. 在ohosTest > ets > test文件夹下 PerfTest.test.ets 文件中编写具体测试代码。
    
    1. import { describe, it, expect, Level } from '@ohos/hypium';
    2. import { PerfMetric, PerfTest, PerfTestStrategy, PerfMeasureResult } from '@kit.TestKit';
    3. import { abilityDelegatorRegistry, Driver, ON } from '@kit.TestKit';
    4. import { Want } from '@kit.AbilityKit';
    
    5. const delegator: abilityDelegatorRegistry.AbilityDelegator = abilityDelegatorRegistry.getAbilityDelegator();
    6.   export default function PerfTestTest() {
    7.     describe('PerfTestTest', () => {
    8.     it('testExample2',Level.LEVEL3, async (done: Function) => {
    9.         let driver = Driver.create();
    10.         await driver.delayMs(1000);
    11.         const bundleName = abilityDelegatorRegistry.getArguments().bundleName;
    12.         // 被拉起应用的包名和Ability组件名，请开发者替换为实际的bundleName和abilityName
    13.         const want: Want = {
    14.             bundleName: bundleName,
    15.             abilityName: 'EntryAbility'
    16.         };
    17.         await delegator.startAbility(want); // 拉起测试应用
    18.         await driver.delayMs(1000);
    19.         let scroll = await driver.findComponent(ON.type('Scroll'));
    20.         await driver.delayMs(1000);
    21.         let center = await scroll.getBoundsCenter();  // 获取Scroll可滚动组件坐标
    22.         await driver.delayMs(1000);
    23.         let metrics: Array<PerfMetric> = [PerfMetric.LIST_SWIPE_FPS]  // 指定被测指标为列表滑动帧率
    24.         let actionCode = async (finish: Callback<boolean>) => { // 测试代码段中使用uitest进行列表滑动
    25.             await driver.fling({x: center.x, y: Math.floor(center.y * 3 / 2)}, {x: center.x, y: Math.floor(center.y / 2)}, 50, 20000);
    26.             await driver.delayMs(3000);
    27.             finish(true);
    28.         };
    29.         let resetCode = async (finish: Callback<boolean>) => {  // 复位环境，将列表划至顶部
    30.             await scroll.scrollToTop(40000);
    31.             await driver.delayMs(1000);
    32.             finish(true);
    33.         };
    34.         let perfTestStrategy: PerfTestStrategy = {  // 定义测试策略
    35.             metrics: metrics,
    36.             actionCode: actionCode,
    37.             resetCode: resetCode,
    38.             iterations: 5,  // 指定测试迭代次数
    39.             timeout: 50000, // 指定actionCode和resetCode的超时时间
    40.         };
    41.         try {
    42.             let perfTest: PerfTest = PerfTest.create(perfTestStrategy); // 创建测试任务对象PerfTest
    43.             await perfTest.run(); // 执行测试，异步函数需使用await同步等待完成
    44.             let res: PerfMeasureResult = perfTest.getMeasureResult(PerfMetric.LIST_SWIPE_FPS); // 获取列表滑动帧率指标的测试结果
    45.             perfTest.destroy(); // 销毁PerfTest对象
    46.             expect(res.average).assertLargerOrEqual(60);  // 断言性能测试结果
    47.         } catch (error) {
    48.             console.error(`Failed to execute perftest. Cause:${JSON.stringify(error)}`);
    49.         }
    50.         done();
    51.       })
    52.   })
    53. }
    # 应用UI测试（基于Python）

更新时间: 2025-11-20 20:14

## 框架概述

DevEco Testing Hypium （以下简称Hypium）是HarmonyOS平台的UI自动化测试框架，支持用户使用Python语言为应用编写UI自动化测试脚本，主要包含以下特性：

1. Hypium提供了控件、图像和比例坐标等**多种控件定位能力**，支持多窗口操作以及触摸屏/鼠标/键盘等**多种模拟输入功能**，支持**多设备**并行操作，能够覆盖各类场景和多种形态设备上的自动化用例编写需求，可支持鸿蒙手机、平板、PC等设备。
2. Hypium提供了在PyCharm中使用的**用例编写辅助插件**，支持控件查看/投屏操作等多种用例开发辅助功能，提升用例开发体验和效率。
3. Hypium能够为执行的用例生成详细的**用例执行报告**，并且自动记录设备日志以及执行步骤截图，为用户提供高效和专业的测试用例执行和结果分析体验。

## 安装向导

**1.安装Python**

推荐从[Python官网](https://www.python.org/)安装Python3.10版本。

**2.安装PyCharm**

推荐从[PyCharm官网](https://www.jetbrains.com.cn/en-us/pycharm/)安装2022.3以后的社区版本。

说明

项目创建功能只支持2022.3至2025.1的Pycharm版本。2024.3版本由于pycharm自身原因，只能选择单设备模板进行创建。

**3.安装hdc**

请参考[调试工具-hdc](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/hdc)中环境准备章节来安装和配置hdc环境。

**4.安装****Hypium**

- **方式一：****PyPI在线安装(推荐)**

在命令行中执行以下命令安装最新版本hypium

1. pip install hypium -U

- **方式二：安装包离线安装**

访问华为开发者联盟官网[下载DevEco Testing Hypium安装包](https://developer.huawei.com/consumer/cn/download/deveco-testing-hypium)。下载后解压该安装包，找到其中的hypium-6.0.6.210.zip（此版本仅作为示例，请以实际版本号为准）。再次解压hypium-6.0.6.210.zip，进入解压后的文件目录执行以下命令，按照顺序安装4个安装包（命令中版本号仅做示例，请以实际版本号为准）。

1. python -m pip install xdevice-6.0.6.210.tar.gz
2. python -m pip install xdevice-devicetest-6.0.6.210.tar.gz
3. python -m pip install xdevice-ohos-6.0.6.210.tar.gz
4. python -m pip install hypium-6.0.6.210.tar.gz

5. # 此版本仅作为示例，实际请根据项目使用的版本选择

**5.DevEco Testing Hypium插件安装及使用方法**

注意

Mac系统使用UiViewer功能时，需在设置面板中手动指定hdc路径，详情可见 **本小节中 · 插件功能 Ⅳ.设置面板区域-hdc路径**。

- **插件安装**

Ⅰ. 访问华为开发者联盟官网[下载页面](https://developer.huawei.com/consumer/cn/download/deveco-testing-hypium)下载DevEco Testing Hypium安装包，下载后解压该安装包，找到其中的hypium-pycharm-plugin-6.0.6.210.zip（该版本号仅做示例，请以实际版本号为准），此文件为插件的安装包，无需再进行解压。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201405.50017809029220841853682943944410:50001231000000:2800:0F40F90BE0EDA9E7CF0E35AA95F2B0CC7B28477C7EC4E732292BB9223BF76A71.jpg "点击放大")

Ⅱ. 打开PyCharm后，点击File -> Settings -> Plugin -> 齿轮图标 -> Install Plugin from Disk。在弹出的文件选择器中，选择第一步下载的hypium-pycharm-plugin-6.0.6.210.zip（该版本号仅做示例，请以实际版本号为准）离线安装包，完成安装。安装完成后，重启PyCharm即可使用新安装的DevecoTesting Hypium插件。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201405.79018542235005810953611640047586:50001231000000:2800:FDA91109BDDC2EF2A6AA2872E4775C2E6C4759646A1E26B372D755E1F2712175.png "点击放大")

安装完成后在Plugins界面可以看到DevEcoTesting-Hypium插件。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201405.53227865896386394748847824341408:50001231000000:2800:10644B567D8869AD3AD1F578CDF86B2AB7955FF30529BE03B58A300DE8BDD76F.png)

- **插件功能**

PyCharm有三个主要的开发功能区，如下图所示。DevEco Testing Hypium插件在不同的开发功能区提供了对应的用例开发辅助功能，在PyCharm的设置面板中提供了插件的设置功能，在PyCharm的工程新建面板中提供了用例工程模板创建功能，下文分区域介绍这些功能。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201406.12374351644313895426381003228709:50001231000000:2800:C303E6E26BECDA4B78DD799F15628923396920F78073E7465F824A6161631444.png "点击放大")

**Ⅰ. 项目文件区域**

在项目文件区域右键点击项目目录或者文件，选择 DevEco Testing Hypium，弹出对应的功能菜单。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201406.61545505152547531761235195599060:50001231000000:2800:5C2441F30A51B4A512966421FF088DEF35B38BB1E90FF6AE41C20E80855D6BD1.png)

功能菜单根据选择的目录和文件不同存在区别，详细参见下表：

|序号|功能|图片|说明|注意|
|:--|:--|:--|:--|:--|
|1|执行当前目录|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201406.85104574551377483775438090656591:50001231000000:2800:C5C684F9C4E2AF8E410F8726D2AD6082F950F41168E26058DCE18F2523C76902.jpg "点击放大")|执行当前目录中的所有测试用例。|此功能仅右键选中文件夹时可用。|
|2|一键执行当前用例|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201406.08658201135721961065835456245332:50001231000000:2800:C4B76DE397259567DFF7566B9426DA291D216D392A83951F02D4ECB571C321E5.jpg "点击放大")|执行当前选中的测试用例文件。|此功能仅右键选中测试用例对应Python或JSON文件时可用。|
|3|生成Hypium模板用例|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201406.12558147629227675314036750296840:50001231000000:2800:12C0AC32BADDF3CEA1EDD221ED43F1E304474B71B9D6D9F0B1B24FFE1E21EF83.jpg "点击放大")|在当前选中的目录下生成测试用例模板文件。|此功能右键选中testcases或其子文件夹时可用。|
|4|生成Hypium模板测试套|在当前选中的目录下生成测试套模板文件。|此功能仅右键选中testcases或其子文件夹时可用。|
|5|生成测试服务包|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201406.70844819322512196519275109912693:50001231000000:2800:3A9B5710C0D08632202C1315F60A5A3BAC2C962AFBB1BC918A052BDDB213500D.png "点击放大")|该功能支持生成“回归测试”和“场景化性能”两种类型的测试服务包模板，用户可根据实际需求填写配置项，完成设置后即可生成对应的测试服务包。|1. 该功能仅在右键点击项目根目录时可用，选中其他目录无法触发此功能。<br>2. 项目根目录下需要包含 testcases 文件夹。<br>3. 项目根目录下需存在 setup-sceneperf.py 或 setup-regression.py 文件之一，以支持相应测试服务包的生成。|

**Ⅱ. 代码编辑区域**

|序号|功能|图片|说明|注意|
|:--|:--|:--|:--|:--|
|1|一键执行当前用例|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201406.90203348925432347838918538310076:50001231000000:2800:16ACA9C9E0D555C6DC07B8F14D7C5220AC231D1B06B7AA2BB1C907ED37DD506D.jpg "点击放大")|执行当前文件对应的测试用例。|此功能仅在当前项目根目录下存在config文件夹和testcases文件夹时可用。|
|2|一键调试当前用例|以调试模式执行当前文件对应的测试用例|此功能仅在当前项目根目录下存在config文件夹和testcases文件夹时可用。|
|3|选区快速执行|快速执行选中的代码片段，无需运行整个用例。|1. 此功能仅在正常连接被测设备时可用。<br><br>2. 此功能仅在当前项目根目录下存在config文件夹和testcases文件夹时可用。|
|4|选区快速调试|以调试模式快速执行选中的代码片段。|1. 此功能仅在正常连接被测设备时可用。<br><br>2. 此功能仅在当前项目根目录下存在config文件夹和testcases文件夹时可用。|
|5|生成Hypium模板代码|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201406.86825211024100639018697505098154:50001231000000:2800:00B076EB643300C7E5AB5B633609E67019F1A42BDF9EE2E7A21F8058D3C22150.png "点击放大")|快速生成内置的模板操作代码。||
|6|函数快速执行|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201406.74292705364270966021287879804850:50001231000000:2800:C6732DF16B4CD5D1451506B4AB6B0B3140C2A2EEBE5E1D772B0E9C2B2A01B84E.jpg "点击放大")|快速执行测试用例中的指定生命周期函数。|1. 此功能仅在正常连接被测设备时可用。<br><br>2. 此功能仅在当前项目根目录下存在config文件夹和testcases文件夹时可用。<br><br>3. 此功能仅在当前编辑的文件为Hypium测试用例Python文件时可用。|

**Ⅲ. ToolWindow区域**

**UiViewer功能**

DevEco Testing Hypium插件会在PyCharm界面右边缘的ToolWindow区域生成UiViewer标签，点击后会展开UiViewer功能面板。UiViewer功能目前分为4个界面：设备选择界面 、单设备控件查看界面 、单设备投屏界面 、双设备投屏界面。

注意

UiViewer插件当前仅支持USB连接本地设备调测，暂不支持模拟器。

**设备选择界面**

设备选择界面如下图所示， 若首次进入该界面，或设备状态发生变化，需点击“刷新”按钮以更新设备列表。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201406.62115431248717290831105159588832:50001231000000:2800:C5E82E44EABBD046F50DE52F5CDC9DC67443196543E68E2820960C8DA5FBA129.png "点击放大")

设备信息说明见下表：

|序号|参数名称|说明|
|:--|:--|:--|
|1|SN（Serial Number）号|该参数为已连接设备的序列号（SN号），用于区分不同设备。|
|2|设备类型|该参数为设备连接通道类型，仅支持hdc连接，对应设备类型显示为HDC。|
|3|设备状态|该参数显示当前设备是否支持使用 UiViewer 工具：“OK” 表示该设备可用；“NOT_SUPPORT” 表示设备不可用。|
|4|设备编号|该参数用于在多设备同时投屏时配置各设备的显示位置，用户可手动进行调整。<br><br>在双设备投屏界面中，默认情况下，设备编号为 dev1 的设备显示在左侧，设备编号为 dev2 的设备显示在右侧。|

设备选择界面最多支持同时选择两个设备进行投屏。

- 若仅勾选一个设备并点击“确定”按钮，则进入单设备投屏界面。
- 若勾选了两个设备并点击“确定”按钮，将进入双设备投屏界面；其中，设备编号为 “dev1” 的设备显示在左侧，设备编号为 “dev2”的设备显示在右侧，用户可以通过设备编号的下拉选项框自定义配置设备编号，控制双设备投屏。

**单设备投屏界面**

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201406.10233271932078310966747122081375:50001231000000:2800:38582B83D6F047862E915BDAA589105EABE43DA5E2484DB4C781D91DD5BCC34C.png "点击放大")

**功能说明：**

- **设备切换按钮：**点击后返回设备选择界面，可重新选择要投屏的设备。
- **设备屏幕显示区域：**显示当前设备的实时屏幕画面。在投屏模式下，可通过鼠标点击或滑动该界面来操作设备。
- **工具区：**位于设备屏幕显示区域右侧，从上至下分为以下三个子工具区。

**工具区1：**

该工具区提供控件查看功能。进入控件查看模式后，设备画面将保持静止，不再实时更新。若需获取当前页面的最新控件信息，需手动点击“控件刷新”按钮以重新抓取页面结构和控件数据。

|序号|图标|功能|说明|
|:--|:--|:--|:--|
|1|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201406.94624995896660926839676001824549:50001231000000:2800:48AD6633E0C041A928153CCC869B9A14C43D13E88CAC9D0719AE8339B9AFD807.jpg)|查看控件|点击该按钮进入控件查看模式，插件会读取设备当前的控件树和屏幕截图，并显示到界面上（此过程需要一定时间，在鼠标光标处于转圈状态时，请勿点击其他按钮，以免操作冲突或导致异常）。在控件查看模式下再次点击该按钮，可退出当前模式，返回实时投屏模式。|
|2|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201406.93546521501796988340171563984554:50001231000000:2800:E465654B16CFA948B19099520039792DA9BD35C4253062FD2FDEB080D83D4014.jpg)|进入高级控件查看模式|点击该按钮进入高级控件查看模式，系统会根据鼠标移动实时高亮对应控件，并持续展示其控件信息。点击某一控件信息后，将自动切换到普通控件查看模式，并定位显示该控件在控件树中的详细信息。<br><br>处于高级控件查看模式时，再次点击该按钮，可退出当前模式，则返回实时投屏模式。|
|3|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201406.28137906700037723895050956179400:50001231000000:2800:98E23E33AF59616631D21DAE9B2F4395FC87BAF3A7C2FB44F4385A6347EFF16D.png)|录制Hypium测试用例脚本|点击该按钮进入操作录制模式，在此模式下，用户点击或操作投屏画面中的控件时，系统将自动识别操作行为，并在编辑器当前光标位置生成对应的 Hypium 自动化测试脚本代码。<br><br>处于操作录制模式时，再次点击该按钮可退出当前模式，返回实时投屏模式。|
|4|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201406.69564348874702187498524427845151:50001231000000:2800:3A073B652125163F6B742E61786E93DC21CDC98733F3A0041E65AE3A236F85AE.jpg)|刷新控件|如果设备界面发生变动，可点击此按钮重新获取当前页面的最新控件信息。|

**工具区2：**

此工具区提供一系列常用的设备操作功能，便于在投屏过程中快速执行基本控制与调试操作，当前支持的功能见下表：

|序号|图标|功能|说明|
|:--|:--|:--|:--|
|1|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201407.05587622682384637894974147444401:50001231000000:2800:1B2C9D632A969F41BD8064D4F3D5CB778F99DE631AA4283AF15C5C76549543ED.jpg)|提高音量|点击后对设备进行音量加操作。|
|2|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201407.74208582034919763887095265245300:50001231000000:2800:DB9C17BCF7BE855CC2165B416CCEF3E60D6D33DF4130B0F35781A822DB2D7B23.jpg)|降低音量|点击后对设备进行音量减操作。|
|3|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201407.58767670516018046113711215160365:50001231000000:2800:54A23A4A7F21789AE433A861AA1FF1E1F5C10C96D4C6D36488027E670A7EAA16.jpg)|触发电源键|点击后模拟按下设备电源键。|
|4|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201407.78591146452057232461528389248206:50001231000000:2800:716A9EE60FF7BD6355E9EEC17EDF24969138C9F019ABFEE9296EEEC3E6020F94.jpg)|执行重启操作|点击后重启设备。|
|5|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201407.03231926730833651443446373326380:50001231000000:2800:3933F247F8B4A691F39697E2EDAD2009CB705BF2A09B079925894F51E87CE8B5.jpg)|触发返回键|点击后模拟返回键操作。|
|6|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201407.76427298170139423168512646201482:50001231000000:2800:63EED7A371811B876E37B0D6F5D99838D291135A84D4E30159DE0C00A9DA100B.jpg)|触发返回桌面操作|点击后模拟返回桌面操作。|

**工具区3：**

此工具区提供系统管理相关功能，当前支持的功能见下表：

|序号|图标|功能|说明|
|:--|:--|:--|:--|
|1|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201407.98541070925456551507782805108537:50001231000000:2800:16333CE782405C653051870662C737CDDAC09CE21A2A990AE5E02323203C173D.jpg)|查看设备信息|点击后在“设备信息展示区”显示当前设备的信息。|
|2|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201407.41406318738902371183623888172913:50001231000000:2800:FE2F09500D9AC0E8D29C530E59BBE870D3FEAAA42DAC82FCD3678B4B93DF040C.jpg)|执行全屏截图|点击后会将当前屏幕画面保存至当前项目的“resource”文件夹下的“Hypium”目录下。|
|3|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201407.16264001076622625180799831545486:50001231000000:2800:E8E17B73A741BD3003912ED2005215F8CC9E6C96898BFC84F711650714AD6B08.jpg)|执行区域截图|点击该按钮后，设备显示界面将进入区域截图状态。此时，在设备画面中按住鼠标左键并拖动，可自由框选需要截图的区域。松开鼠标后，系统将对选定区域进行截图，并自动保存至当前项目的 resource/Hypium/ 目录下。|
|4|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201407.07492242186174506235080906115367:50001231000000:2800:C834C0D8AD95768D2791C0B56D83A800A43E8DDF937A33043663DB69E90439AE.jpg)|切换竖屏|将设备屏幕方向设置为竖屏（Portrait）状态。点击该按钮后，设备将旋转显示方向至竖屏模式。此操作会向设备发送系统指令，实际效果取决于当前应用是否支持方向控制。|
|5|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201407.22150330048660173672610987925568:50001231000000:2800:0C7FDF9136C10011332F587E4509B2051DA962700BFE01D919D83F053AFDD2BE.jpg)|切换横屏|将设备屏幕方向设置为横屏（Landscape）状态。点击该按钮后，设备将旋转显示方向至横屏模式。此操作会向设备发送系统指令，实际效果取决于当前应用是否支持方向控制。|
|6|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201407.74232666952457493238374034294408:50001231000000:2800:0A89FCC05BC17A3E36F341DE4DD1409EA8E1D65A1C727BFDEC46CFFE95F520AD.jpg)|安装应用|点击该按钮后，用户可以从本地计算机选择一个HAP文件安装到连接的设备中。|
|7|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201407.40256406701481524629314304023584:50001231000000:2800:78F8E3D45D73EBAEB0C360A21668D3AFED2EF1A6C1CBFCB736E4270AE4F04965.jpg)|卸载应用|用户可对当前连接设备上已安装的应用程序进行卸载操作。点击该按钮后，系统将获取设备上已安装应用列表，用户可从中选择目标应用并执行卸载。|
|8|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201407.40543376073595395049377825228856:50001231000000:2800:C06660FF852298EA8145DD5FA7B3582795453068BD01BCFCE10245F61160668B.jpg)|发送文件|用户可以从电脑本地选择单个文件或整个目录，通过此功能将其发送至设备端指定的存储路径。|
|9|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201407.86849773507712882086225094872852:50001231000000:2800:8CCF3BEDCE66D5C700B38A88323BF3BFD2EE0F596C972063CECE389621BABA46.jpg)|管理应用|点击该按钮后将打开一个独立的应用管理界面，用户可以在应用管理界面安装和卸载应用。|
|10|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201407.87142205770271113630625786449500:50001231000000:2800:E08EDAE2EF3DC50E6CE55A4FA194B5E1319DD912B6D1D279F92C415F8E76F3B3.png)|录制文本输入|此按钮在进入录制状态后才能够使用。点击此按钮后将进入录制输入状态，此时点击界面上要进行输入的文本框控件后，会弹出一个输出框；用户在输入框中输入要插入的文本后点击确定，此时工具便会在代码编辑区光标处生成录制出的文本输入语句，同时设备侧也会自动输入文本。|

**双设备投屏界面**

该界面支持同时对两个设备进行投屏与操作，双设备投屏时，每个设备的显示区域功能与单设备投屏一致，支持独立触摸控制、截图、旋转等操作。

当需要对某一设备进行控件查看时，插件将自动退出双设备投屏模式，切换至单设备控件查看界面，以确保控件信息的准确展示与操作体验。完成控件查看后，用户可手动返回双设备投屏视图。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201407.07581835520526338202564736642344:50001231000000:2800:49DE3020CC346A106A34C3CCD44324ABD49A071A9C4D7604067E609FAAE470FD.png "点击放大")

**执行结果报告展示功能**

使用“一键执行当前用例”功能完成测试用例执行后，插件将在控制台旁边自动生成执行结果标签。点击该标签，即可查看本次用例执行过程中各步骤的截图。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201407.34140818554796434666540206538650:50001231000000:2800:8C6C10E2D43B158EC0D234E5EA9C4F0A0C7216DDF3307B09921D6791E229B763.png "点击放大")

**Ⅳ. 设置面板区**

打开PyCharm设置面板，选中左侧的DevEco Testing Hypium选项，可以进入DevEco Testing Hypium的设置面板，如下图所示。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201408.46956873617881855487471893256672:50001231000000:2800:7EFC8789113EE3ACFE85264B874A3BDFA9A8251180B610EF309B8E9CA579C9F7.png)

各个配置项的详细说明见下表：

|序号|功能|说明|注意|
|:--|:--|:--|:--|
|1|配置文件路径|配置一键执行/调试功能所使用的配置文件路径，如不设置，默认使用当前项目下的config文件夹作为配置文件路径。|-|
|2|测试用例路径|配置一键执行/调试功能所使用的测试文件路径，如不设置，则默认使用当前项目下的testcases文件夹作为测试用例路径。|-|
|3|额外执行参数|配置运行用例一键执行/调试功能时，额外传递给Hypium测试框架的命令行参数。例如用户需要开启Hypium框架的用例单步骤截图功能，可以将额外执行参数设置为“-ta screenshot:true”。|-|
|4|是否以bin模式执行|配置是否以bin模式执行用例时，通过该模式执行时，可避免投屏和用例执行冲突。|**正常使用时该选项无需配置。**<br><br>该设置项在DevEco Testing Hypium 6.0.5.200以及更新的版本中不再需要，已移除。|
|5|hdc路径|配置UiViewer所使用的hdc路径。|-|
|6|高级控件查看模式自动刷新间隔|配置UiViewer功能中的高级控件查看模式的刷新间隔，默认60秒自动重新获取一次界面的布局，最小时间可以设为30秒，最大时间300秒。|-|
|7|录制步骤是否生成性能脚本|操作录制模式默认生成功能测试脚本，通过该选项可以配置生成性能测试步骤脚本。注意执行性能测试脚本需要首先安装hypium-perf性能测试插件。|该功能仅DevEco Testing Hypium 6.0.5.200以及更新的版本支持。|
|8|是否使用视频流投屏模式|配置是否使用视频流模式投屏。当投屏异常时，可尝试将此选项改为否，切换投屏方式，注意此时的投屏帧率大幅降低，|**正常使用时该选项无需进行配置。**|
|9|依赖下载参数|配置生成测试服务包下载PyPI依赖包是传递给pip命令的额外参数。例如出现依赖下载慢或失败的情况时，可设置“-i <PyPI Source>”参数，配置可正常访问的PyPI源。|-|
|10|本地依赖文件存放文件夹|设置该文件夹后，在生成测试服务包时，插件将优先使用该目录中已下载的依赖文件，避免重复在线下载，有效应对因网络问题导致的PyPI依赖包安装失败等场景。|-|

**Ⅴ. 工程创建区域**

在PyCharm顶部点击File -> New Project 进入模板工程创建面板。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201408.70601960760747259199840907414656:50001231000000:2800:7C9A864EECBEED9B2406C986B3BE9F9957B641B509391085E3F27A4AD338D9E3.png)

点击左侧的DevEco Testing Hypium，可以创建Hypium用例模板工程。共有两种类型的Hypium模板工程，分别对应单设备和双设备的测试场景。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201408.34905664195849182806055745779114:50001231000000:2800:21871D97B1F77298EBD85269A50CC1AA2D6AA5174105AB7BDC8322F1D3A234DC.jpg "点击放大")

选择对应模板，配置工程路径以及Python环境参数，点击Create即可创建Hypium测试用例工程。工程目录中包含一个模板用例和一个模板配置文件user_config.xml。

以单设备工程为例，创建完成后的界面如下图所示。连接被测设备后，可右键点击模板用例文件代码编辑区域“执行hypium用例”来运行当前用例。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201408.83577085193401748189495583896501:50001231000000:2800:7131CB7A2B7D0E92BBC42A10294BE5F08342DDC5200492B9A4CF5285BC72B9CE.png)

## 测试脚本开发快速入门

本章节将指导用户创建并执行一个简单的测试脚本工程，快速掌握项目目录结构中的关键文件，熟悉基于Hypium的测试脚本开发流程。

- **测试脚本工程创建**

测试脚本工程创建主要有两种方式：

a）直接使用以下附件中的模板工程。

[HypiumProjectTemplate.zip](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201409.75697659191060809151386814142127:50001231000000:2800:ADE23F1AAA8A021B240473886EAFB71696B0D00B61A73CD86433262511E31C90.zip?needInitFileName=true)

b）通过PyCharm上的DevEcoTesting-Hypium插件进行创建。请参考本文档的**“安装向导 -> DevEco Testing Hypium插件安装及使用方法 -> 插件功能 -> 工程创建区域****”**小节。

**Ⅰ.工程目录文件介绍**

1. HypiumProjectTemplate
2. |     |----aw                                     // 工程中自定义模块文件夹
3. |     |     |----Utils.py                           // 示例模块文件
4. |     |----config                                   // 测试工程配置文件夹
5. |     |     |----user_config.xml                    // 测试工程配置文件
6. |     |----resource                              // 测试资源文件夹，测试过程中用到的资源文件默认会优先从当前文件夹进行查找。
7. |     |----testcases                             // 测试用例文件夹，测试过程中的测试用例文件优先会从当前文件夹进行查找。
8. |     |    |----Example.json                        // Example测试用例配置文件，配置用例所需设备等参数。
9. |     |    |----Example.py                          // Example测试用例文件，存储测试逻辑代码。注意该文件无法直接运行，要通过测试框架启动后加载执行，详情参见后文测试用例执行部分。
10. |     |----main.py                               // 测试用例执行入口文件，用户可以通过运行该文件启动测试任务，执行测试用例。

**Ⅱ.工程配置文件介绍**

1. <?xml version="1.0" encoding="UTF-8"?>
2. <user_config>
3.     <environment>
4.         <!-- type: 设备连接方式，仅支持设置为usb-hdc，表示使用hdc命令控制设备（默认)。 -->
5.         <device type="usb-hdc">
6.             <!-- ip: 远端hdc server的ip地址，ip和port为空时使用本地设备，非空时使用远端设备。 -->
7.             <!-- port: 远端hdc server的端口号 -->
8.             <!-- sn：设备序列号，设为空时，表示所有设备均可用 -->
9.             <info ip="" port="" sn="sn"/>
10.             <!-- 可添加多个info标签，配置多个设备 -->
11.             <info ip="" port="" sn="sn"/>
12.         </device>
13.     </environment>
14.     <testcases>
15.         <!-- 测试用例目录，该属性为空时默认使用为当前项目下的testcases目录。 -->
16.         <dir></dir>
17.     </testcases>
18.     <resource>
19.         <!-- 测试资源文件目录，该属性为空时默认使用为当前项目下的resource目录。 -->
20.         <dir></dir>
21.     </resource>
22.     <!-- 用例执行日志级别，当前仅支持设置为INFO或者DEBUG，默认为INFO，如需更详细信息可设置为DEBUG。 -->
23.     <loglevel>DEBUG</loglevel>
24.     <devicelog>
25.         <!-- 指定用例执行完成后自动从设备端拉取的文件目录，多个目录使用分号分隔。 -->
26.         <dir>/data/log/tee;/data/log/test</dir>
27.         <!-- 设置用例执行时抓取的hilog日志等级，默认值为INFO。 -->
28.         <loglevel>DEBUG</loglevel>    
29.         <!-- 设置单个用例执行完成并抓取设备端hilog日志文件后，是否自动清空设备端的日志文件，默认值为true。-->
30.         <clear></clear>                
31.         <!-- 设置用例执行完成后是否抓取设备端hilog日志文件，默认值为ON。注意设置为OFF时上述devicelog配置下的dir、loglevel以及clear属性不生效。 -->
32.         <enable>ON</enable>            
33.     </devicelog>
34.     <taskargs>
35.         <!-- pass_through，透传参数给测试用例。如{"task_id":"950191","user_define":{"execType":"3"}} -->
36.         <!-- 参数获取方法：from xdevice import Variables; print(Variables.config.pass_through) -->
37.         <pass_through></pass_through>
38.         <!-- repeat，用例重复运行多少次。大于1的整数才生效 -->
39.         <repeat></repeat>
40.         <!-- screenshot，操作类接口运行后是否截图。true开启/false不开启，默认值false -->
41.         <screenshot>false</screenshot>
42.         <!-- screenrecorder，用例Step步骤是否录屏。true开启/false不开启，默认值false -->
43.         <screenrecorder>false</screenrecorder>
44.     </taskargs>   
45. </user_config>

**Ⅲ.测试用例介绍**

Hypium 测试用例由两部分组成：测试用例配置文件（JSON 格式）和测试用例脚本文件（Python 格式）。测试用例的组织方式支持两种模式：

- **单个用例模式：**包含一个测试用例脚本（Python）文件和一个测试用例配置（JSON）文件；
- **测试套模式：**包含一个测试套脚本（Python）文件、多个测试用例脚本（Python）文件和一个测试套配置（JSON）文件。

用户可根据实际需求选择合适的组织方式。

**单个测试用例模式**

- **测试用例脚本文件**

该文件包含测试用例的执行逻辑，核心为三个关键的生命周期函数：setup、process、teardown。在用例开发时，用户需要根据业务需求在对应的函数中编写测试逻辑代码。生命周期函数的详细说明见下表：

|序号|生命周期函数|说明|
|:--|:--|:--|
|1|setup|测试用例的前置步骤，主要用于执行测试用例的预置动作。|
|2|process|测试用例的实际操作步骤，主要描述当前测试用例中的所有测试用例步骤集合。|
|3|teardown|测试用例的清理步骤，主要用于执行测试用例的环境清理等操作。|

**示例代码**

1. # !/usr/bin/env python
2. # coding: utf-8
3. **from** devicetest.core.test_case **import** TestCase, Step
4. **from** devicetest.utils.file_util **import** get_resource_path
5. **from** hypium **import** *
6. **from** aw import Utils
7. **class Example**(TestCase):
8.     def **__init__**(self, controllers):
9.         self.TAG = self.__class__.__name__
10.         TestCase.__init__(self, self.TAG, controllers)
11.         self.driver = UiDriver(self.device1)
12.     def **setup**(self):
13.         Step('1.回到桌面')
14.         self.driver.swipe_to_home()
15.     def **process**(self):
16.         Step('2.检查短信应用版本')
17.         mms_version = Utils.get_app_version_code(self.driver, 'com.ohos.mms')
18.         host.check_greater(mms_version, 0)
19.         Step('3.点击桌面上的短信')
20.         self.driver.touch(BY.text("信息"))
21.     def **teardown**(self):
22.         Step("4. 停止短信应用")
23.         self.driver.stop_app("com.ohos.mms")

- **测试用例配置文件**

该文件主要描述测试用例的配置信息，如测试用例所需设备类型和数量、测试用例的测试驱动信息、测试用例的描述信息等。

**注意**：JSON文件不支持注释，请在使用示例时移除其中以 “//”开头的注释部分。

**示例：**

1. {
2.     // description属性为测试用例的功能描述。
3.     "description": "Config for app test suites",
4.     // environment属性用于配置测试用例需要的设备类型和数量。
5.     "environment": [
6.         {
7.             "type": "device",   // 设备操作系统类型，device表示HarmonyOS设备。
8.             "label": "phone"    // 设备物理形态，phone为手机，tablet为平板，设置为空字符串或者移除该属性表示用例对设备类型无要求。用户可以通过执行hdc shell param get const.product.devicetype查看设备类型。
9.         }，
10.         {
11.             "type": "device",   // 测试用例需要多个设备时，在environment属性中添加多个设备配置项。
12.             "label": "phone"
13.         }
14.     ],
15.     // driver字段主要描述测试用例的测试驱动是什么，以及具体要执行的Python脚本文件在哪（填写与当前JSON文件的相对路径即可）
16.     // 不填写则在当前JSON文件下寻找同名Python文件
17.     "driver": {
18.         "type": "DeviceTest",
19.            }
20. }

**测试套模式**

- **测试套脚本文件**

该文件包含测试套的初始化和清理逻辑，核心为两个关键的生命周期函数：setup、teardown。在用例开发时，用户需要根据业务需求在对应的函数中编写测试逻辑代码。生命周期函数的详细说明见下表：

|序号|生命周期函数|说明|
|:--|:--|:--|
|1|setup|整个测试套的前置步骤，在测试套运行前先执行该函数。|
|2|teardown|整个测试套的清理步骤，在执行完所有测试用例后执行。|

**示例代码**

1. **from** devicetest.core.test_case **import** Step
2. **from** devicetest.core.suite.test_suite **import** TestSuite
3. **class** Testsuite1(TestSuite):
4.     # 测试套的前置步骤将在所有测试用例执行前运行。当多个测试用例具有相同的初始化操作时，可将共用的前置逻辑定义在此。
5.    ** def** **setup**(self):
6.         Step("TestSuite: setup")
7.     # 测试套的清理步骤会在所有测试用例执行完成后运行。
8.    **def** **teardown**(self):
9.         Step("TestSuite: teardown")

- **测试套配置文件**

该文件主要描述测试套的配置信息，如测试套所需设备类型和数量、测试套的测试驱动信息、测试套的描述信息等。

**注意**：JSON文件不支持注释，请在使用示例时移除其中以 “//”开头的注释部分。

**示例代码**

1. {
2.     "description": "Config for app test suites",
3.     // environment属性用于配置测试用例需要的设备类型和数量。
4.     "environment": [
5.         {
6.             "type": "device",     // 配置设备操作系统类型，device表示HarmonyOS设备。
7.             "label": "phone"      // 设备物理形态，phone为手机，tablet为平板，设置为空字符串或者移除该属性表示用例对设备类型无要求。用户可以通过执行hdc shell param get const.product.devicetype查看设备类型。
8.         }
9.     ],
10.     // driver 属性用于定义测试用例的驱动类型及待执行脚本的路径，脚本路径需为相对于当前 JSON 文件的路径。
11.     "driver": {
12.         "type": "DeviceTestSuite",
13.         // 指定测试套配置（JSON）文件对应的测试套脚本（Python）文件路径（可省略 .py 后缀），支持相对路径或绝对路径。若使用相对路径，需相对于测试工程根目录；若未指定，则默认查找与当前 JSON 文件同目录下同名的 Python文件。
14.         "testsuite": "TS_001/TS_001",
15.         // 指定测试套中的测试用例脚本(Python)文件列表，指定方式有两种。
16.         // 方式一：定义 suitecases 字段，并在其中指定测试用例脚本文件的路径。路径可使用相对路径或绝对路径；若使用相对路径，其根目录为当前测试套目录。
17.         "suitecases": [
18.             "TestCase1.py",         // 相对路径
19.             "/path/to/TestCase2.py" // 绝对路径
20.         ]
21.         // 方式二：将测试用例脚本（Python）文件保存到测试套目录中，并且设置文件名前缀为"TC_"，框架即可自动扫描当前测试套对应的所有测试用例脚本文件。
22.     },
23.     // kits字段主要描述测试用例需要的测试公共kit，如pushkit、shellkit等
24.     "kits": []
25. }

- **测试用例脚本文件**

测试套模式中的测试用例脚本文件和单个测试用例中对应文件完全相同，请参考上文**“单个测试用例模式** -> **测试用例脚本文件**“小节。此处介绍测试用例脚本文件和测试套关联的两种方式：

**方式一：**框架自动扫描的与测试套关联的测试用例脚本，测试用例脚本的保存目录和文件命名需要满足以下规则：

1. 测试用例脚本文件需与测试套脚本文件位于同一目录。
2. 测试用例脚本文件的文件名前缀是“TC_”（例如：TC_Login.py）。

**方式二：** 在测试套配置文件中指定所有的测试用例脚本文件路径，详情请参考上文的**“测试套配置文件“**小节。

- **测试用例执行**

本章节主要介绍测试用例的执行方式。测试用例支持两种执行方式：一是通过命令行执行，二是通过 PyCharm IDE 中的DevEco Testing Hypium 插件进行一键执行。

**命令介绍**

Hypium框架命令可以分为三类：help、list和run。其中run为最常用的执行命令。

**命令交互入口**

打开命令行窗口，切换到测试脚本工程的根目录，执行以下命令可以进入Hypium控制台。

1. python -m hypium

**常用命令介绍**

**help命令**

输入help指令可以查询框架指令帮助信息。

1. **help:**
2.    ** use help** to get information.  
3. usage:
4.     **run:  Display** a **list** of supported run command.
5.     **list: Display** a **list** of supported device and task record.  
6. Examples:
7.     **help run**
8.     **help list**

说明

help run：展示run指令相关说明；help list：展示 list指令相关说明。

**list命令**

list指令用来展示设备和相关的任务信息。

1. list:
2.     This command **is** used to display device list and task record.  
3. usage:
4.       list
5.       list history
6.       list <id> 
7. Introduction:
8.     list:         display device list
9.     list history: display history record of a serial of tasks
10.     list <id>:    display history record about task what contains specific id  
11. Examples:
12.     list
13.     list history
14.     list 6e****90

说明

list：展示设备信息；

list history：展示任务历史信息；

list< id >：展示特定id的任务其历史信息。

**run命令**

run指令主要用于执行测试任务。

1. run:
2.     This command **is** used to execute the selected testcases.
3.     It includes a series of processes such **as** use case compilation, execution, and result collection.  
4. usage: run [-l TESTLIST [TESTLIST ...] | -tf TESTFILE
5.             [TESTFILE ...]] [-tc TESTCASE] [-c CONFIG] [-sn DEVICE_SN]
6.             [-rp REPORT_PATH [REPORT_PATH ...]]
7.             [-respath RESOURCE_PATH [RESOURCE_PATH ...]]
8.             [-tcpath TESTCASES_PATH [TESTCASES_PATH ...]]
9.             [-ta TESTARGS [TESTARGS ...]]
10.             [-env TEST_ENVIRONMENT [TEST_ENVIRONMENT ...]]
11.             [--retry RETRY] [--session SESSION]
12.             [--repeat REPEAT]
13.             action task  
14. Specify tests to run.
15.   positional arguments:
16.   action                Specify action
17.   task                    Specify task name,such as "ssts", "acts", "hits"

run常用指令基本使用方式如下：

|序号|hypium命令|功能|示例|
|:--|:--|:--|:--|
|1|run -l <testcase>|运行指定测试用例。如有多个测试用例，测试用例之间以分号分隔。|run -l Example1;Example2|
|2|run -sn|指定运行设备SN号，多个SN号之间以分号分隔（英文分号）。|run -l Example1 -sn sn1<br><br>run -l Example1 -sn sn1;sn2|
|3|run -rp|指定报告生成路径，默认报告生成在项目根目录下的reports文件夹，以时间戳或任务id建立子目录。|run -l Example1 -rp /path/to/report|
|4|run -respath|指定测试资源路径，默认为项目根目录下的resource文件夹。|run -l Example1 -respath /path/to/resource|
|5|run -tcpath|指定测试用例路径,默认为项目根目录下的testcases文件夹。|run -l Example1 -tcpath /path/to/testcases|
|6|run - ta|指定模块运行参数，当前仅支持配置步骤截图开关，配置方式参考示例。|run -l Example1 -ta screenshot:true|
|7|run --retry|重新运行上次失败的测试用例，通过-session指定report任务报告目录。|run --retry --session 2022-12-13-12-21-11|

**PyCharm中用例执行**

Pycharm中执行用例依赖本文档的安装向导部分介绍的PyCharm插件： DevEco Testing Hypium，请参考本文档的**“安装向导 -> DevEco Testing Hypium插件安装及使用方法”**小节。

**测试报告查看**

测试框架执行完用例后，会生成执行结果报告。报告默认存放在测试工程目录的reports目录下。如果用户在启动测试任务时通过-rp参数指定了报告路径，报告会生成在指定的路径下。

测试报告目录结构如下：

1. 当前报告目录（默认目录/指定目录）
2.     ├── details（用例步骤截图存放目录）
3.     ├── result（模块执行结果存放目录）
4.     │     ├── <测试用例1结果>.xml
5.     │     ├──  ... ...  
6.     ├── log (设备和任务运行log存放目录)
7.     │     ├── <测试用例1设备执行>.log
8.     │     ├── ... ...
9.     │     ├── <任务执行>.log
10.     ├── static (报告展示页面css元素存放目录)
11.     ├── summary_report.html（测试任务可视化报告）
12.     ├── summary_report.xml（测试任务数据报告）
13.     ├── summary.ini（记录测试类型，使用的设备，开始时间和结束时间等信息）
14.     ├── task_info.record（记录执行命令，失败用例等清单信息）

## API使用说明

Hypium测试框架提供了两大类API来支持用例的编写：设备相关API和设备无关API。

设备相关的API主要包括四个基础API类：**UiDriver，BY，IUiComponent，UiWindow**。

- **UiDriver**类为UI测试的入口，代表了一个被测设备，提供控件查找、控件检查、用户操作模拟、执行shell命令、安装卸载应用等UI测试核心能力。
- **BY**对象用于描述需要操作的控件属性，实现控件定位。
- **IUiComponent**为UiDriver查找返回的控件对象，提供控件属性查询、控件点击、滑动查找等触控/检视能力。
- **UiWindow**为UiDriver查找返回的窗口对象，提供窗口属性查询、窗口拖动、大小调整等触控能力。

**示例代码**

1. # -*- coding: utf-8 -*-
2. from devicetest.core.test_case import TestCase, Step, CheckPoint
3. from hypium import *
4. from hypium.model import WindowFilter
5. class DemoCase(TestCase):
6.     def __init__(self, configs):
7.         self.TAG = self.__class__.__name__
8.         TestCase.__init__(self, self.TAG, configs)
9.     def setup(self):
10.         pass

11.     def process(self):
12.         _#_ _创建driver对象（self.device1__对象在测试用例类中提供）_
13.         driver = UiDriver(self.device1)
14.         _#_ _查找控件_
15.         component = driver.find_component(BY.text("蓝牙"))
16.         _#_ _查找窗口_
17.         window = driver.find_window(WindowFilter().bundle_name("com.huawei.hmos.settings"))
18.     def teardown(self):
19.         pass

设备无关的API当前主要包括两个基础API类： **host** 和**CV**。

- **host** 提供基础值断言，PC端shell命令执行等PC端基础操作能力。
- **CV** 提供图像查找，图像比较，压缩，清晰度计算等基础图像操作能力。

**示例代码**

1. **from** hypium **import** host, CV

2. _# 执行PC端命令_
3. echo = host.shell("a.bat")
4. _# 调用图像接口_
5. brightness = CV.calculate_brightness("/path/to/image.jpeg")

此外Hypium还包含一些常量类型，例如**KeyCode，UiParam，MatchPattern**等，以及数据类型**Point，Rect**等。

**示例代码**

1. **from** hypium.model **import** KeyCode, UiParam, MatchPattern

2. _# 按下电源键（使用常量KeyCode.POWER）_
3. driver.press_key(KeyCode.POWER)
4. _# 向左滑动屏幕（使用常量UiParam.LEFT）_
5. driver.swipe(UiParam.LEFT)

下文各小节将详细介绍主要测试场景中Hypium的API的使用方法。

## API使用方法

- **控件查看**

通过 DevEco Testing Hypium插件中的 UiViewer 工具，可以查看界面控件的各项属性，有助于在后续测试用例开发中准确定位控件。具体使用方法请参考本文档的**“安装向导 -> DevEco Testing Hypium插件安装及使用方法**“小节。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201408.57136852970050197613525942569656:50001231000000:2800:FF3F7DBB5109F3C27AC1509FB996F283A23042892EB0B6A818E8D8B73E3C3BBF.png "点击放大")

- **控件查找**

Hypium 支持三种主要的控件定位方式：控件属性定位、图片匹配定位和比例坐标定位。

从定位的稳定性与可靠性来看，优先级如下：

- **首选：**控件属性定位（基于控件的属性信息精确定位）；
- **次选：**图片匹配定位（适用于属性不可用但界面稳定的场景）；
- **备用：**比例坐标定位（仅在前两种方式不可用时使用，受分辨率影响较大）。

控件属性定位通过BY选择器对象来实现。下文将详细介绍基于控件属性、图片匹配和比例坐标三种方式的控件定位方法。

**单属性定位控件**

从**hypium**包中导入BY选择器对象，从**hypium.model**包中导入匹配模式常量类**MatchPattern**。

1. **from** hypium **import** BY
2. **from** hypium.model **import** MatchPattern

通过BY对象描述需要查找或者操作的控件对象的属性，例如查找text属性为“蓝牙”的控件。

1. _# 查找text属性为"控件文本"的控件。_
2. component = driver.find_component(BY.text("蓝牙"))
3. _# 读取控件的的边框位置_。
4. bounds = component.getBounds()
5. _# 直接点击控件_。
6. component = driver.touch(BY.text("蓝牙"))

注意

默认情况下，find_component和touch等方法会查找/操作第一个条件匹配的控件，如需操作第n个满足匹配条件的控件，请参考查找所有匹配控件。

当前字符串类型的控件属性支持以下五种**模糊匹配**方式，通过BY选择器方法的第二个可选参数指定，如下表所示：

|序号|匹配方式常量|说明|
|:--|:--|:--|
|1|MatchPattern.STARTS_WITH|前缀匹配|
|2|MatchPattern.ENDS_WITH|后缀匹配|
|3|MatchPattern.CONTAINS|包含匹配|
|4|MatchPattern.REGEXP|正则表达式匹配|
|5|MatchPattern.REGEXP_ICASE|正则表达式匹配（忽略大小写）|

1. _# 点击text属性值前缀为“今天星期”的控件_。
2. driver.touch(BY.text("今天星期", MatchPattern.STARTS_WITH))

BY选择器支持的所有属性如下表所示：

|序号|属性名称|属性值类型|对应BY选择器|是否支持模糊匹配|
|:--|:--|:--|:--|:--|
|1|text|str|BY.text|是|
|2|key|str|BY.key|是|
|3|type|str|BY.type|是|
|4|checkable|bool|BY.checkable|否|
|5|longClickable|bool|BY.longClickable|否|
|6|clickable|bool|BY.clickable|否|
|7|scrollable|bool|BY.scrollable|否|
|8|enabled|bool|BY.enabled|否|
|9|focused|bool|BY.focused|否|
|10|selected|bool|BY.selected|否|
|11|checked|bool|BY.checked|否|
|12|hint|str|BY.hint|是|

**多属性组合定位控件**

BY选择器支持链式调用，允许用户指定多个控件属性进行联合定位。当界面上存在多个控件的部分属性相同而其他属性不同时，可通过组合条件精确匹配目标控件。

1. _# 点击文本为"蓝牙", 类型为"Button", 并且key为"bluetooth_switch"的按钮_。
2. driver.touch(BY.text("蓝牙").type("Button").key("bluetooth_switch"))

3. _#_ _查找__文本为"蓝牙", 类型为"Button", 并且key为"bluetooth_switch"的按钮_。
4. component = driver.find_component(BY.text("蓝牙").type("Button").key("bluetooth_switch"))

**控件相对位置+属性组合定位控件**

对于某些自身属性不唯一，无法精确定位的控件，BY选择器支持通过**与其他控件的相对位置关系**来定位控件。支持的相对定位方式如下表所示：

|序号|相对位置定位接口|功能描述|
|:--|:--|:--|
|1|BY.isBefore|匹配在指定控件前边的控件。|
|2|BY.isAfter|匹配在指定控件后边的控件。|
|3|BY.within|匹配在指定控件内部的控件。|
|4|BY.inWindow|匹配在指定窗口内部的控件。|

**注意：** 相对位置中的“前后”关系，对应控件树的前序遍历顺序（即深度优先遍历中根-子节点的访问次序），用户可以在 UiViewer 的可视化控件树中直观查看该顺序：控件在列表中从上到下的排列顺序，即为其在相对定位中的从前到后顺序。

相对位置通常和控件的属性结合使用来定位控件，以下图场景为例，界面上存在多个按钮，用户需要点击显示通知图标之后的按钮，定位方式如下：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201408.74308335030140886673359167955074:50001231000000:2800:72A4795AF7EF90E407969DD7513A4B2BE773FD194F17599B3FDC296E994A7AE8.png "点击放大")

1. 首先选择一个可以通过属性唯一定位的锚点控件。例如**BY.text("显示通知图标")**
2. 然后找到需要操作的目标控件，选择该控件的一个不唯一属性，通常为type属性。例如**BY.type("Button")**
3. 使用相对位置接口来描述锚点控件和目标控件的位置关系，得到完整的控件选择器。例如**BY.type("Button").isAfter(BY.text****("显示通知图标"))**，注意到这里组合使用了type属性和isAfter相对位置接口。

**示例代码**

1. _# 查找在text属性为"显示通知图标"的控件之后的type属性为"Button"的控件_。
2. component = driver.find_component(BY.type("Button").isAfter(BY.text("显示通知图标")))

3. _# 查找在text属性为"账号"的控件之前的type属性为"Image"的控件_。
4. component = driver.find_component(BY.type("Image").isBefore(BY.text("账号")))

5. _# 查找在key为"nav_container"内部的类型为"Image"的控件_。
6. component = driver.find_component(BY.type("Image").within(BY.key("nav_container")))

7. _# 查找包名为"com.huawei.hmos.settings"的应用内部的text属性为"蓝牙"的控件_。
8. component = driver.find_component(BY.text("蓝牙").inWindow("com.huawei.hmos.settings"))

注意

相对位置中的锚点控件**不能**再使用相对位置描述，即**BY.isBefore**方法的参数中不能再出现**BY.isBefore**或者**BY.isAfter**等相对定位的方式。

**XPath方式查找匹配的控件**

BY.xpath匹配器支持通过XPath语法来查找控件。部分控件没有唯一定位的属性，同时通过相对定位的方式也无法准确定位，推荐使用XPath语法来进行更精确的控件定位。

注意

XPath不能和其他属性匹配一起使用，通过XPath查找控件相比单属性和多属性查找控件的效率会有所下降。

在如下场景中，用户需要找到红框标识的图标，然而该图标没有唯一定位的属性，推荐使用XPath语法描述该控件相对其他可定位控件的路径关系来定位该控件。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201408.87114670157546532655639138799276:50001231000000:2800:76C4310F1420319FAA7F70C9B9978D9E5F6527D5FA3B2A4AD582A8B2F108DAD7.png "点击放大")

该页面上，“可用 WLAN”是一个固定的可唯一定位的文本，用户可以首先通过XPath定位到该文本**//*[@text='可用 WLAN']**，然后定位到该文本控件所在的List控件**/ancestor::List**，然后从该List控件开始找到对应的Image控件**/ListItemGroup/ListItem[1]//Text/following::Image**。

**示例代码**

1. _# 查找上图中红框所示的图标，并点击_。
2. comp = driver.find_component(BY.xpath("//*[@text='可用 WLAN']/ancestor::List/ListItemGroup/ListItem[1]//Text/following::Image"))
3. comp.click()

在支持传入BY选择器的接口均可以使用XPath来定位控件。

1. _# 查找text属性为WLAN的控件_。
2. driver.find_component(BY.xpath("//*[@text='WLAN']"))
3. driver.find_all_components(BY.xpath("//*[@text='WLAN']"))
4. driver.wait_for_component(BY.xpath("//*[@text='WLAN']"))
5. _# 点击text属性为WLAN的控件_。
6. driver.touch(BY.xpath("//*[@text='WLAN']"))

**查找所有匹配控件**

默认情况下，**driver.find_component**接口和其他支持传入BY选择器的接口会查找第一个匹配的控件进行操作。对于需要操作特定次序的匹配控件或所有匹配控件的场景，用户可以使用**driver.find_all_components**接口。

以如下场景为例，界面上存在多个Button，用户需要点击第2个特定的Button或点击所有Button时，可以使用**driver.find_all_components**。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201408.86729051478302090546119141953826:50001231000000:2800:24FABD56F6D57916B7ECCB626E019D2E5DAE5337650E99C1DBF5B027EB6F7C72.png "点击放大")

**示例代码**

1. _# 查找所有type属性为"Button"的控件, 如果有匹配的结果，components为列表，包含多个满足条件的IUiComponent对象_。
2. components = driver.find_all_components(BY.type("Button"))
3. _# 点击所有的控件_。
4. for component in components:
5.     driver.touch(component)
6. _# 点击第2个控件_。
7. driver.touch(component[1])

**图片定位控件**

如果控件没有可用于定位的唯一属性，通过相对位置也无法实现定位，可以通过截取控件的图片，使用**driver.find_image**查找控件的位置，或使用**driver.touch_image**直接点击控件。

以如下场景为例，若红框中的控件没有可以唯一定位的属性，也无法通过与附近控件的相对位置定位，用户可以尝试使用图片匹配的方式定位控件，定位方式如下：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201408.69235588012243055245127453106618:50001231000000:2800:AFF03D90691D6E906919D22757B7A26D32DCB02F40BA0F96F0EFC90140C5C017.png "点击放大")

1. 截取红框中图片保存到为template.jpeg（文件名根据需要定义）。
2. 调用driver.touch_image，传入template.jpeg图片的路径。

注意

使用图片定位控件需要安装opencv-python包，使用如下命令安装：

python -m pip install opencv-python

**示例代码**

1. _# 点击屏幕上和模板图片template.jpeg匹配的位置_。
2. driver.touch_image("/path/to/template.jpeg")

3. _# 查找屏幕上和模板图片template.jpeg匹配的位置, bounds为Rect类型，记录了控件上下左右边框的位置_。
4. bounds = driver.find_image("template.jpeg")
5. print(bounds.top, bounds.left, bounds.bottom, bounds.right)

注意

当前仅支持查找匹配度最高的匹配的图片区域，不支持匹配多个目标。

**比例坐标定位控件**

如果图像特征不明显，使用图像匹配的方式也无法准确识别控件位置，用户可以通过比例坐标的方式点击控件。使用坐标的方式操作控件存在以下两个问题：

1. 在屏幕比例或者控件位置发生变化时该方法可能无法操作到预期的控件。

2. 当实际操作界面非预期页面时，点击也会成功，但实际执行效果不符合预期。

因此，在使用该方法时，建议用户在前一步或者后一步操作中通过控件属性定位控件，避免脚本未按照预期方式操作设备，但用例仍然可以执行通过的问题。

以下图场景为例，如果红框中的控件无法通过上述方式定位，用户可以采用比例坐标的方式点击。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201409.01225936332239277106195767465828:50001231000000:2800:84AF32661F4A4EE1D4A41A45F0C8042F6FADBCCDF115E255B813E11DA9726F53.png "点击放大")

用户可以通过 UiViewer 工具的控件查看模式获取控件的比例坐标。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251120201409.86674549890317762468531699716913:50001231000000:2800:A8C0C341EDA6DA3B06E447B98E1C064FEA3236CF631F096C00CDBA614C99C4BB.png)

1. _# 点击屏幕上(0.52 * 屏幕宽度, 0.98 * 屏幕高度)的位置_。
2. driver.touch((0.52, 0.98))

- **窗口查找**

**查找窗口**

1. def find_window(filter: WindowFilter) -> UiWindow

**接口说明**

根据指定条件查找窗口，返回窗口对象。

**参数说明**

|参数名称|参数描述|
|:--|:--|
|filter|使用WindowFilter对象指定的窗口查找条件|

**返回值**

如果找到window则返回UiWindow对象，否则返回None。

**使用示例**

1. _# 查找标题为日历的窗口_。
2. window = driver.find_window(WindowFilter().title("日历"))
3. _# 查找包名为com.huawei.hmos.calendar，并且处于活动状态的窗口_。
4. window = driver.find_window(WindowFilter().bundle_name("com.huawei.hmos.calendar").actived(True))
5. _# 查找处于活动状态的窗口_。
6. window = driver.find_window(WindowFilter().actived(True))
7. _# 查找聚焦状态的窗口_。
8. window = driver.find_window(WindowFilter().focused(True))

- **界面操作**

**Ⅰ.触摸屏**

**点击**

1. **def touch**(target: **Union**[ISelector, IUiComponent, tuple], mode: str = UiParam.NORMAL, scroll_target: **Union**[ISelector, IUiComponent] = None, wait_time: float = 0.1)

**接口说明**

根据选定的控件或坐标位置执行点击操作。

**参数说明**

|序号|参数名称|参数描述|
|:--|:--|:--|
|1|target|需要点击的目标，支持三种类型：<br><br>1. BY控件选择器<br><br>2. 控件对象<br><br>2. 屏幕坐标（通过tuple类型指定，例如(100, 200)， 其中100为x轴坐标，200为y轴坐标。）|
|2|mode|点击模式，支持三种模式：<br><br>UiParam.NORMAL 点击<br><br>UiParam.LONG 长按（长按后放开）<br><br>UiParam.DOUBLE 双击。|
|3|scroll_target|指定可滚动的控件，在该控件中滚动搜索指定的目标控件target，仅在target为BY选择器时有效。|
|4|wait_time|点击后等待响应的时间，单位为秒，默认0.1秒。|

**使用示例**

1. _# 点击文本为"hello"的控件_。
2. driver.touch(BY.text("hello"))
3. _# 点击(100, 200)的位置_。
4. driver.touch((100, 200))
5. _# 点击比例坐标为(0.8, 0.9)的位置_。
6. driver.touch((0.8, 0.9))
7. _# 双击确认按钮(控件文本为"确认", 类型为"Button")_。
8. driver.touch(BY.text("确认").type("Button"), mode=UiParam.DOUBLE)
9. _# 在类型为Scroll的控件上滑动查找文本为"退出"的控件并点击_。
10. driver.touch(BY.text("退出"), scroll_target=BY.type("Scroll"))
11. _# 长按比例坐标为(0.8, 0.9)的位置_。
12. driver.touch((0.8, 0.9), mode="long")

**长按**

1. def long_click(self, target: Union[ISelector, IUiComponent, tuple], press_time: float = 2, offset=None):

**接口说明**

执行长按操作。

**注意：**该接口仅DevEco Testing Hypium 6.0.5.200以及更新的版本支持。

**参数说明**

|序号|参数名称|参数描述|
|:--|:--|:--|
|1|target|需要点击的目标，可以为控件查找条件，控件对象或者屏幕坐标(通过tuple类型指定，例如(100, 200)， 其中100为x轴坐标，200为y轴坐标。）|
|2|press_time|长按时间，单位为秒。|
|3|offset|点击坐标在目标控件区域的偏移值。不设置时该参数时默认为(0.5, 0.5), 表示控件中心。支持设置范围是0到1，如(0.1, 0.1)表示点击目标左上角为坐标原点x方向10%，y方向10%的位置。|

**使用示例**

1. _#_ _长按文本为"按钮"的控件5秒_
2. driver.long_click(BY.text("按钮"), press_time=5)
3. _#_ _长按(100, 200)的位置5秒_
4. driver.long_click((100, 200), press_time=5)
5. _#_ _长按文本为"设置"的控件左上角(偏移0, 0)_
6. driver.long_click(BY.text("设置"), offset=(0, 0))

**多指点击**

1. def **multi_finger_touch**(points: **List**[tuple], duration: float = 0.1, area: Rect = None)

**接口说明**

执行多指点击操作。

**参数说明**

|序号|参数名称|参数描述|
|:--|:--|:--|
|1|points|需要点击的坐标位置列表，每个坐标对应一个手指，例如[(0.1, 0.2), (0.3, 0.4)]，最多支持4指点击。|
|2|duration|按下/抬起的时间，可实现多指长按操作，单位秒。|
|3|area|点击操作的区域，当起始结束坐标为(0.1, 0.2)等相对比例坐标时生效，默认为操作区域为全屏。|

**使用示例**

1. _# 执行多指点击操作, 同时点击屏幕(0.1, 0.2), (0.3, 0.4)的位置。_
2. driver.multi_finger_touch([(0.1, 0.2), (0.3, 0.4)])
3. _# 执行多指点击操作, 设置点击按下时间为1秒。_
4. driver.multi_finger_touch([(0.1, 0.2), (0.3, 0.4)], duration=2)
5. _# 查找Image类型控件。_
6. comp = driver.find_component(BY.type("Image"))
7. _# 在指定的控件区域内执行多指点击(点击坐标为控件区域内的比例坐标)。_
8. driver.multi_finger_touch([(0.5, 0.5), (0.6, 0.6)], area=comp.getBounds())

**滑动**

**执行指定方向的滑动操作**

1. **def swipe**(direction: str, distance: int = 60, area: **Union**[ISelector, IUiComponent] = None, side: str = None, start_point: tuple = None, swipe_time: float = 0.3)

**接口说明**

在屏幕上或者指定区域中执行朝向指定方向的滑动操作。该接口用于无需指定精确起始和结束坐标的滑动操作场景。

**参数说明**

|序号|参数名称|参数描述|
|:--|:--|:--|
|1|direction|滑动方向，目前支持：<br><br>UiParam.LEFT 左滑<br><br>UiParam.RIGHT 右滑<br><br>UiParam.UP 上滑<br><br>UiParam.DOWN 下滑|
|2|distance|相对滑动区域总长度的滑动距离，范围为1-100，表示滑动长度为滑动区域总长度的1%到100%， 默认为60。|
|3|area|通过控件指定的滑动区域，默认为None表示滑动区域为整个屏幕。|
|4|side|滑动位置， 指定滑动区域内部（屏幕内部）执行操作的大概位置，支持：<br><br>UiParam.LEFT 靠左区域<br><br>UiParam.RIGHT 靠右区域<br><br>UiParam.TOP 靠上区域<br><br>UiParam.BOTTOM 靠下区域|
|5|start_point|滑动起始点，默认为None，表示在区域中间位置执行滑动操作，可以传入滑动起始点坐标，支持使用比例坐标，例如(0.5, 0.5)。<br><br>当同时传入side和start_point的时候，仅start_point生效。|
|6|swipe_time|滑动时间，单位为秒， 默认0.3秒。|

**使用示例**

1. _# 在屏幕上向上滑动, 距离40_。
2. driver.swipe(UiParam.UP, distance=40)
3. _# 在屏幕上向右滑动, 滑动时间为0.1秒_。
4. driver.swipe(UiParam.RIGHT, swipe_time=0.1)
5. _# 在屏幕起始点为比例坐标为(0.8, 0.8)的位置向上滑动，距离30_。
6. driver.swipe(UiParam.UP, 30, start_point=(0.8, 0.8))
7. _# 在屏幕左边区域向下滑动， 距离3_0。
8. driver.swipe(UiParam.DOWN, 30, side=UiParam.LEFT)
9. _# 在屏幕右侧区域向上滑动，距离30_。
10. driver.swipe(UiParam.UP, side=UiParam.RIGHT)
11. _# 在类型为Scroll的控件中向上滑动_。
12. driver.swipe(UiParam.UP, area=BY.type("Scroll"))

**执行指定起始结束位置的精确滑动操作**

1. **def slide**(start: **U****nion**[ISelector, tuple], end: **Union**[ISelector, tuple], area: **Union**[ISelector, IUiComponent] = None, slide_time: float = 0.3)

**接口说明**

根据指定的起始和结束位置执行滑动操作，起始和结束的位置可以为控件或屏幕坐标。该接口用于执行精准的滑动操作。

**参数说明**

|序号|参数名称|参数描述|
|:--|:--|:--|
|1|start|滑动起始位置，支持三种类型：<br><br>1. BY控件选择器<br><br>2. 控件对象<br><br>3. 屏幕坐标（通过tuple类型指定，例如(100, 200)， 其中100为x轴坐标，200为y轴坐标。）|
|2|end|滑动结束位置，支持三种类型：<br><br>1. BY控件选择器<br><br>2. 控件对象<br><br>3. 屏幕坐标（通过tuple类型指定，例如(100, 200)， 其中100为x轴坐标，200为y轴坐标。）|
|3|area|滑动操作区域。指定区域后，当start或end参数为坐标类型时，其坐标被视为相对于该指定的区域的相对位置坐标。|
|4|slide_time|滑动时间，单位为秒，默认为0.3秒。|

**使用示例**

1. _# 从类型为Slider的控件滑动到文本为最大的控件_
2. driver.slide(BY.type("Slider"), BY.text("最大"))
3. _# 从坐标100, 200滑动到300，400_
4. driver.slide((100, 200), (300, 400))
5. _# 从坐标100, 200滑动到300，400, 滑动时间为3秒_
6. driver.slide((100, 200), (300, 400), slide_time=3)
7. # _在类型为Slider的控件上从(0, 0)滑动到(100, 0)_
8. driver.slide((0, 0), (100, 0), area = BY.type("Slider"))

**拖拽**

1. **def drag**(start: **Union**[ISelector, tuple, IUiComponent], end: Union[ISelector, tuple, IUiComponent], area: Union[ISelector, IUiComponent] = None, press_time: float = 1, drag_time: float = 1)

**接口说明**

根据指定的起始和结束位置执行拖拽操作，起始和结束的位置可以为控件或者屏幕坐标。

**参数说明**

|序号|参数名称|参数描述|
|:--|:--|:--|
|1|start|拖拽起始位置，支持三种类型：<br><br>1. BY控件选择器<br><br>2. 控件对象<br><br>3. 屏幕坐标（通过tuple类型指定的坐标，例如(100, 200)， 其中100为x轴坐标，200为y轴坐标；或相对于区域长度和宽度的比例坐标，例如(0.1, 0.2)。)|
|2|end|拖拽结束位置，支持三种类型：<br><br>1. BY控件选择器<br><br>2. 控件对象<br><br>3. 屏幕坐标（通过tuple类型指定的坐标，例如(100, 200)， 其中100为x轴坐标，200为y轴坐标；或相对于区域长度和宽度的比例坐标，例如(0.1, 0.2)。)|
|3|area|拖拽操作区域，指定区域后，当start或end参数为坐标类型时，其坐标被视为相对于该指定的区域的相对位置坐标。|
|4|press_time|拖拽操作开始时，长按的时间，单位为秒，默认为1.5秒。<br><br>**注意：** 该参数为可选参数，仅DevEco Testing Hypium 6.0.5.200及更新的版本，且配套测试设备的API level >= 20时支持。|
|5|drag_time|拖动的时间，单位秒， 默认为1秒（拖拽操作总时间 = press_time + drag_time）。|

**使用示例**

1. _#_ _拖拽文本为"文件.txt"的控件到文本为"上传文件"的控件_。
2. driver.drag(BY.text("文件.txt"), BY.text("上传文件"))
3. _#_ _拖拽id为"start_bar"的控件到坐标(100, 200)的位置, 拖拽时间为2秒_。
4. driver.drag(BY.key("start_bar"), (100, 200), drag_time=2)
5. _#_ _在id为"Canvas"的控件上执行拖拽操作，从"Canvas"控件中(0.1, 0.5)的位置拖拽到(0.9, 0.5)位置。_
6. _# 假如"Canvas"控件左上角坐标(100, 100), 宽度为200，高度为50，此操作等价于_
7. _# driver.drag((100 + 0.1 * 200, 100 + 0.5 * 50), (100 + 0.9 * 200, 100 + 0.5 * 50))_。
8. driver.drag((0.1, 0.5), (0.9, 0.5), area=BY.id("Canvas"))
9. _#_ _在滑动条上执行拖拽操作, 以滑动条组件左上角为原点, 从滑动条区域中的(10, 10)拖拽到(10, 200)。_
10. _# 假设滑动条左上角坐标为(500, 500), 此操作等价于driver.drag((500 + 10, 500 + 10), (500 + 10, 500 + 200))。_
11. driver.drag((10, 10), (10, 200), area=BY.type("Slider"))

**捏合缩小**

1. **def pinch_in**(area: **Union**[ISelector, IUiComponent, Rect], scale: float = 0.4, direction: str = "diagonal", **kwargs)

**接口说明**

在指定控件上执行双指捏合缩小操作。

**参数说明**

|序号|参数名称|参数描述|
|:--|:--|:--|
|1|area|手势操作执行的区域，支持三种类型：<br><br>1. BY控件选择器<br><br>2. 控件对象<br><br>3. 屏幕区域，通过Rect类型指定，例如 Rect(left, right, top, bottom)，其中 left，right，top，bottom 为区域左右上下的坐标值。|
|2|scale|缩放的比例，范围(0, 1)，值越小表示缩放操作距离越长，缩小的越多。|
|3|direction|双指缩放时缩放操作方向，当前支持：<br><br>"diagonal" 对角线滑动<br><br>"horizontal" 水平滑动|
|4|kwargs|其他可选滑动配置参数：<br><br>dead_zone_ratio 缩放操作时控件靠近边界不可操作的区域占控件长度/宽度的比例，默认为0.2，调节范围为(0, 0.5)。|

**使用示例**

1. _# 在类型为Image的控件上进行双指捏合缩小操作_。
2. driver.pinch_in(BY.type("Image"))
3. _# 在类型为Image的控件上进行双指捏合缩小操作, 设置水平方向捏合_。
4. driver.pinch_in(BY.type("Image"), direction="horizontal")

**双指放大**

1. **def pinch_out**(area: **Union**[ISelector, IUiComponent, Rect], scale: float = 1.6, direction: str = "diagonal", **kwargs)

**接口说明**

在指定控件上执行双指放大操作。

**参数说明**

|序号|参数名称|参数描述|
|:--|:--|:--|
|1|area|手势操作执行的区域，支持三种类型：<br><br>1. BY控件选择器<br><br>2. 控件对象<br><br>2. 屏幕区域，通过Rect类型指定，例如 Rect(left, right，top, bottom)，其中 left，right，top，bottom 为区域左右上下的坐标值。|
|2|scale|缩放的比例，范围 (1, 2)，值越大表示缩放操作滑动的距离越长。|
|3|direction|双指缩放时缩放操作方向，当前支持：<br><br>"diagonal" 对角线滑动<br><br>"horizontal" 水平滑动|
|4|kwargs|其他可选滑动配置参数：<br><br>dead_zone_ratio 缩放操作时控件靠近边界不可操作的区域占控件长度/宽度的比例，默认为0.2，调节范围为(0, 0.5)。|

**使用示例**

1. _# 在类型为Image的控件上进行双指放大操作_。
2. driver.pinch_out(BY.type("Image"))
3. _# 在类型为Image的控件上进行双指捏合缩小操作, 设置水平方向捏合_。
4. driver.pinch_out(BY.type("Image"), direction="horizontal")

**双指滑动**

1. def two_finger_swipe(start1: tuple, end1: tuple, start2: tuple, end2: tuple, duration: float = 0.5, area: Rect = None)

**接口说明**

执行双指滑动操作。

**参数说明**

|序号|参数名称|参数描述|
|:--|:--|:--|
|1|start1|手指1起始坐标|
|2|end1|手指1结束坐标|
|3|start2|手指2起始坐标|
|4|end2|手指2结束坐标|
|5|duration|滑动操作持续时间，单位为秒，默认0.5秒。|
|6|area|滑动操作的区域，当起始结束坐标为(0.1, 0.2)等相对比例坐标时生效，默认为操作区域为全屏。|

**使用示例**

1. _# 执行双指滑动操作, 手指1从(0.4, 0.4)滑动到(0.2, 0.2), 手指2从(0.6, 0.6)滑动到(0.8, 0.8)。_
2. driver.two_finger_swipe((0.4, 0.4), (0.2, 0.2), (0.6, 0.6), (0.8, 0.8))
3. _# 执行双指滑动操作, 手指1从(0.4, 0.4)滑动到(0.2, 0.2), 手指2从(0.6, 0.6)滑动到(0.8, 0.8), 持续时间3秒。_
4. driver.two_finger_swipe((0.4, 0.4), (0.2, 0.2), (0.6, 0.6), (0.8, 0.8), duration=3)
5. _# 查找Image类型控件。_
6. comp = driver.find_component(BY.type("Image"))
7. _# 在指定的控件区域内执行双指滑动(滑动起始/停止坐标为控件区域内的比例坐标)。_
8. driver.two_finger_swipe((0.4, 0.4), (0.1, 0.1), (0.6, 0.6), (0.9, 0.9), area=comp.getBounds())

**自定路径滑动手势（单指）**

1. **def inject_gesture**(gesture: Gesture, speed: int = 2000)

**接口说明**

执行自定义滑动手势操作。

**参数说明**

|序列|参数名称|参数描述|
|:--|:--|:--|
|1|gesture|描述手势操作的Gesture对象。|
|2|speed|默认操作速度，单位像素/秒，默认值为2000像素/秒，当生成Gesture对象的步骤中未传入操作时间时默认使用该速度进行操作。|

**使用示例**

1. from hypium.uidriver import Gesture

2. _# 创建一个gesture对象_。
3. gesture = Gesture()
4. _# 获取控件计算器的位置_。
5. pos = driver.findComponent(BY.text("计算器")).getBoundsCenter()
6. # 获取屏幕尺寸。
7. size = driver.getDisplaySize()
8. _# 起始位置, 长按2秒_。
9. gesture.start(pos.to_tuple(), 2)
10. _# 移动到屏幕边缘_。
11. gesture.move_to(Point(size.X - 20, int(size.Y / 2)).to_tuple())
12. _# 停留2秒_。
13. gesture.pause(2)
14. _# 移动到(360, 500)的位置_。
15. gesture.move_to(Point(360, 500).to_tuple())
16. _# 停留2秒结束_。
17. gesture.pause(2)
18. _# 执行gesture对象描述的操作_。
19. driver.inject_gesture(gesture)

**自定路径滑动手势(多指)**

1. def inject_multi_finger_gesture(gestures: List[Gesture], speed: int = 6000)

**接口说明**

注入多指手势操作。

**参数说明**

|序号|参数名称|参数描述|
|:--|:--|:--|
|1|gestures|表示单指手势操作的Gesture对象列表，每个Gesture对象描述一个手指的操作轨迹，最多4指。<br><br>注意如果各个手势持续时间不同，时间短的手势操作会保持在结束位置，等待所有手势完成后抬起对应手指。|
|2|speed|Gesture对象的步骤未设置时间时，使用该速度计算时间，单位为像素/秒，默认为6000像素/秒。|

**使用示例**

1. from hypium.uidriver import Gesture
2. _# 创建手指1的手势, 从(0.4, 0.4)的位置移动到(0.2, 0.2)的位置。_
3. gesture1 = Gesture().start((0.4, 0.4)).move_to((0.2, 0.2), interval=1)
4. _# 创建手指2的手势, 从(0.6, 0.6)的位置移动到(0.8, 0.8)的位置。_
5. gesture2 = Gesture().start((0.6, 0.6)).move_to((0.8, 0.8), interval=1)
6. _# 注入多指操作。_
7. driver.inject_multi_finger_gesture((gesture1, gesture2))

**Ⅱ. 键盘鼠标**

**鼠标点击**

1. **def mouse_click**(pos: **Union**[tuple, IUiComponent, ISelector], button_id: MouseButton = MouseButton.MOUSE_BUTTON_LEFT, key1: Union[KeyCode, int] = None, key2: **Union**[KeyCode, int] = None)

**接口说明**

执行鼠标点击操作, 支持键鼠组合操作。

**参数说明**

|序号|参数名称|参数描述|
|:--|:--|:--|
|1|pos|点击的位置，支持三种类型：<br><br>1. BY控件选择器<br><br>2. 控件对象<br><br>3. 屏幕坐标（通过tuple类型指定，例如(100, 200)， 其中100为x轴坐标，200为y轴坐标。)|
|2|button_id|需要点击的鼠标按键。|
|3|key1|需要组合按下的第一个键盘按键。|
|4|key2|需要组合按下的第二个键盘按键。|

**使用示例**

1. _# 使用鼠标左键点击(100, 200)的位置_。
2. driver.mouse_click((100, 200), MouseButton.MOUSE_BUTTON_LEFT)
3. _# 使用鼠标右键点击文本为"确认"的控件_。
4. driver.mouse_click(BY.text("确认"), MouseButton.MOUSE_BUTTON_RIGHT)
5. _# 使用鼠标右键点击比例坐标(0.8, 0.5)的位置_。
6. driver.mouse_click((0.8, 0.5), MouseButton.MOUSE_BUTTON_RIGHT)

**鼠标拖拽**

1. **def mouse_drag**(start: **Union**[tuple, IUiComponent, ISelector], end: **Union**[tuple, IUiComponent, ISelector], speed: int = 3000)

**接口说明**

执行鼠标拖拽操作（即按住鼠标左键并移动鼠标）。

**参数说明**

|序号|参数名称|参数描述|
|:--|:--|:--|
|1|start|起始位置，支持三种类型：<br><br>1. BY控件选择器<br><br>2. 控件对象<br><br>3. 屏幕坐标（通过tuple类型指定，例如(100, 200)， 其中100为x轴坐标，200为y轴坐标。)|
|2|end|结束位置，支持三种类型：<br><br>1. BY控件选择器<br><br>2. 控件对象<br><br>3. 屏幕坐标（通过tuple类型指定，例如(100, 200)， 其中100为x轴坐标，200为y轴坐标。)|
|3|speed|鼠标移动速度，像素/秒，默认3000像素/秒。|

**使用示例**

1. _# 鼠标从控件1拖拽到控件2_。
2. driver.mouse_drag(BY.text("控件1"), BY.text("控件2"))

**鼠标移动**

1. **def mouse_move**(start: **Union**[tuple, IUiComponent, ISelector], end: **Union**[tuple, IUiComponent, ISelector], speed: int = 3000)

**接口说明**

将鼠标指针从指定起始位置移动到结束位置，模拟移动轨迹和移动速度。

**参数说明**

|序号|参数名称|参数描述|
|:--|:--|:--|
|1|start|起始位置，支持三种类型：<br><br>1. BY控件选择器<br><br>2. 控件对象<br><br>3. 屏幕坐标（通过tuple类型指定，例如(100, 200)， 其中100为x轴坐标，200为y轴坐标。）|
|2|end|结束位置，支持三种类型：<br><br>1. BY控件选择器<br><br>2. 控件对象<br><br>3. 屏幕坐标（通过tuple类型指定，例如(100, 200)， 其中100为x轴坐标，200为y轴坐标。）|
|3|speed|鼠标移动速度，像素/秒，默认3000像素/秒。|

**使用示例**

1. _# 鼠标从控件1移动到控件2_。
2. driver.mouse_move(BY.text("控件1"), BY.text("控件2"))

**按键**

1. **def press_key**(key_code: **Union**[KeyCode, int], key_code2: **Union**[KeyCode, int] = None, mode="normal")

**接口说明**

执行按键操作（注意不推荐使用该接口实现组合按键模拟，模拟组合按键键请使用press_combination_key）。

**参数说明**

|序号|参数名称|参数描述|
|:--|:--|:--|
|1|key_code|需要按下的按键编码。|
|2|key_code2|需要按下的按键编码。|
|3|mode|按键模式，仅在进行单个按键时支持，当前支持以下模式：<br><br>UiParam.NORMAL 单击<br><br>UiParam.LONG 长按<br><br>UiParam.DOUBLE 双击|

**使用示例**

1. _# 按下电源键_。
2. driver.press_key(KeyCode.POWER)
3. _# 长按电源键_。
4. driver.press_key(KeyCode.POWER, mode=UiParam.LONG)
5. _# 按下音量下键_。
6. driver.press_key(KeyCode.VOLUME_DOWN)

**按组合键**

1. **def press_combination_key**(key1: **Union**[KeyCode, int], key2: **Union**[KeyCode, int], key3: **Union**[KeyCode, int] = None)

**接口说明**

执行组合键操作，支持2键或3键组合。

**参数说明**

|序号|参数名称|参数描述|
|:--|:--|:--|
|1|key1|组合键第一个按键|
|2|key2|组合键第二个按键|
|3|key3|组合键第三个按键|

**使用示例**

1. _# 按下音量下键和电源键的组合键_
2. driver.press_combination_key(KeyCode.VOLUME_DOWN, KeyCode.POWER)
3. # _同时按下ctrl, shift和F键_
4. driver.press_combination_key(KeyCode.CTRL_LEFT, KeyCode.SHIFT_LEFT, KeyCode.F)

- **hdc/shell命令执行**

**hdc命令执行**

1. **def hdc**(cmd, timeout: float = 60) -> str

**接口说明**

执行hdc命令。

**参数说明**

|序号|参数名称|参数描述|
|:--|:--|:--|
|1|cmd|需要执行的hdc命令。|
|2|timeout|超时时间，单位秒，默认60秒。|

**返回值**

命令执行后的回显内容。

**使用示例**

1. _# 执行hdc命令list targets_。
2. echo = driver.hdc("list targets")
3. _# 执行hdc命令hilog, 设置30秒超时_。
4. echo = driver.hdc("hilog", timeout = 30)

**设备侧shell命令执行**

1. **def shell**(cmd: str, timeout: float = 60) -> str

**接口说明**

在设备端shell中执行命令。

**参数说明**

|序号|参数名称|参数描述|
|:--|:--|:--|
|1|cmd|需要执行的shell命令。|
|2|timeout|超时时间，单位秒，默认60秒。|

**返回值**

命令执行后的回显内容。

**使用示例**

1. _# 在设备shell中执行命令ls -l。_
2. echo = driver.shell("ls -l")
3. _# 在设备shell中执行命令top, 设置10秒超时时间。_
4. echo = driver.shell("top", timeout=10)

**PC侧shell命令执行**

1. **def shell**(cmd: **Union**[str, list], timeout: float = 300) -> str

**接口说明**

在PC端执行shell命令。

**参数说明**

|序号|参数名称|参数描述|
|:--|:--|:--|
|1|cmd|需要执行的命令内容。|
|2|timeout|超时时间，单位秒，默认300秒。|

**使用示例**

1. _# 在PC端执行dir命令_。
2. echo = host.shell("dir")
3. _# 在PC端执行netstat命令读取回显结果, 设置超时时间为10秒_。
4. echo = host.shell("netstat", timeout=10)

- **应用预置操作**

**安装应用**

1. **def install_app**(package_path: str, options: str = "", **kwargs)

**接口说明**

安装指定应用安装包。

**参数说明**

|序号|参数名称|参数描述|
|:--|:--|:--|
|1|package_path|PC端保存的安装包路径。|
|2|options|传递给bm install命令的额外参数。|

**使用示例**

1. _# 安装路径为test.hap的安装包到手机_。
2. driver.install_app(r"test.hap")
3. _# 替换安装路径为test.hap的安装包到手机(增加-r参数指定替换安装)_。
4. driver.install_app(r"test.hap", "-r")

**卸载应用**

1. **def uninstall_app**(package_name: str, **kwargs)

**接口说明**

卸载指定包名应用。

**参数说明**

|参数名称|参数描述|
|:--|:--|
|package_name|需要卸载的应用包名|

**使用示例**

1. _# 卸载包名为com.test.myapp的应用_。
2. **driver.uninstall_app**("com.test.myapp")

**清除应用缓存数据**

1. **def clear_app_data**(package_name: str)

**接口说明**

清除应用的缓存数据。

**参数说明**

|参数名称|参数描述|
|:--|:--|
|package_name|需要清除缓存的应用包名（bundle name）|

**使用示例**

1. _# 清除包名为com.test.myapp的应用的缓存数据_。
2. driver.clear_app_data("com.test.myapp")

**启动应用**

1. def **start_app**(package_name: str, page_name: str = None, params: str = "", wait_time: float = 1)

**接口说明**

根据包名启动指定的应用。

**参数说明**

|序号|参数名称|参数描述|
|:--|:--|:--|
|1|package_name|应用程序包名(bundle name)。|
|2|page_name|应用内页面名称(ability name)。|
|3|params|其他传递给aa命令的参数。|
|4|wait_time|发送启动指令后，等待应用启动的时间，单位为秒，默认为1秒。|

**使用示例**

1. _# 启动浏览器_。
2. driver.start_app("com.huawei.hmos.browser", "MainAbility")

**停止应用**

1. **def stop_app**(package_name: str, wait_time: float = 0.5)

**接口说明**

停止指定包名的应用。

**参数说明**

|序号|参数名称|参数描述|
|:--|:--|:--|
|1|package_name|应用程序包名。|
|2|wait_time|停止应用后等待的时间，单位为秒，默认为0.5秒。|

**使用示例**

1. _# 停止包名为com.huawei.hmos.settings_的应用。
2. driver.stop_app("com.huawei.hmos.settings")

- **文件拉取/推送**

**拉取文件**

1. **def pull_file**(device_path: str, local_path: str = None, timeout: int = 60)

**接口说明**

从设备端的传输文件到PC端。

**参数说明**

|序号|参数名称|参数描述|
|:--|:--|:--|
|1|device_path|设备侧保存文件的路径。|
|2|local_path|PC侧保存文件的路径。|
|3|timeout|拉取文件超时时间，单位秒，默认60秒。|

**使用示例**

1. _# 从设备中拉取文件"/data/local/tmp/test.log"保存到PC端的test.log_。
2. driver.pull_file("/data/local/tmp/test.log", "test.log")

**推送文件**

1. **def push_file**(local_path: str, device_path: str, timeout: int = 60)

**接口说明**

从PC端传输文件到设备端。

**参数说明**

|序号|参数名称|参数描述|
|:--|:--|:--|
|1|local_path|PC侧文件的路径。|
|2|device_path|设备侧文件的路径。|
|3|timeout|推送文件超时时间，单位秒，默认60秒。|

**使用示例**

1. _# 从PC端推送文件test.hap保存到设备端的"/data/local/tmp/test.hap"_。
2. driver.push_file("test.hap", "/data/local/tmp/test.hap")

**查询文件是否存在**

1. **def has_file**(file_path: str) -> bool

**接口说明**

查询设备中是否有存在路径为file_path的文件。

**参数说明**

|参数名称|参数描述|
|:--|:--|
|file_path|需要检查的设备端文件路径。|

**使用示例**

1. _# 查询设备端是否存在文件/data/local/tmp/test_file.txt_。
2. driver.has_file("/data/local/tmp/test_file.txt")

- **文本输入/清除**

**输入文本**

1. def input_text(component: Union[ISelector, IUiComponent, tuple], text: str, mode: InputTextMode = None):

**接口说明**

向指定控件中输入文本内容。

**参数说明**

|序号|参数名称|参数描述|
|:--|:--|:--|
|1|component|需要输入文本的控件，支持三种类型：<br><br>1. BY控件选择器<br><br>2. 控件对象<br><br>3. 屏幕坐标（通过tuple类型指定，例如(100, 200)， 其中100为x轴坐标，200为y轴坐标。）|
|2|text|需要输入的文本。|
|3.|mode|输入模式配置，默认模式操作如下：<br><br>1. 默认清空指定的控件中的文本后再执行输入。<br><br>2. 英文字符长度<200时，逐个输入，超过200时，通过剪切板粘贴一次输入。<br><br>3. 中文文本通过剪切板粘贴一次输入。<br><br>通过该参数可以配置：<br><br>1. 追加输入：InputTextMode().addition(True)。<br><br>2. 输入英文时，不考虑文本长度直接使用剪切板快速输入：InputTextMode().paste(True)。<br><br>**注意**：该参数为可选参数，仅DevEco Testing Hypium 6.0.5.200以及更新的版本，且配套测试设备的API level >= 20支持。|

使用示例

1. from hypium import BY
2. from hypium.model import InputTextMode
3. _#_ _在类型为"TextInput"的控件中输入文本"hello world"。_
4. driver.input_text(BY.type("TextInput"), "hello world")
5. _#_ _在类型为"TextInput"的控件中使用剪切板一次性输入文本"hello world"。_
6. driver.input_text(BY.type("TextInput"), "hello world", mode=InputTextMode().paste(True))
7. _#_ _在类型为"TextInput"的控件中使用剪切板一次性并追加输入文本"hello world"。_
8. driver.input_text(BY.type("TextInput"), "hello world", mode=InputTextMode().paste(True).addition(True))

**清除文本**

1. **def clear_text**(component: [ISelector, IUiComponent])

**接口说明**

清空指定控件中的文本内容。

**参数说明**

|参数名称|参数描述|
|:--|:--|
|component|需要清除文本的控件|

使用示例

1. _# 清除类型为"InputText"的控件中的内容_。
2. driver.clear_text(BY.type("InputText"))

- **断言**

**Ⅰ. 常规断言**

**检查是否相等**

1. **def check_equal**(value: **Any**, expect: **Any** = True, fail_msg: str = None, expect_equal=True)

**接口说明**

检查实际值和期望值相等，在不一致时抛出异常，并打印fail_msg。

**参数说明**

|序号|参数名称|参数描述|
|:--|:--|:--|
|1|value|实际值，如果为list或者tuple，将取其中每个值同expect中的每个值进行比较。|
|2|expect|期望值， 如果为list或者tuple，将取其中每个值同value中的每个值进行比较。|
|3|fail_msg|断言失败时打印的提示信息。|

**使用示例**

1. _# 检查a等于b_。
2. host.check_equal(a, b, "a != b")

**检查是否超过预期值**

1. **def check_greater**(value: **Any**, expect: **Any**, fail_msg: str = None)

**接口说明**

检查value是否大于expect，不满足时抛出异常，并在日志中打印fail_msg。

**参数说明**

|序号|参数名称|参数描述|
|:--|:--|:--|
|1|value|实际值|
|2|expect|期望值|
|3|fail_msg|断言失败时打印的提示信息|

**使用示例**

1. _# 检查a大于b_
2. host.check_greater(a, b)

**Ⅱ. 控件断言**

**检查控件是否存在**

1. **d****ef check_component_exist**(component: ISelector, expect_exist: bool = True, wait_time: int = 0, scroll_target: **Union**[ISelector, IUiComponent] = None)

**接口说明**

检查指定控件在当前界面是否存在。

**参数说明**

|序号|参数名称|参数描述|
|:--|:--|:--|
|1|component|待检查的UI控件，使用BY选择器指定。|
|2|expect_exist|是否期望控件存在，True表示期望控件存在，False表示期望控件不存在。|
|3|wait_time|检查过程中等待控件出现的时间，单位秒，默认为0。|
|4|scroll_target|需要上下滚动检查目标控件时滑动的控件，默认为None，表示不进行滑动查找。|

**使用示例**

1. _# 检查类型为Button的控件存在_。
2. driver.check_component_exist(BY.type("Button"))
3. _# 检查类型为Button的控件存在，如果不存在等待最多5秒_。
4. driver.check_component_exist(BY.type("Button"), wait_time=5)
5. _# 在类型为Scroll的控件上滚动检查文本为"hello"的控件存在_。
6. driver.check_component_exist(BY.text("hello"), scroll_target=BY.type("Scroll"))
7. _# 检查文本为确认的控件不存在_。
8. driver.check_component_exist(BY.text("确认"), expect_exist=False)

**检查控件属性**

1. **def check_component**(component: **Union**[ISelector, IUiComponent], expected_equal: bool = True, **kwargs)

**接口说明**

检查当前界面上指定控件的属性是否符合预期。

**参数说明**

|序号|参数名称|参数描述|
|:--|:--|:--|
|1|component|需要检查的控件，支持BY选择器或控件对象。|
|2|expected_equal|预期值和实际值是否相等，True表示预期相等，False表示预期不相等。|
|3|kwargs|指定预期的控件属性值，目前支持：<br><br>"id"，"text"，"key"，"type"，"enabled"，"focused"，"clickable"，"scrollable"<br><br>"checked"，"checkable"。|

**使用示例**

1. _# 检查id为xxx的控件的checked属性为True_。
2. driver.check_component(BY.key("xxx"), checked=True)
3. _# 检查id为check_button的按钮enabled属性为True_。
4. driver.check_component(BY.key("checked_button"), enabled=True)
5. _# 检查id为container的控件文本内容为“正在检查_”。
6. driver.check_component(BY.key("container"), text="正在检查")
7. _# 检查id为container的控件文本内容不为空_。
8. driver.check_component(BY.key("container"), text="", expect_equal=False)

**检查图片是否存在**

1. def check_image_exist(image_path_pc: str, expect_exist: bool = True, similarity: float = 0.95, timeout: int = 3, mode="template", **kwargs)

**接口说明**

使用图片模板匹配算法检测当前屏幕截图中是否有指定图片，需要保证模板图片的分辨率和屏幕截图中目标图像的分辨率一致。

**参数说明**

|序号|参数名称|参数描述|
|:--|:--|:--|
|1|image_path_pc|待检查的图片路径（图片保存在PC端）。|
|2|expect_exist|是否期望图片在设备屏幕上存在，True表示期望控件存在，False表示期望控件不存在。|
|3|similarity|图像匹配算法比较图片时使用的相似度，范围[0, 1]。|
|4|timeout|检查的总时间，每秒会进行获取一次屏幕截图检查指定图片是否存在，通过timeout可指定检查的次数。|
|5|mode|图片匹配模式，支持"template"和"sift"，图片分辨率/旋转变化对sift模式影响相对较小，但sift模式难以处理缺少较复杂图案的纯色，无线条图片。|
|6|kwargs|其他配置参数：<br><br>min_match_point： 最少匹配特征点数，值越大匹配越严格，默认为16，仅sift模式有效。|

**使用示例**

1. _# 检查图片存在。_
2. driver.check_image_exist("test.jpeg")
3. _# 检查图片不存在。_
4. driver.check_image_exist("test.jpeg", expect_exist=False)
5. _# 检查图片存在, 图片相似度要求95%, 重复检查时间5秒。_
6. driver.check_image_exist("test.jpeg", timeout=5, similarity=0.95)
7. _# 检查图片不存在, 重复检查时间5秒。_
8. driver.check_image_exist("test.jpeg", timeout=5, expect_exist=False)
9. _# 使用sift算法检查图片存在, 设置最少匹配特征点数量为16。_
10. driver.check_image_exist("test.jpeg", mode="sift", min_match_point=16)

**Ⅲ. 窗口断言**

**检查窗口**

1. **def check_window**(window: WindowFilter, title: str = None, bundle_name: str = None)

**接口说明**

检查指定的window的属性是否符合预期。

**参数说明**

|序号|参数名称|参数描述|
|:--|:--|:--|
|1|title|预期的窗口标题，None表示不检查。|
|2|bundle_name|预期窗口所属的应用包名，None表示不检查。|

**使用示例**

1. _# 检查当前焦点窗口的包名为com.huawei.hmos.settings_。
2. driver.check_window(WindowFilter().focused(True), bundle_name="com.huawei.hmos.settings")

- **日志打印**

用户使用以下方法可以在测试用例脚本中打印日志，日志会记录到测试报告中。

1. **from** devicetest.core.test_case **import** Step, CheckPoint, MESSAGE

2. Step("点击按钮")
3. CheckPoint("检查联系人存在")
4. MESSAGE("打印一条提示消息")

在自定义实现的接口中，可以调用driver对象中的log模块打印日志消息，对应日志也会记录到测试报告中。

1. driver.log.debug("debug级别的日志")
2. driver.log.info("info级别的日志")
3. driver.log.warning("warning级别的日志")
4. driver.log.error("error级别的日志")

- **读取测试项目中资源文件路径**

用户可通过以下接口读取测试工程资源目录中的文件路径。接口接收文件名或相对路径作为参数，搜索测试工程资源文件目录并返回文件的完整路径。若未找到对应文件，则抛出异常。

1. **from** devicetest.utils **import** file_util
2. file_path = file_util.get_resource_path("filename")

该接口默认搜索文件，开发者可以设置isdir=True来搜索目录路径。

1. dir_path = file_util.get_resource_path("dirname", isdir=True)

## 隐私协议

**概述**

DevEco Testing Hypium(以下简称Hypium)是由华为终端有限公司（以下简称“我们”或“华为”）提供的UI自动化测试框架。华为非常重视您的个人信息和隐私保护，我们将会按照法律要求和业界成熟的安全标准，为您的个人信息提供相应的安全保护措施。

**1** **我们如何收集和使用您的个人信息**

我们将通过Hypium为您提供下述业务功能，在您使用相关业务功能的过程中，我们会处理下列提供功能所必需的信息，以便履行我们的合同义务。若您不提供相关信息，会影响到您使用本应用的相关功能。

**运行Hypium**

在您使用Hypium的过程中，我们会收集执行设备的操作系统平台和版本号，用于更好的提供和执行平台适配的测试服务。

**测试鸿蒙设备**

当您使用Hypium测试鸿蒙设备上的应用时，我们会收集被测设备的型号以及鸿蒙系统版本、被测应用的名称或者包名、Hypium特性功能的触发时间和使用次数，用于分析Hypium各功能在不同平台上的使用情况，从而针对性的优化我们的产品，更好的为客户提供服务。

**2** **对未成年人的保护**

我们非常重视对未成年人个人信息的保护，华为将严格按照国家法律法规要求在未成年人使用服务时提供相应的保护。如果您是未成年人，需要您的父母或其他监护人同意您使用本应用并同意相关应用的服务条款。父母或其他监护人也应采取适当的预防措施来保护未成年人，包括监督其对本应用的使用。如您是儿童，请务必退出使用本应用。

**3** **管理您的个人信息**

华为非常尊重您对个人信息的关注，并为您提供了数据主体权利及选择。

**3.1** **信息访问**

如您希望收集和存储的您的个人信息及其副本，可通过本声明中“如何联系我们”章节中所述方式与我们取得联系，并获取您的个人信息及其副本。

**3.2** **信息更正**

当您需要更新您的个人信息，或发现我们处理您的个人信息有误时，您有权作出更正或更新。您可以通过本声明中“如何联系我们”章节中所述方式与我们取得联系，并修改您的个人信息。

**3.3** **信息删除**

您随时可以通过本声明中“如何联系我们”章节中所述方式与我们取得联系，并要求我们删除您的个人信息。

**3.4** **停用服务**

对于hypium-driver-js安装包，您可以在项目根目录运行 `npx hypium-driver telemetry disable` 来停止Hypium处理您的个人信息。

对于hypium安装包，您可以在项目根目录运行 `python -m hypium telemetry disable` 来停止Hypium处理您的个人信息。

对于hypium-pycharm-plugin的插件，您可以在pycharm顶部导航栏中的DevEco Testing Hypium > 隐私协议页面，点击“拒绝并关闭”按钮来停止Hypium处理您的个人信息。

对于hypium-driver-js安装包，您可以在项目根目录运行 `npx hypium-driver telemetry enable ` 来恢复Hypium对您个人信息的处理。

对于hypium安装包，您可以在项目根目录运行 ` python -m hypium telemetry enable` 来恢复Hypium对您个人信息的处理。

对于hypium-pycharm-plugin的插件，您可以在pycharm顶部导航栏中的DevEco Testing Hypium > 隐私协议页面，点击“同意并开启”按钮来恢复Hypium对您个人信息的处理。

对于hypium-driver-js安装包，您可以在项目根目录运行 `npx hypium-driver telemetry status` 来查看Hypium个人信息处理状态。

对于hypium安装包，您可以在项目根目录运行 `python -m hypium telemetry status` 来查看Hypium个人信息处理状态。

对于hypium-pycharm-plugin的插件，您可以在pycharm顶部导航栏中的DevEco Testing Hypium > 隐私协议页面来查看Hypium个人信息处理状态。

**4** **数据存储地点及期限**

**4.1** **存储地点**

上述信息将会传输并保存至中华人民共和国境内的服务器。

**4.2** **存储期限**

我们仅在实现本声明所述目的所必需的时间内保留您的个人信息，并在超出下述保留时间后删除或匿名化处理您的个人信息，除非法律法规另有要求。

工具自身的测试数据及其备份数据将保存5年，目的是为了确保您的数据安全。

此外，当我们的产品或服务发生停止运营的情形时，我们将以推送通知、公告等形式通知您，并在合理的期限内删除您的个人信息或进行匿名化处理。

**5** **如何联系我们**

我们指定了个人信息保护负责人，您可以通过此[链接](https://consumer.huawei.com/cn/legal/privacy-questions/)联系个人信息保护负责人。您也可以通过访问[隐私问题页面](https://consumer.huawei.com/cn/legal/privacy-questions/)与我们其取得联系，我们会尽快回复。

如果您对我们的回复不满意，特别是当我们的个人信息处理行为损害了您的合法权益时，您还可以通过向有管辖权的人民法院提起诉讼、向行业自律协会或政府相关管理机构投诉等外部途径进行解决。您也可以向我们了解可能适用的相关投诉途径的信息。

华为将始终遵照我们的隐私政策来收集和使用您的信息。有关我们的隐私政策，可参阅[华为消费者业务隐私声明](https://consumer.huawei.com/minisite/legal/privacy/statement.htm?code=CN&language=zh-CN)。
# 自定义性能脚本测试（基于Python）

更新时间: 2025-12-11 16:00

## **概述**

DevEco Testing场景化的性能测试服务，基于Hypium自动化测试框架，为开发者提供性能测试能力，支持使用Python编写应用的性能测试脚本。本指南主要讲解性能测试脚本的开发。

Hypium基本API接口功能介绍，请参考指导：[Hypium框架-API使用方法](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/hypium-python-guidelines#section1141818121333)。

测试服务执行测试脚本详情介绍，请参考指导：[场景化性能测试](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/specialized-testing#section8642101711299)。

## **环境搭建**

**1、系统要求**

**Windows**

操作系统：Windows 10/11 64 位

内存：推荐使用16GB及以上（可用内存大于8G）

处理器：i7-10700@2.9GHz或者同等性能的型号

硬盘：可用硬盘空间100GB以上

**Mac**

操作系统：MacOS 13及以上

内存：推荐使用16GB及以上（可用内存大于8G）

处理器：i7-10700@2.9GHz及以上或Apple silicon M系列

硬盘：可用硬盘空间100GB以上

**2、环境配置**

**安装Python及Hypium**

参考指导：[应用UI测试-安装指导](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/hypium-python-guidelines)。

**安装hypium_perf**

1）打开Deveco Testing客户端-专项测试-场景化性能测试卡片，点击获取安装包，打开安装包目录，如下图。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251211160035.26426537434301255472366317321797:50001231000000:2800:74ED88CBB7D3D2D8C778B0919392C92171C9111FB726E28EC2473D0CA76244BB.png)

2）由于存在依赖关系，需要依次步骤1目录下的hypium、hypium-perf、perf_analyzer等安装包。

安装命令示例

1. pip install hypium-6.0.7.210.tar.gz
2. pip install hypium-perf-6.0.7.210.tar.gz
3. pip install perf_analyzer-6.0.7.203b0-py3-none-any.whl perf_collector-6.0.7.203b0-py3-none-any.whl perf_common-6.0.7.203b0-py3-none-any.whl perf_resource-6.0.7.203b0-py3-none-any.whl

注意

1、以上命令中安装包的版本仅供示例，具体版本号请参照实际下载版本。

2、若安装 paddlepaddle 失败，请先安装当前目录下提供的 paddlepaddle 的 whl 包，然后再安装其他 Python 包。

3）安装完成后，可前往查看PyCharm-设置-项目-Python解释器中的软件包与已安装版本是否一致。

## **脚本写作&调试**

## 脚本写作

**1、下载工程模板**

1）打开Deveco Testing客户端-专项测试-场景化性能测试卡片，在测试前准备中，点击创建工程模板按钮。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251211160035.07113015271392367616015935738171:50001231000000:2800:D51052AEB8535C63D3C0BA4C5F5D8C55218E44391F0AA0B96BCA629D4F58C6B9.png "点击放大")

2）填写工程项目名称，选择工程存放路径，点击开始生成按钮。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251211160035.78125246648340342036687456503214:50001231000000:2800:0360E98F1B2FFA1AC11B89C8F4C8003B902AF77299A589EBBDAB0A7299FB1AFB.png "点击放大")

3）在步骤2中填写的项目路径下，将自动生成用例模板。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251211160035.32290761895225748486426573265751:50001231000000:2800:0E53C65E56F67A2E7E53CC9F3061DF5DF4164F6C2736867B486541A35B672ABD.png)

注意

已创建的工程模板可在PyCharm中直接调试，或根据实际测试场景编写脚本。调试成功后，即可在DevEco Testing上执行性能测试。详细步骤请参阅本地脚本调试及测试执行章节。

**2、场景用例和原子用例使用说明**

（1）测试步骤

用户的一次操作定义为一个测试步骤。

（2）原子用例

多个测试步骤组合完成一套操作，形成一个原子用例。原子用例存放在models目录中，对应脚本中的一个模型，具有独立的编号。原子用例是最小的用例单元，且可以被重复使用。

（3） 场景用例

用户完成一件事情定义为一个场景用例。例如：用户在小红书浏览后去淘宝搜索购物。

一个场景用例对应一个用例文件，编号与文件名一致，存放在testcases目录下。场景用例是测试执行的入口，一个场景用例可以由多个原子用例组成。例如，上述场景可以由两个原子用例组成：1）用户浏览小红书；2）用户在淘宝搜索并购物。这两个原子用例独立且可被重用。

如果有另一个场景用例：用户在小红书浏览后去京东购物，那么“用户浏览小红书”这个原子用例即可被重用。

测试的执行入口和结果反馈均以场景用例为单位。

注意

- 1个性能场景用例由1-N个原子用例(Model)组成，1个原子用例对应1-N个测试步骤。
- 每个场景用例都需要一个配对的json配置文件。
- 场景用例包含的步骤数建议在30个步骤以下，步骤数过多可能会导致执行异常，建议进行用例拆分。
- 原子用例可以放在models目录下，推荐按照APP进行区分。

**3、场景用例写作指导**

**Testcase编写规范：**

Testcase对应的是测试场景中的一系列相关的原子用例操作序列。

（1）命名规范：

一个Testcase是一个独立的Python文件，Testcase编号与Python文件名一致，例：OH_PerfDemoTest.py。

（2）继承规范：

Testcase必须继承PerfBaseCase类，PerfBaseCase会负责用例开始时的初始化流程，进行一些设备环境检查操作。

（3）注释规范：

将Testcase的场景描述放置在用例最上方，方便审视测试场景所包含的原子用例执行步骤对应关系。

**场景用例示例：**

1. import os
2. from hypium.advance.perf.application_model.perf_basecase import PerfBaseCase
3. from models.browse_huawei_video import BrowseHuaweiVideo
4. # 场景用例名，和py文件名一致，可以自定义，但有推荐命名格式，需同步生成同名的json文件
5. # 测试用例应继承PerfBaseCase
6. '''
7. @场景用例
8. 浏览视频应用界面
9. @预置条件
10. 无
11. @原子用例
12. 视频页面浏览
13. '''
14. class OH_PerfDemoTest(PerfBaseCase):
15.     def __init__(self, controllers):  # 初始化操作，这里一般情况下不作变动
16.         self.TAG = self.__class__.__name__
17.         self.tests = [  # 指定场景用例执行入口
18.             "test_step"
19.         ]
20.         self.case_id = os.path.splitext(os.path.basename(__file__))[0]  # 文件名, 类名, case_id 三者保持一致
21.         self.case_scene_name = '浏览视频应用界面'  # 指定场景用例名称，用于显示在报告中
22.         case_pkg = 'com.huawei.hmsapp.himovie'  # 指定被测试应用，用于采集应用资源使用信息，如果未配置，则不采集
23.         PerfBaseCase.__init__(self, controllers, case_pkg)  # 调用父类初始化方法
24.         self.log.info("Case id is %s" % self.case_id)
25.     def setup(self):
26.         # 场景用例前置化操作，在test_step前执行的一些操作
27.         self.log.info("预置工作:初始化设备开始................." + self.devices[0].device_sn)
28.     def test_step(self):
29.         # 组装需要调用的原子用例，使用原子化用例构建场景步骤，可以一个场景用例添加多个相关的原子用例
30.         steps = [
31.             # 原子用例需要传入driver，case_id
32.             BrowseHuaweiVideo(self.driver, self.case_id)
33.         ]
34.         # 按顺序执行原子用例
35.         for item in steps:
36.             item.execute()
37.     def teardown(self):
38.         # 获取用例测试结果
39.         result = self.get_case_result()
40.         # 场景用例结束后执行该teardown操作
41.         self.log.info("收尾工作................., result is {}".format(result))
42.         # 此处为用例结尾时执行的PerfBaseCase的teardown方法，处理一些结束操作
43.         PerfBaseCase.teardown(self)

OH_PerfDemoTest.json 配置文件示例

1. {
2.     "description": "Config for OpenHarmony devicetest test cases",
3.     "environment": [
4.         {
5.             "type": "device"
6.         }
7.     ],
8.     "driver": {
9.         "type": "DeviceTest",
10.         "py_file": ["OH_PerfDemoTest.py"]
11.     }
12. }

注意

py_file 的值表示场景用例文件相对于 testcases 文件夹的路径。

例如，若场景用例文件直接位于 testcases 文件夹下，则 py_file 的值为 ["OH_PerfDemoTest.py"]，若场景用例文件位于 testcases 下的 test_01 文件夹中，则 py_file 的值为 ["test_01/OH_PerfDemoTest.py"]。

**4、原子用例写作指导**

**Model编写规范：**

Model对应的是原子用例中的一组操作序列，在脚本编写时对应一个Model类。

（1）命名规范：

一个Model是一个原子用例，Model类命名要有一定业务含义，例如：”视频页面浏览”命名为BrowseHuaweiVideo。

（2）继承规范：

Model类必须继承基类ModelBase，ModelBase会负责与采集器的交互，并且处理Model类抛出的异常。

（3）注释规范：

将原子用例操作步骤放置在用例最上方，方便审视Model类步骤和用例执行步骤对应关系。

**原子用例示例：**

1. from hypium import BY
2. from hypium.advance.perf.application_model.model_base import ModelBase
3. from hypium.advance.perf.driver_perf.idriver_perf import IDriverPerf
4. from hypium.advance.perf.driver_perf.tag import SceneType
5. from hypium.model import UiParam
6. '''
7. @原子用例
8. 视频页面浏览
9. @预置条件
10. 无
11. @用例步骤
12. 1.冷启动视频
13. 2.上滑1次浏览界面
14. 3.下滑1次浏览界面
15. 4.切换到影院界面
16. 5.精确的向上滑动界面
17. 6.抛滑，向下滑动界面
18. 7.侧滑返回
19. 8.点击我的
20. 9.上滑返回桌面
21. '''
22. APP_NAME = "视频"
23. class BrowseHuaweiVideo(ModelBase):  # 原子用例统一继承ModelBase
24.     def __init__(self, uidriver: IDriverPerf, case_id):  # 进行初始化操作
25.         ModelBase.__init__(self, uidriver, case_id)  # 调用父类初始化方法
26.         self.scene_no = "browse_huawei_video"  # 原子用例id
27.         self.scene_name = "浏览视频应用"  # 原子用例名字
28.         self.scene_type = "浏览视频应用场景"  # 原子用例类型
29.         self.scene_path = "日常高频操作-基础操作场景-系统通用操作场景-浏览视频应用"  # 原子用例所属路径
30.         self.driver = uidriver
31.     def setup(self):
32.         # 原子用例预置动作
33.         # 停止指定的应用
34.         self.driver.stop_app('com.huawei.hmsapp.himovie')
35.         # 返回手机桌面主页
36.         self.driver.go_home()
37.     @ModelBase.scene_recover
38.     def execute(self):
39.         # 1.冷启动应用'视频'
40.         # start_application_perf 启动应用的接口，从主页开始滑动查找对应APP名的应用，应用需要在桌面上可见，找到应用直接点击，打开应用
41.         # start_application_perf 接口为6.0版本新增接口请基于 Deveco Testing Hypium6.0.0 Release版本使用
42.         self.driver.start_application_perf("视频", SceneType.COLD_START)
43.         # 等待指定时间，等待界面稳定，再进行下一步操作
44.         self.driver.wait(3)
45.         # 2.上滑1次浏览界面
46.         # swipe_perf 在屏幕上或者指定区域area中执行朝向指定方向direction的滑动操作
47.         self.driver.swipe_perf(UiParam.UP,
48.                                tag=self.create_tag("上滑1次浏览界面", SceneType.NO_PAGE_SWITCH))
49.         # 等待指定时间，等待界面稳定，再进行下一步操作
50.         self.driver.wait(1)
51.         # 3.下滑1次浏览界面
52.         self.driver.swipe_perf(UiParam.DOWN,
53.                                tag=self.create_tag("下滑1次浏览界面", SceneType.NO_PAGE_SWITCH))
54.         # 等待指定时间，等待界面稳定，再进行下一步操作
55.         self.driver.wait(1)
56.         # 4.使用find_component查找控件，返回一个控件对象（控件文本为影院）
57.         com = self.driver.find_component(BY.text('影院'))
58.         # 可将控件对象传入touch_perf，会自动识别并转换为坐标点击
59.         self.driver.touch_perf(com, tag=self.create_tag("切换到影院界面", SceneType.WITH_PAGE_SWITCH))
60.         # 5.精确的向上滑动界面
61.         # slide_perf 根据指定的起始和结束位置执行滑动操作，起始和结束的位置可以为控件或者屏幕坐标。该接口用于执行较为精准的滑动操作。
62.         self.driver.slide_perf((0.5, 0.8), (0.5, 0.2), slide_time=0.5,
63.                                tag=self.create_tag("精确的向上滑动界面", SceneType.NO_PAGE_SWITCH))
64.         # 6.抛滑，向下滑动界面
65.         # fling_perf 抛滑接口
66.         self.driver.fling_perf(UiParam.DOWN, tag=self.create_tag("抛滑，向下滑动界面", SceneType.NO_PAGE_SWITCH))
67.         # 对于不需要性能指标的接口，可以使用不带perf的接口
68.         self.driver.touch((0.5, 0.3))
69.         # 等待指定时间，等待界面稳定，再进行下一步操作
70.         self.driver.wait(3)
71.         # 7.侧滑返回，退出
72.         # swipe_to_back_perf 滑动屏幕右侧返回
73.         self.driver.swipe_to_back_perf(tag=self.create_tag("侧滑返回", SceneType.WITH_PAGE_SWITCH))
74.         # 使用find_all_components根据BY指定的条件查找控件, 返回所有符合条件的控件，返回值是多个多个控件对象的值组成的列表（控件text值为我的）
75.         comps = self.driver.find_all_components(BY.text("我的"))
76.         # 8.点击我的
77.         # 可将控件对象传入touch_perf，会自动识别并转换为坐标点击
78.         self.driver.touch_perf(comps[0], tag=self.create_tag("点击我的", SceneType.WITH_PAGE_SWITCH))
79.         # 9.上滑返回桌面
80.         # swipe_to_home_perf 从屏幕底部上滑返回桌面
81.         self.driver.swipe_to_home_perf(tag=self.create_tag("上滑返回桌面", SceneType.WITH_PAGE_SWITCH))
82.     def teardown(self):
83.         # 原子用例结束清理步骤
84.         # 停止指定的应用
85.         self.driver.stop_app('com.huawei.hmsapp.himovie')

**5、使用UIViewer查看控件**

使用DevEco Testing->实用工具->UIViewer工具，辅助脚本写作。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251211160036.91240180846488944581172343263762:50001231000000:2800:8D953B97AA383718F22DF6ACB49CA562D707A83FF60D5791C8CC79CA894F2718.png)

## 测试框架介绍

**1、功能介绍**

性能测试框架作为Hypium自动化测试框架的增强能力，其设备操作API与Hypium保持一致。该框架主要负责性能自动化测试模型的流程控制，管理测试过程中的trace资源和视频资源采集，并提供自动化测试完成后的指标分析功能。

Hypium基本API接口功能介绍，请参考指导：[Hypium框架-API使用方法](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/hypium-python-guidelines#section1141818121333)。

注：若测试场景包含隐私界面则无法录屏进行测试，例如银行类应用、密码界面等。

**2、场景tag**

场景tag是测试框架定义的一套用于标注测试步骤使用场景的标签。

1. def create_tag(self, step_name="", scene_type="", tag_id="", pkg_name="", dynamic_type="", action_type="", trigger_type="", is_first_swipe=False, wait_time=0, is_watch=False, is_seek=False, is_short_video=False, need_wait_scene=True, ad_monitor=False, cold_start_wait_time=None, pop_up_window_enable=True, extend_param={})

|参数名称|参数描述|
|:--|:--|
|step_name|必填，测试步骤名字。|
|scene_type|必填，对应性能tag类型，从SceneType中选择。|
|tag_id|非必填，指定标签id。|
|pkg_name|非必填，测试应用相关包名。|
|dynamic_type|非必填，标记当前操作是否为动态阈值。|
|action_type|非必填，标记当前操作的类型。|
|is_first_swipe|默认False，标记是否为列表页面的首次滑动。|
|wait_time|默认0，增加采集时长，避免采集未包含全部动效。|
|is_watch|默认False，不做视频观看操作，设置为True会对页面进行30S观看，在scene_type为WATCH时生效。|
|is_seek|默认False，设置为True表示该操作为滑动进度条的操作。|
|is_short_video|默认False，在scene_type字段为PLAY_VIDEO时生效，标记起播视频为长视频（False）或者短视频（True）。<br><br>（时长小于5分钟的视频为短视频）|
|need_wait_scene|默认True，在执行完perf接口后需要进行预置等待时间，设置为False时，不需要进行等待。|
|ad_monitor|默认为False，在scene_type字段为COLD_START时生效，设置为True时，会进行广告检测。|
|cold_start_wait_time|非必填，在scene_type字段为COLD_START时生效，表示冷启动后，需要额外等待的时间。|
|pop_up_window_enable|默认True，在scene_type字段为COLD_START时生效，表示冷启动后，是否执行一次弹窗检测操作。|
|extend_param|预留字段。|

注意

所有性能测试需要采集指标的步骤，有以下3个原则：

- API接口使用 _perf方法。
- 必须带上场景tag。
- 每个步骤必须是单独的tag，不能多个步骤共用一个tag。

**3、****场景tag类型**

1. class SceneType(Enum):
2.     # 起播时延
3.     PLAY_VIDEO = "PLAY_VIDEO"
4.     # 冷启
5.     COLD_START = "COLD_START"
6.     # 热启
7.     HOT_START = "HOT_START"
8.     # 有页面切换
9.     WITH_PAGE_SWITCH = "WITH_PAGE_SWITCH"
10.     # 无页面切换
11.     NO_PAGE_SWITCH = "NO_PAGE_SWITCH"
12.     # 视频观看
13.     WATCH = "WATCH"

注：滑动和无页面切换操作的场景不测完成时延；冷启动操作前需要杀掉该后台应用，热启动操作前需要拉起该应用并置于后台。

**4、****hypium_perf常用接口和用法**

在Hypium的界面操作接口上封装一套perf接口，提供给性能测试使用。

注意

以下所有示例代码中driver都是UiExplorerPerf对象。

**Phone常用接口**

**1、点击****操作**

1. def touch_perf(self, target: **Union**[By, UiComponent, tuple], wait_time: float = 0.1, tag: Tag = None)

**接口说明**

根据选定的控件或者坐标位置执行点击操作。

**参数说明**

|序号|参数名称|参数描述|
|:--|:--|:--|
|1|target|需要点击的目标，可以为控件（通过By类指定）或者屏幕坐标（通过tuple类型指定，例如（100，200）， 其中100为x轴坐标，200为y轴坐标）， 或者使用find_component找到的控件对象。|
|2|wait_time|点击后等待响应的时间，默认0.1s。|
|3|tag|对应性能场景tag，点击如果进入新界面，需使用WITH_PAGE_SWITCH（有界面切换的场景类型）。|

**使用示例**

1. # 点击文本为"hello"的控件
2. driver.touch_perf(BY.text("hello"), tag=self.create_tag("点击hello", SceneType.NO_PAGE_SWITCH))

3. # 点击（100，200）的位置
4. driver.touch_perf(（100，200）, tag=self.create_tag("点击（100，200）", SceneType.NO_PAGE_SWITCH))

5. # 冷启动相机
6. APP_NAME="相机"
7. icon_pos = self.driver.find_app_in_launcher(APP_NAME)
8. driver.touch_perf(icon_pos, tag=self.create_tag("相机冷启动", SceneType.COLD_START))

**2、长按****操作**

1. def long_touch_perf(self, target: **Union**[By, UiComponent, tuple], tag: Tag = None)

**接口说明**

根据选定的控件或者坐标位置执行长按操作。

**参数说明**

|序号|参数名称|参数描述|
|:--|:--|:--|
|1|target|需要点击的目标，可以为控件（通过By类指定）或者屏幕坐标（通过tuple类型指定，例如（100，200）， 其中100为x轴坐标，200为y轴坐标），或者使用find_component找到的控件对象。|
|2|tag|对应性能场景tag，点击如果进入新界面，需使用WITH_PAGE_SWITCH（有界面切换的场景类型）。|

**使用示例**

1. # 长按相机图标，弹出弹窗
2. APP_NAME="相机"
3. icon_pos = self.driver.find_app_in_launcher(APP_NAME)
4. driver.long_touch_perf(icon_pos, tag=self.create_tag("长按相机图标弹出弹窗", SceneType.NO_PAGE_SWITCH))

**3、双击****操作**

1. def double_touch_perf(self, target: **Union**[By, UiComponent, tuple], tag: Tag = None)

**接口说明**

根据选定的控件或者坐标位置执行双击操作。

**参数说明**

|序号|参数名称|参数描述|
|:--|:--|:--|
|1|target|需要点击的目标，可以为控件（通过By类指定）或者屏幕坐标（通过tuple类型指定，例如（100，200）， 其中100为x轴坐标，200为y轴坐标），或者使用find_component找到的控件对象。|
|2|tag|对应性能场景tag，点击如果进入新界面，需使用WITH_PAGE_SWITCH（有界面切换的场景类型）。|

**使用示例**

1. # 双击确认按钮（控件文本为确认）
2. driver.double_touch_perf(BY.text("确认"), tag=self.create_tag("双击确认按钮", SceneType.WITH_PAGE_SWITCH))

**4、执行指定距离的滑动操作**

1. def **swipe_perf**(self, direction: str, distance: int = 60, start_point: tuple = None, swipe_time: float = None, tag: Tag = None)

**接口说明**

在屏幕上或者指定区域area中执行朝向指定方向direction的滑动操作。该接口用于执行不太精准的滑动操作。

|序号|参数名称|参数描述|
|:--|:--|:--|
|1|direction|滑动方向，目前支持：”LEFT” 左滑；”RIGHT” 右滑；”UP” 上滑；”DOWN” 下滑。|
|2|distance|相对滑动区域总长度的滑动距离，范围为1~100，表示滑动长度为滑动区域总长度的1%到100%， 默认为60。|
|3|start_point|滑动起始点，默认为None，表示在区域中间位置执行滑动操作，可以传入滑动起始点坐标，支持使用(0.5, 0.5)这样的比例坐标。当同时传入side和start_point的时候，仅start_point生效。|
|4|swipe_time|滑动时间（s)， 默认0.3s。|
|5|tag|对应性能场景tag，若该操作不涉及页面切换，需使用NO_PAGE_SWITCH。|

**使用示例**

1. # 在屏幕上向上滑动40
2. driver.swipe_perf(UiParam.UP, distance=40, tag=self.create_tag("向上滑动", SceneType.NO_PAGE_SWITCH))

3. # 在屏幕上向右滑动, 滑动时间为0.1秒
4. driver.swipe_perf(UiParam.RIGHT, swipe_time=0.1, tag=self.create_tag("向右滑动", SceneType.NO_PAGE_SWITCH))

5. # 在屏幕起始点为比例坐标为(0.8, 0.8)的位置向上滑动30
6. driver.swipe_perf(UiParam.UP, 30, start_point=(0.8, 0.8), tag=self.create_tag("向上滑动", SceneType.NO_PAGE_SWITCH))

**5、执行精准的滑动操作**

1. def **slide_perf**(self, start: **Union**[By, tuple], end: Union[By, tuple], slide_time: float = 2, tag: Tag = None)

**接口说明**

根据指定的起始和结束位置执行滑动操作，起始和结束的位置可以为控件或者屏幕坐标。该接口用于执行较为精准的滑动操作。

**参数说明**

|序列|参数名称|参数描述|
|:--|:--|:--|
|1|start|滑动起始位置，可以为控件BY.text("滑块")或者坐标（100，200），或者使用find_component找到的控件对象。|
|2|end|滑动结束位置，可以为控件BY.text("最大值")或者坐标（100，200）, 或者使用find_component找到的控件对象。|
|3|slide_time|滑动操作总时间，单位秒。|
|4|tag|对应性能场景tag，若该操作不涉及页面切换，需使用NO_PAGE_SWITCH。|

**使用示例**

1. # 从类型为Slider的控件滑动到文本为最大的控件
2. driver.slide_perf(BY.type("Slider"), BY.text("最大"),tag=self.create_tag("滑动到最大", SceneType.NO_PAGE_SWITCH))

3. # 从坐标100，200滑动到300，400
4. driver.slide_perf(（100，200）, (300, 400), tag=self.create_tag("向上滑动", SceneType.NO_PAGE_SWITCH))

5. # 从坐标100，200滑动到300，400, 滑动时间为3秒
6. driver.slide_perf(（100，200）, (300, 400), slide_time=3, tag=self.create_tag("向上滑动", SceneType.NO_PAGE_SWITCH))

**6、拖拽****操作**

1. def **drag_perf**(self, start: **Union**[By, tuple], end: **Union**[By, tuple],
2.                   area: By = None, press_time: float = 1, drag_time: float = 1, tag: Tag = None)

**接口说明**

根据指定的起始和结束位置执行拖拽操作，起始和结束的位置可以为控件或者屏幕坐标。

**参数说明**

|序号|参数名称|参数描述|
|:--|:--|:--|
|1|start|拖拽起始位置，可以为控件BY.text("滑块")或者坐标（100，200），或者使用find_component找到的控件对象。|
|2|end|拖拽结束位置，可以为控件BY.text("最大值")或者坐标（100，200），或者使用find_component找到的控件对象。|
|3|area|拖拽操作区域，可以为控件BY.text("画布")，或者使用find_component找到的控件对象。目前仅在start或者end为坐标时生效，指定区域后，当start和end为坐标时，其坐标将被视为相对于指定的区域的相对位置坐标。|
|4|press_time|拖拽操作开始时长按的时间，默认为1s（暂不支持修改）。|
|5|drag_time|拖动的时间， 默认为1s（整个拖拽操作总时间 = press_time + drag_time）。|
|6|tag|对应性能场景tag，若该操作不涉及页面切换，需使用NO_PAGE_SWITCH。|

**使用示例**

1. # 拖拽文本为"文件.txt"的控件到文本为"上传文件"的控件
2. driver.drag_perf(BY.text("文件.txt"), BY.text("上传文件"), tag=self.create_tag("拖拽文件", SceneType.NO_PAGE_SWITCH))

3. # 拖拽id为"start_bar"的控件到坐标（100，200）的位置, 拖拽时间为2秒
4. driver.drag_perf(BY.key("start_bar"), （100，200）, drag_time=2, tag=self.create_tag("拖拽start_bar", SceneType.NO_PAGE_SWITCH))

5. # 在id为"Canvas"的控件上从相对位置(10, 20)拖拽到（100，200）
6. driver.drag_perf((10, 20), （100，200）, area = BY.id("Canvas"), tag=self.create_tag("拖拽Canvas", SceneType.NO_PAGE_SWITCH))

7. # 在滑动条上从相对位置(10, 10)拖拽到(10, 200)
8. driver.drag_perf((10, 10), (10, 200), area=BY.type("Slider"), tag=self.create_tag("拖拽滑动条", SceneType.NO_PAGE_SWITCH))

**7、屏幕侧边滑动返回****操作**

1. def **swipe_to_back_perf**(self, side=UiParam.RIGHT, times: int = 1, height: float = 0.5, tag: Tag = None)

**接口说明**

滑动屏幕侧边返回。设备需开启触摸屏手势导航。

**参数说明**

|序号|参数名称|参数描述|
|:--|:--|:--|
|1|side|滑动的位置，“RIGHT“表示在右边滑动返回，“LEFT“表示在左边滑动返回。|
|2|times|滑动次数，默认1次，某些场景可能需要两次才能返回。|
|3|height|滑动位置在屏幕中Y轴的比例高度（从屏幕顶部开始计算）。|
|4|tag|对应性能场景tag，侧边返回有界面切换时，需使用WITH_PAGE_SWITCH。|

**使用示例**

1. # 侧滑返回
2. self.driver.swipe_to_back_perf(tag=self.create_tag("侧滑返回", SceneType.WITH_PAGE_SWITCH))

3. # 侧滑2次返回
4. self.driver.swipe_to_back_perf(times=2, tag=self.create_tag("侧滑2次返回", SceneType.WITH_PAGE_SWITCH))

5. # 设置侧滑位置的高度比例为屏幕高度的80%，即在屏幕靠下的位置侧滑返回
6. self.driver.swipe_to_back_perf(height=0.8, tag=self.create_tag("屏幕靠下的位置侧滑返回", SceneType.WITH_PAGE_SWITCH))

**8、从屏幕底部上滑返回桌面**

1. def **swipe_to_home_perf**(self, times: int = 1, tag: Tag = None)

**接口说明**

屏幕底端上滑回到桌面，设备预置：设备开启触摸屏手势导航。

**参数说明**

|序号|参数名称|参数描述|
|:--|:--|:--|
|1|times|上滑次数，默认1次，某些场景可能需要两次上滑才能返回桌面。|
|2|tag|对应性能场景tag，返回桌面一般带有界面切换，需使用WITH_PAGE_SWITCH。|

**使用示例**

1. # 上滑返回桌面
2. self.driver.swipe_to_home_perf(tag=self.create_tag("上滑返回桌面", SceneType.WITH_PAGE_SWITCH))

3. # 连续上滑2次返回桌面
4. self.driver.swipe_to_home_perf(times=2, tag=self.create_tag("上滑返回桌面", SceneType.WITH_PAGE_SWITCH))

**9、观看视频**

1. def watch_perf(self, watch_time, is_bullet_screen=False, is_full_screen=False, watch_tag_desc=None)

**接口说明**

在页面停留指定时间，进行观看视频操作。

**参数说明**

|序号|参数名称|参数描述|
|:--|:--|:--|
|1|watch_time|观看时长，防止长时间观看行为导致视频过大，会按照30S对时长进行分割。|
|2|is_bullet_screen|默认False，设置为True时，对视频播放与弹幕进行卡顿检测。|
|3|is_full_screen|默认False，设置为True时，表示当前为全屏播放。|
|4|watch_tag_desc|非必填，填写后会生成步骤操作描述，对于观看时间大于30S的场景，不建议设置。|

**使用示例**

1. # 观看20S视频，检测视频卡顿
2. self.watch_perf(20)

3. # 全屏观看20S视频，检测弹幕卡顿与视频卡顿
4. self.watch_perf(20, is_bullet_screen=True, is_full_screen=True)

5. # 指定操作步骤观看视频
6. self.watch_perf(20, watch_tag_desc="观看直播视频")

**10、在桌面滑动查找APP，并打开应用**

1. def start_application_perf(self, app_name, scene_type, tag=None)

**接口说明**

基于APP名称，在桌面上滑动查找指定APP，并进行点击。设备预置：需提前下载APP，并放置在桌面，不要放入文件夹中。

**参数说明**

|序号|参数名称|参数描述|
|:--|:--|:--|
|1|app_name|应用名称，与桌面上显示的名称一致。|
|2|scene_type|应用启动方式，为SceneType.COLD_START或者SceneType.HOT_START。|
|3|tag|非必填，如果没赋值，则会根据scene_type自动生成。|

**使用示例**

1. # 启动设置应用
2. self.driver.start_application_perf("设置", SceneType.COLD_START)

**使用示例**

1. # 查找需要操作的窗口
2. window = driver.find_window(WindowFilter().bundle_name(package_name))
3. # 点击窗口最小化
4. driver.minimize_window_perf(window, tag=self.create_tag("点击窗口最小化", 
5. scene_type=SceneType.WITH_PAGE_SWITCH))

**常用视频检测场景介绍**

**1、视频起播时延测试步骤**

1. # 点击视频图框播放视频
2. self.driver.touch_perf(BY.text("视频"), tag=self.create_tag("点击播放长视频", SceneType.PLAY_VIDEO, is_seek=False, is_short_video=True))

**2、视频卡顿测试步骤**

场景1：测试视频卡顿

1. # 观看180S视频
2. self.watch_perf(180)

场景2：测试起播时延与视频卡顿

1. watch_tag=self.create_tag("点击播放长视频并观看", SceneType.PLAY_VIDEO, is_seek=False, is_short_video=True)
2. watch_tag.watch_time=10
3. # 点击视频图框播放视频，并观看10S视频
4. self.driver.touch_perf(BY.text("视频"), tag=watch_tag)

## 本地脚本调试

**1、****main.py实现**

**方法一：**在main.py中修改cmd命令，将参数替换为本地调试的场景用例名称。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251211160036.53258987659356758415976938680935:50001231000000:2800:6F3A1DABC0FC0A33F8C2D8CC090C71931A01D1D372433BAC7D9A6564E4E791F3.png "点击放大")

main.py示例

1. import time
2. from xdevice.__main__ import main_process
3. if __name__ == "__main__":
4.     try:
5.         pass_dict = dict()
6.         pass_dict['task_id'] = time.strftime('%Y%m%d%H%M%S', time.localtime())
7.         cmd = 'run -l OH_PerfDemoTest -ta pass_through:' + str(pass_dict)
8.         main_process(cmd)
9.         time.sleep(10)
10.     except Exception as e:
11.         print(e)
12.     finally:
13.         print("Task is End")

**方法二：**在main.py同级目录下，新建一个json文件，命名为action_testsuite.json，并在main.py中修改cmd命令。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251211160036.59600806355487389338608302887029:50001231000000:2800:AB8FCC8A45A31943AD756C0B3130237697883764211FCC823962C9E2AE855153.png "点击放大")

action_testsuite.json示例

1. {
2.     "description": "hypium test case",
3.     "environment": [
4.         {
5.             "type": "device"
6.         }
7.     ],
8.     "driver": {
9.         "type": "DeviceTest",
10.         "py_file": [
11.             "OH_PerfDemoTest.py"
12.         ]
13.     },
14.     "kits": [
15.     ]
16. }

**2、本地多用例执行方式**

一个测试任务执行多个场景用例，而不必每个场景用例单独执行，任务会按照顺序依次执行指定的场景用例。

**方法一：**在main.py 的cmd命令中指定多个case，用”;”分割。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251211160036.20845559308309712451295042273055:50001231000000:2800:CCA7D217FC8DAEB4C09018A4FC78EB2473F1A288CC059F7DBA58C7C9E3ABE603.png "点击放大")

**方法二：**在json文件配置，并在main.py的cmd命令参数中指定json文件。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251211160036.93210948928552429723550109647457:50001231000000:2800:A57BDEC72DF92F0EC88E703DA46A1E75E88398228CAB90944959623C282EABDB.png "点击放大")

action_testsuite.json示例

1. {
2.     "description": "hypium test case",
3.     "environment": [
4.         {
5.             "type": "device"
6.         }
7.     ],
8.     "driver": {
9.         "type": "DeviceTest",
10.         "py_file": [
11.             "Open_Perf_Test.py",
12.             "OH_PerfDemoTest.py"
13.         ]
14.     },
15.     "kits": [
16.     ]
17. }

## **性能脚本测试执行**

性能脚本本地调试验证成功后，可在DevEco Testing创建性能测试任务，请查看文档：[场景化性能测试-任务创建](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/specialized-testing#section8642101711299)。
