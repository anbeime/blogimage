# 工具概述

更新时间: 2025-12-16 15:58

DevEco Studio AI辅助编程工具（CodeGenie）支持智能问答、代码生成、页面生成、万能卡片生成、单元测试用例生成、代码智能解读、编译报错智能分析、智慧调优、应用UI生成、意图装饰器生成、小艺智能体创建、MCP配置、自定义Agent等能力，帮助开发者更高效的开发应用。

## 使用方式

在DevEco Studio右侧边栏点击**CodeGenie**或输入快捷键**Alt/Option+U**，可以进入DevEco CodeGenie。

点击**Sign in** ，跳转华为账号登录页面。授权登录完成后返回DevEco Studio，提示登录成功后，点击**Agree**，同意隐私安全政策及使用条款后开始体验。

若使用非最新版本的DevEco CodeGenie，可通过[下载中心](https://developer.huawei.com/consumer/cn/download/deveco-codegenie)获取并使用相关功能，具体请参考[插件获取及安装](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-codegenie#section18337533718)。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155802.39625816370431868841764960913913:50001231000000:2800:D7EC0CF071F81540518A86CD5DC1F76112E567C794807541B5F8528E6DA63064.png "点击放大")

## 插件获取及安装

如需在历史版本DevEco Studio中使用最新版本的CodeGenie功能，可通过访问[下载中心](https://developer.huawei.com/consumer/cn/download/deveco-codegenie)获取最新CodeGenie插件版本，并根据下载中心页面**工具完整性**指导进行完整性校验。安装包存放路径不能包含中文字符。

安装压缩包**无需解压**，下载完成可直接依照下方步骤进行安装。

1. 在DevEco Studio菜单栏，点击**File > Settings**（macOS为**DevEco Studio > Preferences****/****Settings**）**> Plugins**，点击![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155802.00572828778474956956404756256230:50001231000000:2800:9DFCD76163BBFC133BC795CA586118842362BF80E2D46A6C38CC07683D50D0D7.png) **> Install Plugin from Disk…**安装本地插件。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155802.06669953243125917655350037949406:50001231000000:2800:A42DCAF28649BAC06778404AB1F79BE19D87A061BD37C42A7DD67F033B3F3460.png "点击放大")
    
2. 在弹出的文件选择窗口中，选择**未解压的插件****包**的存放位置，点击**OK**确认安装插件。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155802.25425579809569873889731742802269:50001231000000:2800:FB107F5686D3EE38DD561A276CE9D86B6202D3BCE2DBCAD9365ED8B27D27D0FB.png)
    
3. 点击**Restart IDE**，重新启动DevEco Studio。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155802.93576603089994142263845458348691:50001231000000:2800:56963821A780080C58B97F72E8E187D2A6A06F9E4188AB9120AA4C2C5ECE2561.png)
    
4. 在DevEco Studio右侧边栏点击**CodeGenie**进入DevEco CodeGenie，完成登录并开始体验。

[版本说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-codegenie-releasenote "版本说明")

[智能问答](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-codegenie-knowledge "智能问答")
# 智能问答

更新时间: 2025-12-16 15:58

CodeGenie基于生成式搜索能力，通过查询生成、内容优选服务高效理解用户意图，问答交互式地获取编码相关知识。

## 对话示例

在对话区域输入需要查询的问题，开始问答。示例如下：

- ArkTS如何实现多线程？
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155803.39210445286469584378085637675217:50001231000000:2800:45289906DDCEC60BE3BAA5B4A2A6EE55F4C047505CA86ACF8AE9F23B30005E41.gif)
    

## 上下文问答

在对话框中输入**@**符号选择**Files**，或点击上方**@****Add Context** > **Files**，可指定对单个或多个代码文件进行分析。

点击![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155803.32638765690231786962836138991984:50001231000000:2800:42C81C8AAAF4464BB5F9E2B76FCFE3DC9A6E3C7F7DDCD5DF65F481492D35731F.png)图标开启光标上下文功能，该功能可识别光标位置和选中的代码片段，让CodeGenie分析指定文件和选中的代码片段。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155803.36585291529802253466876795787297:50001231000000:2800:83C3D6705F3C3D0F84B853E203C042502BE571A1D5777FE02B0D757EEBEAC60E.gif)

## 指定风格的上下文问答

从DevEco Studio 6.0.0 Beta5开始，CodeGenie允许用户导入设计文档和代码等文件形成文档集，多个文档集组合成本地知识库。智能问答时，根据用户输入内容检索本地知识库以提升AI生成的能力。

1. 点击**File > Settings****...**（macOS为**DevEco Studio > Preferences/Settings**） **> CodeGenie** **> Knowledge >** **Docs**，或在DevEco Studio右侧边栏点击**CodeGenie**（或输入快捷键**Alt/Option+U**） **>** **@****Add Context** **> Docs > Set Local Knowledge Base**，进入配置页面。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155803.77668514795431472034674323381753:50001231000000:2800:88218A05DDFB10BBBC23A064CAC5AE970DF1A6295313205ADDCF2139A59632E7.png "点击放大")
    
2. 首次打开时，点击![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155803.94337169514638504065345934668871:50001231000000:2800:95C5E65C819B55FFB25E04D88E16E00F597D4A2F941863387BB23EDA8FBE282A.png)按钮，填写相关信息，创建文档集。
    
    - **Knowledge Base Path**：知识库保存路径。在同一个路径下保存的文档集，会形成一个知识库。
    - **Document set name**：文档集名称。
    - **Description**：可选，文档集描述。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155803.67434971444170372222029999254245:50001231000000:2800:9B0BD8FB371EEA995CCC33796BBB3058AB9D4F386C4356678E9250DBAF26591E.png "点击放大")
    
3. 点击![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155803.01885316712140837063716743825647:50001231000000:2800:B97537E6AB2BED8C112EB11DE814735FCB9E8C4A0F9E453256FE71A675B04FC7.png)按钮，添加文档集中的文件，添加成功的文件在下方展示。
    
    说明
    
    1. 支持的文件格式：txt、md、json、html、cpp、ets、ts、js。
    2. 单个文档集中文件个数：不超过1000个。
    3. 单个文件大小：不超过10M。
    4. 单个知识库中文档集个数：不超过20个。
    5. 单个知识库大小：不超过50M。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155803.05970841606115227635614818008108:50001231000000:2800:67AAFE412C730861BB42B8513E203FEED596718FCC6C74C9A9F4B5158CF46375.png "点击放大")
    
4. 点击“**OK**”，完成本地知识库配置和同步，在DevEco Studio页面下方**Storing document set**可查看同步进度。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155803.51383362839413061822674121132715:50001231000000:2800:DAD203166A829163DC18B2EA2E758ECF4BBB98B3A3FC5B852E9425B8BAEDD9ED.png "点击放大")
    
5. 同步完成后，在对话框中输入**@**符号选择**Docs** ，或点击上方**@****Add Context** **> Docs** ，选择需要的文档集。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155803.26443670399151121381907066289231:50001231000000:2800:03F29576C1776C4C79464E653BD901CBA2EB95322124234DC5E0EDDE6E7DA667.png)
    
6. 选择代码文件进行上下文问答，具体请参考[上下文问答](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-codegenie-knowledge#section1464704715252)。

[工具概述](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-codegenie "工具概述")

[代码生成](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-codegenie-code-edit "代码生成")
# 自然语言代码生成

更新时间: 2025-12-16 15:58

安装CodeGenie后，在对话框内输入代码需求描述，将根据描述智能生成代码，生成内容可一键复制或一键插入至编辑区当前光标位置，以及生成内容可与文件内容可快速对比和采纳。

提问问答和代码修改逻辑不同，若更换代码生成方式，需要重新开启对话框。

## 提问问答

### 操作步骤

在对话区域输入代码需求描述，点击![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155809.39506999457203446374365007293261:50001231000000:2800:C61A9D3A110724ADA73E434604C58D9927B790454A69EB5A95ABD84D01448DBE.png)发送，将自动生成符合要求的代码段，生成内容可一键复制![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155809.49506576690380625618246419551089:50001231000000:2800:0C3F478ABC3CFA256C3377E3CE733C88A6CECF62A05D9496BAE94C7C565B3A47.png)或一键插入![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155809.87666815588454523642823608140091:50001231000000:2800:59A494EB85493B3AA0465D516BDEE2CD22C874EE412426F62AA4CDB8C30B29AC.png)至编辑区当前光标位置。

### 示例

使用ArkTs语言写一段代码，在页面中间部分插入Swiper组件，其中有3个Image组件，其图片资源名分别为app.media.phone，app.media.watch，app.media.glasses。这些Image组件的宽度撑满父布局，高度为600，图片缩放类型为保持图片宽高比不变，将图片完全显示在边界内。 Swiper组件设置为自动播放，播放时间间隔为2秒。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155809.14230259043000039258740152636060:50001231000000:2800:7364E5FFFDC4A1CE821EE8AD942F0EF37A816545F1D9E26FBFF46BCA2635524A.gif)

## 代码修改

从DevEco Studio 6.0.1 Beta1开始，支持选择文件后，再输入代码需求描述，生成内容与文件内容可快速对比和采纳。

**操作步骤**

1. 点击**@Add Context >** **Files**选择需要修改的文件，在对话框输入代码修改描述。
2. 在生成内容中，点击文件路径，打开代码对比页面。点击![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155809.73485244976619489847887176584589:50001231000000:2800:B7B0AC5670D145D124F587B12B2A0116A0C1EB85482D279056303315D42CAFD2.png)，快速采纳修改后的代码。

**示例**

新增如下代码段：使用ArkTs语言写一段代码，在页面中间部分插入Swiper组件，其中有3个Image组件，其图片资源名分别为app.media.phone，app.media.watch，app.media.glasses。这些Image组件的宽度撑满父布局，高度为600，图片缩放类型为保持图片宽高比不变，将图片完全显示在边界内。 Swiper组件设置为自动播放，播放时间间隔为2秒。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155809.87276853669456754249680091927730:50001231000000:2800:A5BD2A3AD894E802B0F0DA1ABE48464D55E25DDA338DDCB7FDF4B9A99B9D4F77.gif)

[代码生成](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-codegenie-code-edit "代码生成")

[编辑区代码生成](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-edit-area-code-generation "编辑区代码生成")
# 编辑区代码生成

更新时间: 2025-12-16 15:58

CodeGenie提供Inline Edit能力，支持在ArkTS文件的编辑窗口中通过自然语言进行问答，基于上下文智能生成代码片段，提升代码可读性。

1. 当前有以下两种方式唤醒Inline Edit对话框：
    
    - 在代码编辑区域，右键选择**CodeGenie > Inline Edit**（或使用快捷键**Alt+I**，macOS中为**Command+I**），唤醒Inline Edit对话框。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155810.21214501951273164595320332582692:50001231000000:2800:DDB6018999A07493B859DA49F85904C50CDB5EA22F019F9CBD5F402F8BF0300A.png)
        
    - 选中一段代码，点击**Inline Edit（**或使用快捷键**Alt+I**，macOS中为**Command+I）**浮框，唤醒Inline Edit对话框。
        
        如未出现浮框，可在**File** > **Settings** > **CodeGenie** > **Code Generation**（macOS中为**DevEco Studio** > **Preferences/Settings** > **CodeGenie** > **Code Generation**）中取消勾选**Hide Inline Edit Overlay**选项。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155810.16351220869033844341787114274047:50001231000000:2800:E6308E0841491B28932FE851BD5A2B6B9C9E23436CB4B7FEF7451D1137A1B10D.png)
        
    
2. 在对话框中输入所需要的代码功能描述，在键盘输入回车开始生成。点击**Stop Generation**，可中断本轮代码生成过程。
3. 生成完毕将在编辑区展示本轮生成的代码内容，并通过不同颜色体现与当前代码的对比差异。
    
    - 绿色区域：新生成的代码内容。
    - 蓝色区域：对现有代码进行修改的内容。
    - 红色区域：删除的代码内容。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155810.76361817503060222058592614981970:50001231000000:2800:51B3C5A320FDADE75A83C43486FB81C7647E62AA314F133DCA4939D0C5DD979A.png)
    
    点击Inline Edit对话框中**Accept All**（或使用快捷键**Alt+Enter**），接受当前生成的全部内容；点击界面中Accept区域（或使用快捷键**Shift+Ctrl+Y**，macOS上为**Shift+Command+Y**），分段逐一接受并保留生成内容；点击界面中Reject区域（或使用快捷键**Shift+Ctrl+N**，macOS上为**Shift+Command+N**），分段逐一拒绝并删除当前生成内容。
    
4. 点击Inline Edit对话框中**刷新/****Regenerate**，将根据当前描述重新生成代码片段。如需开始新一轮问答，点击**Further Edit**（或使用快捷键**Ctrl+K**，macOS上为**Command+K**），重新进行输入。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155810.48396912325789378327701620511269:50001231000000:2800:1E1277A09CC5423C6412421EB1B92B7A9C97E37726A401B742BC8D6D56FB4001.png)
    

[自然语言代码生成](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-natural-language-code-generation "自然语言代码生成")

[编辑区代码续写](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-code-continuation "编辑区代码续写")
# 编辑区代码续写

更新时间: 2025-12-16 15:58

利用AI大模型分析并理解开发者在代码编辑区的上下文信息或自然语言描述信息，智能续写符合上下文的ArkTS或C++代码片段。

## 使用约束

- 建议编辑区已有较丰富上下文，能够使AI模型对编程场景有一定理解的情况下进行续写。若编辑器中内容较少，AI模型可能无法有效理解用户的意图并生成相应的代码。
- AI模型反馈需满足规则：光标上文10行内，有效代码行数超过5行（排除单独{}、（）、[]括号行、空行、纯注释行场景）。

## 续写设置

进入**File > Settings...**（macOS为****DevEco Studio > Preferences/Settings****） **>** **CodeGenie > Code Generation**页面勾选**Enable code generation**，开启代码续写功能。如果已经熟悉了CodeGenie常用的快捷键，想要更加沉浸的体验，可以在该页面勾选**Do not disturb** **mode**，隐藏代码生成工具栏及快捷键提示。

根据编码习惯，选择**Enable snippet generation**（片段续写）和**Enable inline generation**（行内续写），以及设置续写时延。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155810.91014231183767580932507879532017:50001231000000:2800:2046B88C3816A89A0A08D296297FC69FCC2F13BD6440A4448F3E296BB8FBB2EE.png)

## 续写触发和采纳

### 续写触发

不同代码续写类型的触发方式：

- **Enable inline generation**（行内续写）：在编码时稍作停顿，CodeGenie将在当前代码行即时续写代码。
- **Enable snippet generation**（片段续写）：输入回车，将出现CodeGenie根据上下文生成的代码片段。
- 在编辑区输入**Alt+C**快捷键（macOS上为**Option+C**）触发代码续写。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155810.44158317919903958591327007299998:50001231000000:2800:B735A1D00919E6A4822632D4BCA58E346F67004E3BCE73C9DACA08123DED5D80.png)

### 续写采纳

续写内容采纳方式**：**

- 可通过按**Ta****b**键采纳该内容。
- **Ctrl + ↓（**macOS中为Command + ↓**）**逐行采纳该内容。
- **Ctrl + →****（**macOS中为Option + →**）**逐单词采纳该内容。
- 通过按**ESC**键忽略该内容。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155810.81541792728264274902624956143256:50001231000000:2800:32FF51255D3D1E7EB6A367416C079A7B4D4191F9F90C8D1267774DB869359EEE.png "点击放大")

CodeGenie续写常用快捷键如下：

|   |   |   |
|---|---|---|
|**操作**|**macOS**|**Windows**|
|触发多行代码续写|Enter、Option+C|Enter、Alt+C|
|触发单行代码续写|Option+X|Alt+X|
|采纳续写生成的代码|Tab|Tab|
|忽略续写生成的代码|Esc|Esc|
|查看上一个代码续写结果|Option +[|Alt + [|
|查看下一个代码续写结果|Option + ]|Alt + ]|
|重新生成代码内容（最多支持重新生成5次）|Option + R|Alt + R|
|展示CodeGenie面板|Option + U|Alt + U|
|代码逐行采纳|Command + ↓|Ctrl + ↓|
|代码逐单词采纳|Option + →|Ctrl + →|

[编辑区代码生成](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-edit-area-code-generation "编辑区代码生成")

[页面生成](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-page-generation "页面生成")
# 页面生成

更新时间: 2025-12-16 15:58

支持通过自由输入、快捷模板、上传页面参考图片三种方式，生成应用/元服务可用的页面代码，生成结果支持实时预览，帮助开发者快速完成页面搭建。

从DevEco Studio 6.0.1 Beta1开始，在输入框新增页面生成的入口。

1. 点击页面右侧菜单栏CodeGenie图标完成登录后，可以通过如下两种方式进入页面生成窗口：
    
    - 在输入框左下角下拉框选择**Generate UI Code。**
    - 在输入框输入"/"调出命令，**选择Generate UI Code**。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155803.37899854363634460916197085360858:50001231000000:2800:DAE659555A31BABBAD2827E5B166101C94DAF7724EEACABE56B4DE6AE47285DE.png)
    
2. 输入需要生成的页面主题及要求，或者使用快捷模板，勾选下方的行业领域和常用功能标签，或者直接上传一张页面参考图片。当前支持对美食、旅游、购物、新闻和教育五大垂域进行页面生成。点击![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155803.08904527358628733019814869069179:50001231000000:2800:47C994FE3A6912012DB2B6FF693238F68795E3BB648CA2F3A255F620F6B50F53.png)图标，等待生成完成。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155803.77671871858057631438708887700656:50001231000000:2800:C25C4BF276E15B53A1A3185BADF9C4A3E63EC8A57B163A897D1C5FB22849D28B.png)
    
3. 支持通过多轮对话新增或修改页面及页面中的关键字等具体信息，点击历史对话中的**回到本次**可以回退到之前的页面。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155803.42568713344840175533321964192921:50001231000000:2800:51C7D7DFCBF5333107048199BA4D24972F6AA49193E3C094E6771F6666D56125.png)
    
4. 点击**Save to Project**，在弹窗中设置页面名称及指定页面所保存的模块。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155803.73718004928772760402784802255135:50001231000000:2800:0BF1EA8EA6ACE5A0F40323FCA50E58D5CE2690DEDC31C4A1F6BB92937985A2F1.png)
    
5. 点击**Next**将生成的代码文件及资源保存至工程中。弹窗中绿色文件为新增，蓝色文件表示该文件存在更改，点击**Finish**完成添加。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155804.97941845046018337392857286423472:50001231000000:2800:5C44E8B0DC44AC1DD88629FB2ED0E8D538FC58DE5AF8568077C92C78B8C550C7.png)
    

[编辑区代码续写](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-code-continuation "编辑区代码续写")

[万能卡片生成](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-codegenie-service-widget "万能卡片生成")
# 万能卡片生成

更新时间: 2025-12-16 15:58

基于AI大模型理解开发者的卡片需求信息，通过对话式的交互智能生成HarmonyOS万能卡片工程。

从DevEco Studio 6.0.1 Beta1开始，在输入框新增卡片生成的入口。

## 使用约束

1. 建议从以下维度描述卡片需求：
    
    |   |   |   |   |
    |---|---|---|---|
    |**序号**|**建议描述维度**|**说明**|**举例**|
    |1|卡片用途|卡片的用途/业务场景，比如电商购物、娱乐、生活服务类等。|例如“电商购物卡片”、“娱乐类卡片”。|
    |2|卡片功能|卡片包含的组件，如图标、标题、按钮等。<br><br>组件的状态信息，如图标主题、标题内容、按钮显示的文字等。|例如“新品上市主标题”、“商品搜索按钮”、“热门电影子板块入口”等。|
    |3|卡片尺寸|HarmonyOS官网提供的四种卡片尺寸：1*2（微卡片）、2*2（小卡片）、2*4（中卡片）、4*4（大卡片）。<br><br>卡片尺寸为非必选项，AI会根据前两个维度描述的信息，智能选择效果最佳的尺寸。|例如“2*2尺寸的卡片”、“中卡片”等。|
    
2. 当前不支持在生成卡片预览图后，继续描述需求进行增量修改。

## 万能卡片生成

1. 点击页面右侧菜单栏CodeGenie图标，完成登录后，在对话区域输入"/"调出命令，选择**Service Widget**；或者在输入框左下角下拉框选择**Service Widget**，输入万能卡片的需求，并点击发送。开发者可以根据模型提示进行多轮交互，不断完善需求。
    
    DevEco Studio 6.0.0 Beta1之前的版本，请在对话区域下拉框中选择**Service Widget**后输入需求。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155804.90055281857429496579991497853291:50001231000000:2800:7BA4D0D217F3E3BCBE1AEE84095BFAF02D871EA81102AE828DDD4D2ADC701281.png)
    
2. 需求描述完成后，智能生成卡片（1~3张）及预览效果图。生成效果示例**：**
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155804.46862714473214117987143973612649:50001231000000:2800:EB9335F3CA865AB52A3CA5972A5DB35A2CA72D2C25E62C894D0646AEF615E9DF.gif)
    

## 万能卡片保存

1. 点击![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155804.35829114144451643615663106752318:50001231000000:2800:F108444F53BD392B810AE589F8457173B8B389B1201319C6B13CE63589EC2446.png)，可查看生成卡片的UI代码、配置信息和下载静态资源文件。
2. 保存卡片工程有两种方式：
    
    方式一：使用代码/配置查看窗口的“复制”、“插入”或“创建文件”等按钮，手动保存卡片代码和配置信息。
    
    方式二：点击“保存工程”按钮，自动保存卡片工程，卡片代码、配置、静态资源文件等会自动保存到工程对应目录中。默认勾选保存逻辑代码，逻辑代码用于配置卡片事件及卡片数据等信息，具体请参考[自定义配置逻辑代码](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-codegenie-service-widget#section17840955102711)。
    
    **流程示例：**
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155804.62144146362529816922158656797406:50001231000000:2800:E610221E3345282729B687938995DCF0AEF35DA16F8C444513D673A54A6FFF90.gif)
    
    工程保存完成后，工程中会新增如下卡片相关文件：
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155804.78669133311067880204280622134939:50001231000000:2800:354F4D1D07C2445641CB495852CEE3B19CE0FA888EBE03C3F56C44B355831640.png "点击放大")
    

## 自定义配置逻辑代码

逻辑代码包含实现卡片数据交互和卡片事件两类。

- 卡片数据交互：触发卡片页面刷新。应用工程生成的卡片数据交互，可通过数据库或网络请求两种方式来触发卡片页面刷新；对于元服务工程生成的卡片，数据交互为通过网络请求方式触发卡片页面刷新。
- 卡片事件：使用router事件跳转到指定的UIAbility、使用call事件拉起UIAbility到后台、使用message事件刷新卡片内容。

### 目录结构

在module > src > main > ets 路径下， formcommon目录用于存放生成卡片的逻辑代码。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155804.10801164919811015619983100975459:50001231000000:2800:DE1002E1C3697F5EAC60D926FC39D1CF4D9292218737AFD838E4195BA11B44B7.png "点击放大")

- formsetting：存放用户可配置的文件。
    - formsetting > formdbsetting：自定义配置以数据库方式进行卡片刷新的相关参数。
        - formdbsetting > formdbinfo：存放包含卡片信息的Info.ets文件，可在Info.ets文件中，添加卡片刷新所需要的具体的数据，后续会读取该文件并将数据存入数据库中。
        - UserSettings.ets：可以自定义卡片刷新时从数据库获取数据的规则、数据解析规则、message内容刷新规则。
    - formsetting > formhttpsetting：自定义配置以网络请求方式进行卡片刷新的相关参数。
        
        - formhttpsetting > formhttpinfo：存放包含卡片信息的Info.ets文件，可在Info.ets文件中添加获取卡片刷新数据的URL。
        - UserSettings.ets：可以自定义卡片刷新时从URL获取数据的规则、数据解析规则、message内容刷新规则。
        
        说明
        
        如需使用网络请求方式刷新卡片页面，需在EntryFormAbility.ets文件中将FormDbUpdate的接口注释掉，并将启用FormHttpUpdate接口。
        
    - formsetting > FormAction.ets：配置卡片事件。
- utils：存放工具类的目录，用户不可修改，如果修改再次生成逻辑代码时utils目录会被刷新。

### 自定义配置卡片事件

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155804.95144948463757429705539500984042:50001231000000:2800:FA243BC8ADA6E6EA3A535632CD394741E99D9166B31F2FC02D14E28592ED11AC.png)

1. 在FormAction.ets文件中，配置触发卡片router事件时具体的页面分发规则。

2. 在EntryAbility.ets文件的onWindowStageCreate方法中，会插入页面分发接口的调用，示例如下：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155804.57911601396064550514255247095175:50001231000000:2800:FDF1BD6C9F50C846FE40A79484DA0E516F9D4EA1B1F7B0191D13E28AD60B350E.png)

此接口默认插入到方法开头，可根据当前工程onWindowStageCreate逻辑来将此接口移动至合适的位置，保证页面能正常跳转。

[页面生成](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-page-generation "页面生成")

[单元测试用例生成](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ut-generation "单元测试用例生成")
# 单元测试用例生成

更新时间: 2025-12-16 15:58

根据选中的ArkTS方法名称，CodeGenie支持自动生成对应单元测试用例，提升测试覆盖率。

1. 点击页面右侧菜单栏CodeGenie图标，完成登录后，在ArkTS文档中，光标放置于方法名称上或框选完整的待测试方法代码块，右键选择**CodeGenie > Generate UT**，开始生成单元测试用例。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155804.58189234260664143023001615282197:50001231000000:2800:471D565DA709E8F59C2493919A7096320D4C17CF0DFE84774B66DC6BCC0FFC3C.png)
    
2. 在问答对话区生成单元测试用例后，点击回答代码中右上角的**New File**按钮，弹出文件另存为框，填写文件名称后点击**OK**按钮保存。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155804.48417628946510576210462323793328:50001231000000:2800:C0A9AA25CACA55DA34D4BB1DCDC3950C6FCDB39881B3BF77B8D362A90D7E98AF.gif)
    
3. 生成的单元测试用例文件被保存在待测函数所在模块下的**ohosTest/ets/test**目录，目录结构和待测函数保持一致。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155804.02601561430312160018211004122825:50001231000000:2800:176A28EC7E2E891AA090089D6DE2962C4EC3BDFDB6E22B22CC6005173F08A739.png)
    
4. 运行单元测试用例。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155804.65865040794601244859188435432121:50001231000000:2800:24870E85A580360D3BF40CFE0F5B7CA1FE389E74ED331566B0FB9EEAEAAAE3AB.gif)
    

说明

- 最多支持解读30000字符以内的代码片段。ArkUI代码、生命周期函数、@Extend/@Styles/@Builder修饰的函数、private修饰的私有函数不支持生成单元测试用例。
- 使用该功能需先完成CodeGenie登录授权，具体请参考[工具概述](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-codegenie)。

[万能卡片生成](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-codegenie-service-widget "万能卡片生成")

[代码智能解读](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-explain-code "代码智能解读")
# 代码智能解读

更新时间: 2025-12-16 15:58

CodeGenie提供智能AI能力对框选的代码片段进行逐条解释，总结代码段含义，帮助开发者提升阅读代码的速度和效率。

选中.ets文件或者.cpp文件中需要被解释的代码行或代码片段，右键选择**CodeGenie > Explain Code**，开始解读当前代码内容。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155805.96016815469775060135200038974101:50001231000000:2800:CBB61EB7830BAD7079EA92C1FD3942CA300655D264166CE664F547039FBA4FF3.png)

说明

- 最多支持解读30000字符以内的代码片段。
- 使用该功能需先完成CodeGenie登录授权，具体请参考[工具概述](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-codegenie)。

[单元测试用例生成](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ut-generation "单元测试用例生成")

[编译报错智能分析](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-compilation-error-analysis "编译报错智能分析")
# 编译报错智能分析

更新时间: 2025-12-16 15:58

当DevEco Studio构建ArkTS工程出现失败时，CodeGenie能够对错误进行智能分析，提供错误原因及修复方案，帮助开发者快速解决编译构建问题。

1. 如需开启编译报错智能分析和自动修复，进入**File > Settings**（macOS为****DevEco Studio > Preferences/Settings****） **> CodeGenie** **> General**页面，勾选**Enable AI-Fixed For Build Errors**和**Allow AI Edit Local File**。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155805.87378798198293053704839973701837:50001231000000:2800:8123C1DD59AC9511F2CBDCDE49AC8F472D6025950E0025837AAC58431E6CEDF1.png)
    
2. 当ArkTS工程出现构建报错时，点击报错信息后方**Add To Chat**图标，CodeGenie将自动引用构建报错信息，开发者可在输入框中选择对当前报错修复任务进行补充指令，帮助开发者进行定制化修复，使修复更准确，如"当前工程为API19工程，注意兼容性"，"不修改工程代码"，"仅需给出分析即可"，"不进行编译验证"等，点击或回车发送对话后，CodeGenie会分析该报错及开发者输入信息，并提供可能的错误原因，针对语法错误问题将参考开发者诉求，提供恰当的修复方案。
    
    若弹窗提醒"Please sign in to access DevEco CodeGenie"，请先登录CodeGenie后，再次点击**Add To Chat**图标查看解决方案。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155805.41088095566754345766119381494972:50001231000000:2800:45BED6F762B001F3D63950627D15BA760F1F5291DA3E6EB4E00E7845F6BEBC99.png)
    
3. CodeGenie分析后，点击编辑区**Accept**（或使用快捷键**Shift+Ctrl+Y**），接受AI提供的修复方案；或者点击**Reject**（或使用快捷键**Shift+Ctrl+N**）拒绝；或者点击右侧对话窗口中**Accept All****/Reject All**按钮，快速接受/拒绝所有修改。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155805.24915857193191497720506632914534:50001231000000:2800:CF75CC7DA1DD94D5132E5C5CDB53E4B4C0F1583640BE2495C83364FE8E4803CF.png)
    

[代码智能解读](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-explain-code "代码智能解读")

[智慧调优](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ai-profiler "智慧调优")
# 智慧调优

更新时间: 2025-12-16 15:58

DevEco Studio提供智慧调优能力，支持通过自然语言交互，分析并解释当前实例或项目中存在的性能问题，帮助开发者快速定位影响性能的具体原因。该功能从DevEco Studio 6.0.0 Beta1版本开始支持。

注意

从DevEco Studio 6.0.0.828版本开始，支持对Allocation内存分配问题和Snapshot内存堆快照问题进行智慧调优分析。

1. Profiler工具中已集成智慧调优能力，首次使用请先根据界面提示完成CodeGenie授权登录。当前支持两种开启方式：
    
    方式一：若Launch/Frame/Allocation/Snapshot模板已录制完成，点击Session窗口中该条会话上的![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155805.35234527929513430807148546521824:50001231000000:2800:F7D727DE50787C32F8265BD0D7E54A6BD6C8F1CD319531FB1CE17B92C6108ED4.png "点击放大")图标，开始智慧调优分析。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155805.10383760938255574165008128711002:50001231000000:2800:8807B5E0A37C9EA4AFD918FDE479E74A37B9D911A2E2D2137B96227688E99A2E.png "点击放大")
    
    方式二：切换到Assistant窗口，点击**Create Session**/**Open File**按钮，录制新调优任务或导入已有的调优数据文件。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155805.81101724002952657210812741091995:50001231000000:2800:0522A6FBDE8ACA4A4F7A6B11B5730A7958014ED8BE9C3647618EE963D37780E2.png "点击放大")
    
2. 以第二种创建方式举例，在Assistant页面，点击**Create Session**按钮，选Launch/Frame/Snapshot/Allocation分析模板。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155805.04361089090032195212060526373143:50001231000000:2800:8216AC50C2591A34757ADFC3B6685BB573F62E245AEC30EF75768C1EEB31A664.png "点击放大")
    
3. 录制新的调优任务或导入本地已有的调优数据文件，当前支持导入的文件类型包括.insight、.heapsnapshot、.rawheap。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155805.24225919991108103607072020576081:50001231000000:2800:D48C3030B43A6B7B1590BCEF89E28AD2ED6D08D20B8B74340582126FA5D6D64E.png "点击放大")
    
4. 等待AI分析完成各阶段耗时情况。可以左键选中阶段名称，点击**Analyze**，进一步分析该阶段的具体耗时信息，或点击**View Lane**，在右侧查看具体的泳道信息。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155805.25098554667601581757821277397564:50001231000000:2800:980A88F9C08A288391796B9013C0D1E6659786578E4354AFB3C11821AE358FA5.png "点击放大")
    
5. 点击分析后，逐步深入挖掘当前阶段具体耗时场景，找到影响性能的可能原因。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155805.72361926648401147213882971825973:50001231000000:2800:743138E91935FF333CA93FC27BD850F7AA05A08B6BE28AD3E80BBBED78D2C2B5.png "点击放大")
    
6. 若使用Snapshot模板对堆快照问题进行分析时，支持在对话框中选择单个Snapshot分析，或选择两个Snapshot进行对比分析。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155805.12622100829178607716521714909258:50001231000000:2800:8B11FBE21B6D5CE7034EB7FDF2B7C4E32E23B6758570F5FE01D48DB005064C99.png "点击放大")
    

[编译报错智能分析](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-compilation-error-analysis "编译报错智能分析")

[应用UI生成](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ui-generator "应用UI生成")
# 应用UI生成

更新时间: 2025-12-16 15:58

UI Generator用于快速生成可编译、可运行的HarmonyOS UI工程，支持基于已有UI布局文件（XML），快速生成对应的HarmonyOS UI代码，其中包含HarmonyOS基础工程、页面布局、组件及属性和资源文件等。

## 使用约束

建议使用DevEco Studio 5.0.3.700及以上版本。

## 启用插件

1. 在DevEco Studio菜单栏，点击**File > Setting****s...**（macOS为**DevEco Studio > Preferences****/Settings**）**> Plugins**，在Installed列表中找到UI Generator插件，点击**Enable**启用。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155806.65548821931489775039081818297163:50001231000000:2800:6BCBBC7A0309FAAA5BCEC0383FD8252147B98EABC45EF1F297FF13F0DFD121A5.png "点击放大")
    
2. 单击OK并关闭设置窗口，插件启用成功。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155806.29020442165300382579783289771299:50001231000000:2800:447DBD4EB6C69D6A1D865054BBC24997D8580C85F6864F6D1F5F2BC177054D7A.png "点击放大")
    

## 开始使用

1. 在菜单栏点击**Tools > Generate Project From...**打开UI Generator工具，首次使用需要阅读并确认用户协议，确认后可继续使用。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155806.36835105630323132017740937405033:50001231000000:2800:A3D20C528EE918E4FC82543F9AC6F6A57442354413D0425BD84638B7C134F5C4.png "点击放大")
    
2. 输入待配置项路径，点击Next进入下一步。
    
    |待配置项|说明|
    |:--|:--|
    |Installation package path|待转换的APK应用包的路径，请提供未混淆的Debug版本应用包。|
    |SDK path|等于或高于编译应用包所使用版本的SDK路径。|
    |Git Bash path|Git Bash工具存放路径。若本地已下载安装Git Bash，插件将自动获取其路径。|
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155806.61847163293808862209395233027530:50001231000000:2800:ABFAC713CDC88064B7E1C1C5CE8FD669BC4012E4758D761F931EFC2F471BC933.png "点击放大")
    
3. 选择将要生成的XML页面（可在搜索框进行搜索），勾选后点击向右箭头将选中的XML导入至右侧。点击Next开始生成。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155806.81765957574090974635749425889051:50001231000000:2800:2A6FA1B9B9F3E0EE2F9CFE45E8572925AE5570052839168E965D5BD673252238.png)
    
4. 配置输出工程待配置项，点击Finish进行生成。
    
    |待配置项|说明|
    |:--|:--|
    |Destination Path|生成新工程的保存路径(默认生成到用户目录下UIGenerationProjects，用户可根据需要自行更改)|
    |Compatible SDK|生成的新工程所使用的SDK版本|
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155806.71006940814728895865445451042970:50001231000000:2800:62BBAB6EFC70D5B963EC27611F0C47326E113A415868BBB956A7CA3026F12276.png)
    
5. （可选）如果所选XML无有效根节点，需要选择根节点信息。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155806.93572008742751576314494398250302:50001231000000:2800:4AE776E9FE5D832240815925896C6F0C9DD2212DF487D7E514421373F1AA9370.png)
    
6. 点击Finish，在弹窗中点击确认，打开新工程，生成的页面位于entry > src > main > ets > pages目录下，可以在Previewer中查看页面预览效果。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155806.89903223845725357685691263378137:50001231000000:2800:B3333EDEE94ED979E0701EDEFD9F15CEAB689366A940068DD5CFC69D31D0D12A.png)
    
7. 生成的新工程内的entry > src > main > resources目录包含文本、图像、颜色资源。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155806.91528662809782029651008474714580:50001231000000:2800:B6F9272419EBF5CB3A9951F7924E5CB7DEFCDA6FCBC82FDD76AEE796073B6FD0.png "点击放大")
    
8. 不支持生成的组件、属性会以注释的形式给出，方便后续定位修改。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155806.40399654418658014039619211567614:50001231000000:2800:E7C2BBC55F608727BCFBBA274D8FA866E9CDC867F9ECBADB670F552A56687755.png)
    
    更多操作指导，请参考视频课程：[毕方HarmonyOS UI代码生成工具](https://developer.huawei.com/consumer/cn/training/course/live/C101731322888995220)。
    

[智慧调优](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ai-profiler "智慧调优")

[意图装饰器生成和小艺智能体创建](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-insight-intent2 "意图装饰器生成和小艺智能体创建")
# 意图装饰器生成和小艺智能体创建

更新时间: 2025-12-16 15:58

通过装饰类或方法可以将应用的功能定义为"意图"，然后将应用功能以"意图"形式集成至系统入口。用户通过系统入口（如语音助手、智能推荐卡片）触发意图执行，即可便捷使用应用提供的功能。

从DevEco Studio 6.0.0 Beta2开始，CodeGenie支持生成意图装饰器，帮助开发者更快更高效的将功能转换为意图和生成智能体。

## 使用约束

- 使用API 20及以上版本。
- 仅支持使用团队账号登录时，添加意图插件。个人加入目标团队方式具体可参考[添加成员](https://developer.huawei.com/consumer/cn/doc/app/agc-help-manageaccount-0000002306610129#section151241455193313)。
- 应用在AGC已注册，具体可参考[创建HarmonyOS应用](https://developer.huawei.com/consumer/cn/doc/app/agc-help-create-app-0000002247955506#section1772711713288)。

## 意图装饰器分类

CodeGenie提供了几类意图装饰器，开发者可根据业务场景进行选择，具体请参考[意图装饰器定义](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-app-ability-insightintentdecorator)：

- @InsightIntentLink装饰器：在class头部或内部位置唤起意图装饰器，在class上方插入生成的代码。
- @InsightIntentPage装饰器：在@Component头部/struct结构体内部/选中整个结构体区域唤起意图装饰器，在@Entry上方插入生成的代码。
- @InsightIntentFunction装饰器：在类中静态方法区域唤起意图装饰器，在class上方插入@InsightIntentFunction，在class内部插入@InsightIntentFunctionMethod生成内容。
- @InsightIntentForm装饰器：在继承FormExtensionAbility的class头部或内部唤起意图装饰器，在class上方插入生成的代码。
- @InsightIntentEntry装饰器：在直接继承InsightIntentEntryExecutor的class头部或内部唤起意图装饰器，在class上方插入生成的代码。

### @InsightIntentLink装饰器

1. 打开module.json5文件，配置**abilities > skills > uris**字段。uri格式要求请参考[应用链接说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-uri-config)。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155806.33065984050088490227713560840678:50001231000000:2800:138558112D0AE45ABEE7345614E2452D7D452E898620CE2C865E4964C65A53E9.png "点击放大")
    
2. 在class头部或内部位置，右键选择 **CodeGenie > Insight Intent > Link Insight Intent**。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155806.82555913484651378064251145444946:50001231000000:2800:1F809ED4A3930E96ED5B4E325D31541C5251D3263C3ED3153655793C49B218C3.png)
    
3. 意图装饰器自动添加至CodeGenie对话框中，可选择输入或不输入提示词，CodeGenie根据代码上下文分析输出结果。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155806.63963707222217156253896194863685:50001231000000:2800:998EA935240AA6BB37B7D15D173E6FCDD0CA0D96BFE5E0E1E05C77CB6684E395.png)
    
4. 生成结果后，点击对话框中生成代码块右上方的**插入**按钮，在class上方插入生成的代码。开发者可基于结果微调，实现意图调用。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155807.35670137631711494841621915722723:50001231000000:2800:119E5B2C66FDF6E91E2323C6BBADCBB3AB12C05D773E0C73D97447FF9A59A613.png)
    

### @InsightIntentPage装饰器

基于组件导航（Navigation）的子页面使用，@Component和struct需成对出现。

1. 在@Component头部\struct结构体内部\选中整个结构体区域，点击**右键 > CodeGenie > Insight Intent > Page Insight Intent**。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155807.35095075088180508719231688808997:50001231000000:2800:5597BF6ED3B79069EF0E2DF6819429A9A85E760F374C088ABABFBE9507745CEE.png)
    
2. 意图装饰器自动添加至CodeGenie对话框中，可选择输入或不输入提示词，CodeGenie根据代码上下文分析输出结果。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155807.02534056947231919644753525146411:50001231000000:2800:D79B0A6D2E7CFB171B45675AD7BC15E2FC6D8380001F65F4CDA022BAAEF1AEA3.png)
    
3. 生成结果后，点击对话框中生成代码块右上方的**插入**按钮，在@Entry上方插入生成的代码。开发者可基于结果微调，实现意图调用。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155807.26863884269662202062138888007035:50001231000000:2800:410B410043370C6BD33F12180D6460D1D12218E986C1E6BB224DEDD92B8E901B.png)
    

### @InsightIntentFunction装饰器

1. 在类中静态方法区域，右键选择 **CodeGenie > Insight Intent > Function Insight Intent**。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155807.15216303037582487298566006119979:50001231000000:2800:00A1437B1AB6F01F7937C79FB5FD9460A6E8925DC1C528994253CCDF6A9345EC.png)
    
2. 意图装饰器自动添加至CodeGenie对话框中，可选择输入或不输入提示词，CodeGenie根据代码上下文分析输出结果。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155807.73284059339527546233242898186690:50001231000000:2800:874C2E2E8D05DC0FDB20F73A7945BD1D791FBCBC5E4F976024EDAAA1CBAE7B68.png)
    
3. 生成结果后，点击对话框中生成代码块右上方的**插入**按钮，在class上方插入@InsightIntentFunction，在class内部插入@InsightIntentFunctionMethod生成内容。开发者可基于结果微调，实现意图调用。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155807.43909362706923728873831737863635:50001231000000:2800:08E91ABB98830362FEA03F16D3AD0160E91EEB1C7763D3BCE1EAB4A95F955A0E.png)
    

### @InsightIntentForm装饰器

1. 基于FormExtensionAbility使用，在继承FormExtensionAbility的class头部或内部，右键选择**CodeGenie > Insight Intent > Form Insight Intent**。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155807.38579495238505551731665022758021:50001231000000:2800:D76C13A0B5B8ADFAB59328302566B8F0917FD7BE5448D1229A1EEDF0AAAE50E2.png)
    
2. 意图装饰器自动添加至CodeGenie对话框中，可选择输入或不输入提示词，CodeGenie根据代码上下文分析输出结果。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155807.28739640547581607007584441177248:50001231000000:2800:F2D1969174C3E0C3333945B578FD4184E7C698189D7E746D622F97264C1F3DA6.png)
    
3. 生成结果后，点击对话框中生成代码块右上方的**插入**按钮，在class上方插入生成的代码，开发者可基于结果微调，实现意图调用。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155807.17824952255263923627040546956538:50001231000000:2800:92D892750EAD40AD527D60C05FBBD9283EC9D594722926F9F7BB4585E0F39ABB.png)
    

### @InsightIntentEntry装饰器

1. 基于InsightIntentEntryExecutor使用，在直接继承InsightIntentEntryExecutor的class头部或内部，右键选择**CodeGenie > Insight Intent > Entry Insight Intent**。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155807.58917673732246176174052344209283:50001231000000:2800:1450BE85DFB0AEE6131B325AB15A5B21120268F7F6E701DCC1FFEC5E1A8E680A.png)
    
2. 意图装饰器自动添加至CodeGenie对话框中，可选择输入或不输入提示词，CodeGenie根据代码上下文分析输出结果。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155807.93467728469808293218069467921452:50001231000000:2800:19E73F1F774794FDD490699A3BE6B0E08836119D4B5B497E08A75C19B4684E04.png)
    
3. 生成结果后，点击对话框中生成代码块右上方的**插入**按钮，在class上方插入生成的代码，开发者可基于结果微调，实现意图调用。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155808.84508538687129574652931001753755:50001231000000:2800:29BDA7701B0736A5B00616125B8AC924503E2061DC597C3060559CD666FB5185.png)
    

## 添加意图插件和创建小艺智能体

1. 点击DevEco Studio右上角![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155808.15857181349897981734041890509106:50001231000000:2800:31548AA78CA90B319EED0B8D532E60367C96C061C71373EFF3E0CD361F0E0600.png)图标登录个人账号，再切换至个人所在的团队账号。
    
    说明
    
    - 个人账号需要完成实名认证，具体请参考[实名认证](https://developer.huawei.com/consumer/cn/doc/start/rna-0000001062530373)。
    - 如下企业开发者账号为某团队账号名称。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155808.40324293909717114140832920420276:50001231000000:2800:EA1529D029F6D442983BF17455BECD31858344C07C03138FEE1BEF616D9548E7.png)
    
2. 在意图注解代码块内部任意位置，右键选择**CodeGenie > Add Intent Plugin**。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155808.77229017168783685583863824857045:50001231000000:2800:A98161EA96FFBAC2191AC83ACB2AFBD26CADFB7D245413C3CEFBD7B13850F4EF.png)
    
3. 在DevEco Studio菜单栏点击**View > Tool Windows > Application Agent** ，打开内嵌的小艺智能平台。
4. 在小艺智能体平台[创建智能体](https://developer.huawei.com/consumer/cn/doc/service/quick-start-0000002469548009)，[内嵌插件](https://developer.huawei.com/consumer/cn/doc/service/develop-plug-ins-0000002435989648)，连接[真机测试和调试](https://developer.huawei.com/consumer/cn/doc/service/list-of-user-groups-for-real-machine-testing-0000002471264273)。更多具体操作可参考[鸿蒙智能体](https://developer.huawei.com/consumer/cn/doc/service/developer-guide-0000002469667881)。

[应用UI生成](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ui-generator "应用UI生成")

[模型上下文协议（MCP）配置和自定义智能体创建](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-mcp-agent "模型上下文协议（MCP）配置和自定义智能体创建")
# 模型上下文协议（MCP）配置和自定义智能体创建

更新时间: 2025-12-16 15:58

从DevEco Studio 6.0.1 Beta1开始，CodeGenie支持用户添加模型和自定义Agent，增强AI问答能力，提升AI辅助编程和分析能力。自定义过程包括模型上下文协议（Model Context Protocol，简称MCP）配置、模型（Model）配置、智能体（Agent）配置和调用。

## MCP配置

为确保MCP Server正常启动，需要安装npx和uvx。其中，npx依赖于Node.js，建议使用Node.js的LTS版本；uvx是基于Python的快速执行工具，建议安装Python 3.9 以上的版本。

1. 点击页面右侧菜单栏CodeGenie图标，完成登录后。点击界面右上方**Settings**![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155808.79399837734290294833106434943741:50001231000000:2800:AFDED3C4AC7C47AC53DB518B25B6C7297BBEF4B47E6361F80411D1AEFED4DEFA.png)按钮，选择**MCP** **Settings**，进入配置页面。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155808.72660631895507192962116546701328:50001231000000:2800:17BEF967BD1A361C75DD2D1100629A7D95D34C43B622264D33CD7E562916C5B7.png)
    
2. 点击![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155808.29998127211795055766087488504231:50001231000000:2800:B73278B632E97C910F689CF2EEA45A1D810E183605542F662C473FD7B804768A.png)按钮，添加MCP工具。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155808.12754286381992009003692392882986:50001231000000:2800:965E424A9DA089B51398B93FD3CAFAB4DD113DD3CE9F375E70637414C09B9A84.png "点击放大")
    
3. 在编辑框中填写MCP工具的配置信息，填写完成后点击**Add**。
    
    说明
    
    MCP Server支持三种通信方式：Stdio 、Server-Sent Events (SSE) 和Streamable HTTP。
    
    Stdio方式支持配置cmd、args和env字段，SSE和Streamable HTTP方式支持配置url字段。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155808.27917168930654885591243118130236:50001231000000:2800:A33F87438FF9A67C5F869CD350460B29D24B8CFFFF3D87BF036D720CE544139A.png "点击放大")
    
4. 在**Added Tools**列表中，展示所有MCP工具信息，包括名称、连接状态、启用状态。同时，将鼠标悬浮在工具上会显示三个操作按钮：刷新、编辑和删除，方便开发者管理工具。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155808.38728420778932256562179803343110:50001231000000:2800:2CA96EF2377DE64FB52D2B4B0F3A4B7308C437D2EB74BD16B573AFCE9D49B90F.png "点击放大")
    
    - 名称：MCP工具名称，如Context7、Time。
    - 连接状态：工具连接状态，包括“成功”、“失败”和“连接中”三种状态。
    - 启用状态：工具是否已启用。
    

## 模型配置

CodeGenie支持通过OpenAI-API协议接入第三方模型，为自定义Agent提供多样化的模型选择。

1. 点击界面右上方**Settings**![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155808.89588830110483455802059875260347:50001231000000:2800:7E3FAD47287D0B0AB81E1AB483F2D36084F9B112582228C5FB53E8CC3DA43711.png)按钮，选择**Model Settings**，进入配置页面。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155808.79371217749344070943109623835473:50001231000000:2800:02A403C096D79A9F4A0E33024D1DAB5AF495873FFFF757B85A999CEDF3C0803D.png "点击放大")
    
2. 点击![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155808.36145489045709924364923767747550:50001231000000:2800:E1A70EBDFCE2893659ED428A2EC919227C0B70DF5BBD413D569131CFE91B9EF4.png)按钮，填写相关信息。点击**Add**，校验成功的模型将被添加到列表中。
    
    - **Name**：模型名称。
    - **Url**：模型的访问地址。
    - **API Key**：模型的访问密钥。
    - **Model**：模型的标识。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155808.20387206560223675924646379807912:50001231000000:2800:BBBAF771C7DA06BECBF52F611D333B9626E743383C5054749B31AC382B273806.png "点击放大")
    
    说明
    
    当前仅支持添加遵循OpenAI-API规范的模型。
    
3. 在**All Models**下展示所有添加成功的模型。将鼠标悬浮在模型上会显示两个操作按钮：编辑、删除，方便开发者管理模型。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155809.39713896236722942826058444571162:50001231000000:2800:B2A3104E15B5B85459E118E524B0BB1FEED3FFA658EB512FA2D84D7C8270710F.png "点击放大")
    

## Agent配置

1. 点击界面右上方**Settings**![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155809.58835943038554794215058497982761:50001231000000:2800:3E6ACB5833038E4F5E5258D4622C6FABD476254FD128E371A35A4F471D338A2C.png)按钮，选择**Agent** **Settings**；或者在输入框左下角下拉框选择**Create Agent**，进入配置页面。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155809.64747677277233396695727713625717:50001231000000:2800:212C27D8B7DF176E193A08BE8B518D2BF9FE5139D6B24F589FCB4DCD4009257E.png)
    
2. 点击![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155809.59423524774716222886173917598028:50001231000000:2800:5525271F8F8CC6410BE4FAB45312034218611DCA9AEDE992C27C8A9862018FDD.png)按钮，填写自定义Agent的相关信息。点击**Add**，将创建自定义Agent。
    
    - **Name**：必填，自定义Agent的名称。
    - **Prompt description**：可选，自定义Agent的提示词。
    - **Added Tools**：可选，添加MCP工具。具体请参考[MCP配置](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-mcp-agent#section1918313413580)。
    - **Select Model**：必填，选择需要使用的模型。具体请参考[模型配置](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-mcp-agent#section13929843125813)。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155809.51923835524154178334624660575775:50001231000000:2800:9104D99B8883B283A9D38EC6B94F83DC297E5F7AD20B10FE8B9F420E785B9020.png "点击放大")
    
3. 在**All Agents**下展示所有内置（HarmonyOS Ask、Generate UI Code、Service Widget）和自定义的Agent（如figma2code）。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155809.54389600254228336148663334075469:50001231000000:2800:7396C93733D4B858A59093D924A520C79B669A7C6B86F65BC1154CF4D86867F6.png "点击放大")
    

## Agent调用

1. Agent配置完成后，在对话区域输入"/"调出命令，选择自定义的Agent（如figma2code）；或者在输入框左下角HarmonyOS Ask处下拉框中选择自定义的Agent（如figma2code）。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155809.71077672159407185925065722746287:50001231000000:2800:2FADAFF58608890A48D16E2B3B48D71A230EDC3B54490F0BC18FCB94F34DCDB5.png)
    
2. 选择自定义的Agent后，在右侧可以切换模型，默认使用[配置Agent时添加的模型](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-mcp-agent#li163941335173012)。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155809.94486940142222648384336974722185:50001231000000:2800:BE69898F6DD06241EC15ED263FF11DC89420512E79E9A334910735648E10B46C.png "点击放大")
    
3. 根据业务需要，进行智能问答、代码生成、代码智能解读等，CodeGenie将会调用自定义的Agent和选择的模型生成内容。若Agent已添加MCP工具，界面会有授权弹框。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155809.35107141411565079387258108313090:50001231000000:2800:8BD8BC3C75CCFF5D3A1A17361C50709C100BA4E4EB99B4DFD90375B0C872744B.png "点击放大")
    

[意图装饰器生成和小艺智能体创建](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-insight-intent2 "意图装饰器生成和小艺智能体创建")
# 代码阅读

更新时间: 2025-12-16 15:58

DevEco Studio支持使用多种语言进行应用/元服务的开发，包括ArkTS、JS和C/C++。在编写应用/元服务阶段，可以通过掌握代码编写的各种常用技巧，来提升编码效率。

## 代码高亮

支持对代码关键字、运算符、字符串、类、标识符、注释等进行高亮显示，您可以打开**File >** **Settings**（macOS为**DevEco Studio > Preferences/Settings**）面板，在**Editor > Color Scheme**自定义各字段的高亮显示颜色**。**默认情况下，您可以在**Language Defaults**中设置源代码中的各种高亮显示方案，该设置将对所有语言生效；如果您需要针对具体语言的源码高亮显示方案进行定制，可以在左侧边栏选择对应的语言，然后取消“Inherit values from”选项后设置对应的颜色即可。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155813.55793846381857229995764470701701:50001231000000:2800:2E5A5B7CCCDF50FBB0913644C497D5FD761C47EDD8C22A2EBA9A7E01A645E90C.png)

## 代码跳转

在编辑器中，可以按住**Ctrl**键（macOS为**Command**键），鼠标单击代码中引用的类、方法、参数、变量等名称，自动跳转到定义处。若单击定义处的类、变量等名称，当仅有一处引用时，可直接跳转到引用位置；若有多处引用，在弹窗中可以选择想要查看的引用位置。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155813.63618931333778065962535257173942:50001231000000:2800:D65FA585C661144E7EF6581C9AE49ADCBB8939ACC16DCF5B548223D830A9D910.gif)

## 跨语言跳转

DevEco Studio支持在声明或引用了Native接口的文件中（如d.ts）跨语言跳转其对应的C/C++函数，从而提升混合语言开发时的开发效率。您可以选中接口名称单击右键，在弹出的菜单中选择**Go To > Implementation(s)**（或使用快捷键**Ctrl+Alt+B**，macOS为****Command**+Option+B**）实现跨语言跳转。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155813.71373681220834104557178323945009:50001231000000:2800:A4B180BC62EA5032C313C04F19B5BB10A96587F04FF9CC0998441175B7A0FFA9.png)

## 代码格式化

代码格式化功能可以帮助您快速的调整和规范代码格式，提升代码的美观度和可读性。默认情况下，DevEco Studio已预置了代码格式化的规范，您也可以个性化的设置各个文件的格式化规范，设置方式如下：在**File > Settings > Editor > Code Style**（macOS为**DevEco Studio > Preferences/Settings > Editor > Code Style**）下，选择需要定制的文件类型，如ArkTS，然后自定义格式化规范即可。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155813.16329194822549896992039190206755:50001231000000:2800:7EE5F89906F25DAFE4EF2A67B655D2495976013C9E227D42823E6536DA95F8C6.png)

在使用代码格式化功能时，您可以使用快捷键**Ctrl + Alt + L**（macOS为**Option+Command +L**） 快速对选定范围的代码进行格式化。

如果部分代码片段不需要进行自动的格式化处理，可以通过如下方式进行设置：

1. 在**File > Settings >Editor > Code Style**（macOS为**DevEco Studio > Preferences/Settings > Editor > Code Style**），单击“Formatter”，勾选“Turn formatter on/off with markers in code comments”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155813.09996085863851917698354522404883:50001231000000:2800:342549C2864DE419C1D19195A56D1B05DB8E5F65E9EE215AF100F16B79E789E9.png)
    
2. 在不需要进行格式化操作的代码块前增加“//@formatter:off”，并在该代码块的最后增加“//@formatter:on”，即表示对该范围的代码块不需要进行格式化操作。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155814.22904740543453308084488360797272:50001231000000:2800:FB28E4BA87FB2C617BC4B06278C6163BF4AAA78264ABE82977D7AD6CD6495936.png)
    

若工程已配置code-linter.json5文件，选中code-linter.json5文件右键选择**Apply CodeLinter Style Rules**，代码格式化规则将与已配置的code-linter.json5文件中相关规则保持一致。code-linter.json5文件配置请参考[配置代码检查规则](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-code-linter#section19310459444)。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155814.13962796186983438671513957543316:50001231000000:2800:98BABFFE420232661D5E0C2BD2066748CDCF5D968E7932C352D9903DAF6DAC21.png)

## 代码折叠

支持对代码块的快速折叠和展开，既可以单击编辑器左侧边栏的折叠和展开按钮对代码块进行折叠和展开操作，还可以对选中的代码块单击鼠标右键选择折叠方式，包括折叠、递归折叠、全部折叠等操作。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155814.54123183833636914569587723128581:50001231000000:2800:D9BB4398F09A2388A0D37E9D5945AE14224D0039A402ECF74C7523C28484139A.gif)

## 代码快速注释

支持对选择的代码块进行快速注释，使用快捷键**Ctrl+/**（macOS为**Command+/**）进行快速注释。对于已注释的代码块，再次使用快捷键**Ctrl+/**（macOS为**Command+/**）取消注释。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155814.52269967820794203328067030953752:50001231000000:2800:0F6A7A0846CBA0EA411BE7B088081A2BA714210900392B5E5A3A12C11E8F101A.gif)

## 代码结构树

使用快捷键**Alt + 7 / Ctrl + F12**（macOS为**Command+7**）打开代码结构树，快速查看文件代码的结构树，包括全局变量和函数，类成员变量和方法等，并可以跳转到对应代码行。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155814.33802706465282221407810978599664:50001231000000:2800:0C4C9A37A804F7DC37B434EE5CAC7C228CC2D6ACD495982B038B1F2210763FCB.png)

## 代码引用查找

提供Find Usages代码引用查找功能，帮助开发者快速查看某个对象(变量、函数或者类等)被引用的地方，用于后续的代码重构，可以极大的提升开发者的开发效率。

使用方法：在要查找的对象上，单击鼠标**右键 > Find Usages**或使用快捷键**Alt +F7**（macOS为**Option +** **F7**）。可点击![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155814.43850679545629570757025215534062:50001231000000:2800:20B1E8C6AE383D2BB56111FAD7528F54E6DBB74F5058912F86FCF4BDCC8D4677.png)图标查看变量赋值位置，点击![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155814.40350248621917781363483225098225:50001231000000:2800:D2F6589FC4C75657C7467E848D462E6839448864B47FD7A2C68EA819269E9FA5.png)图标查看变量引用情况。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155814.61072211834754943629298177686677:50001231000000:2800:5025D22258734F1BA5FC23FD902596D50C7453D249D7A0E892FC57377E47876A.png)

## 函数注释生成

DevEco Studio支持在函数定义处，快速生成对应的注释。在函数定义的代码块前，输入**“/**”+回车键**，快速生成注释信息。

说明

C++文件同时支持使用**“//!”+回车****键**快速生成注释。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155814.95964021375914694526768466349311:50001231000000:2800:08704FD6805A1F0C03CC1C20BF84C37DE34D6FA543CCDDC51FA870430BA6595C.gif)

## 代码查找

通过对符号、类或文件的即时导航来查找代码。检查调用或类型层次结构，轻松地搜索工程里的所有内容。通过连续点击**两次****Shift**快捷键，打开代码查找界面，在搜索框中输入需要查找内容，下方窗口实时展示搜索结果。单击查找的结果可以快速打开所在文件的位置。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155814.70392028919436437928141141124049:50001231000000:2800:A316310F1B0E185611A2547D5825F07B552236E30D179AC9FD420AB6BB196C04.png)

## 快速查阅API接口及组件参考文档

在编辑器中调用ArkTS/JS API或组件时，支持在编辑器中快速、精准调取出对应的参考文档。

可在编辑器中，鼠标悬停在需要查阅的接口或组件，弹窗将显示当前接口/组件在不同API版本下的参数等信息，单击弹窗右下角**Show in API Reference**，或选中接口或组件，右键点击**Show in API Reference**，可以快速查阅更详细的API文档。

说明

DevEco Studio集成了离线版API参考类文档，最新版本请参考官网[HarmonyOS API参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/development-intro-api)。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155814.06619960316746808765756248835690:50001231000000:2800:75205A62010B2D88BAAB6091340490C12A8100D77E23D7B45A20B25F92C69344.gif)

在弹窗中可以查看：

1. 使用的API是否涉及权限申请或仅支持在测试框架下使用。
2. 使用的接口状态。**deprecated**标签表示即将废弃的API接口，可使用**useinstead**标记的API进行替代，请开发时关注。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155814.60722823309940392536618142657986:50001231000000:2800:257A73F7232BB0945CC31920F65E3EBB3F345D5DAF30B489053EC8233DDCD840.png)

## Optimize Imports功能

使用编辑器提供的Optimize Imports，可以快速清除未使用的import，并根据设置的规则对import进行合并或排序。选择文件或目录，使用快捷键**Ctrl+Alt+O**（macOS为**Control+Option+O**），或单击菜单栏**Code > Optimize Imports**。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155814.04417644980725135208750315860957:50001231000000:2800:556D17B8F9B8706DBC572F85BBE54FF9C3368D3C9D50F8304B9097572F980D72.gif)

如需修改优化配置，进入**File > Settings**（macOS为****DevEco Studio > Preferences/Settings****） **> Editor > Code Style**，选择开发语言（当前以ArkTS为例），在**Imports**标签页中，可选择在优化时是否需合并来自同一模块的import，是否需要对同一条import语句导入的元素进行排序，或对多条import语句按模块排序。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155814.49274950250803798012018561868665:50001231000000:2800:EF12505FBE1784E3134709D989E7DCF1B196670D99A1AC742AC6E123432A6F8E.png)

## API变更查询

从DevEco Studio 5.1.0 Release版本开始，DevEco Studio中支持查询、对比从某个选定的SDK版本开始，当前工程中使用到的ArkTS API是否存在行为变更，并提供相应适配指导链接，帮助开发者完成工程代码适配修改。

从DevEco Studio 5.1.1 Release版本开始，支持对C API的变更情况进行查询，提供跨版本查询能力。

### 使用约束

- API废弃情况不在API变更查询的扫描范围。
- ArkTS API函数调用过程中，当开发者使用的API存在泛型参数和包含extends或keyof关键字时，不支持变更查询。示例如下：
    
    1. // API定义
    2. interface ProgressInterface {
    3.   <Type extends keyof ProgressStyleMap>(options: ProgressOptions<Type>): ProgressAttribute<Type>;   //包含extends或keyof关键字不支持变更查询
    4. }
    5. // API调用
    6. Progress({ value: 10, type: ProgressType.Capsule })
    7. .style({content:'Install'})
    

- 使用C++语法实现的API函数变更时不支持查询。示例如下：
    
    1. template <class _Rep, class _Period>
    2. cv_status condition_variable::wait_for(unique_lock<mutex>& __lk,const chrono::duration<_Rep, _Period>& __d)  //C++语法实现的API函数不支持查询
    
- 特殊调用方式下，不支持API变更查询。示例如下：
    
    1. // 反例：函数指针方式
    2. int (*sigptr)(int, const struct sigaction *__restrict, struct sigaction *__restrict) = &sigaction;
    3. sigptr(NULL,NULL);
    4. // 反例：回调方式
    5. callback(sigaction);
    6. // 反例：自定义宏
    7. #define MySig sigaction
    8. MySig(NULL,NULL);
    

### 操作步骤

**使用DevEco Studio 6.0.0 Release及以上版本，按以下步骤操作：**

1. 在菜单栏点击**Tools > API Change Assistant**，编辑区下方的API Change Assistant页签中，支持按模块查看API变更情况，选择需要对比的SDK版本号范围，点击**Start Scan**开始扫描。
    
    说明
    
    API变更查询以选择的起始版本为基线，查询当前工程中所使用的API是否存在行为变更。如选择的SDK版本为5.0.0(12) Release 到 6.0.0(20) Release，查询的是5.0.1(13) Beta3到6.0.0(20) Release版本相比5.0.0(12) Release的API变更。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155814.04823140067382971162881224238984:50001231000000:2800:297A7139514707B6FDF6518361FDB7DF02F2B7F1A1364DB1B60EEB7382BDAA0A.png)
    
2. 点击扫描结果中的代码地址，跳转到相应的代码编写位置；如需更多指导可点击![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155815.81927884384662294176258282236091:50001231000000:2800:47FF2AE287E04D5E1287600F1DEBBFF0AF0AC667181E54B2A84608AE4D95AE64.png)链接图标，跳转至版本说明文档中查看详情；修改完后可点击![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155815.49544952359884277714712367607618:50001231000000:2800:DB35FCE855A9C4415C5DD036580DBC4D8A79CA2557C74D9A1DDF3A6C814AD4C0.png)图标，标注已修改。同时，可通过如下入口搜索或筛选API变更扫描结果、导出扫描结果数据等。
    
    - **Search**：支持在Search框中输入API名称或文件路径，对扫描结果搜索。
    - **API Version**：通过选择API版本，对扫描结果筛选。
    - **Language**：通过ArkTS或C语言，对扫描结果筛选。
    - **API ID**：通过行为变更的API接口，对扫描结果筛选。
    - **Fix Status**：API变更扫描结果的修复情况，All表示所有，Fixed表示已修复，Unfixed表示未修复。通过修复情况，对扫描结果筛选。
    - **Scan Again**：重新扫描。
    - **Export**：选择位置后，导出API变更扫描结果数据。
    - **Settings**：设置在扫描API时，可使用的最大堆内存的大小，默认值为3072MB。当工程代码量较大导致扫描缓慢时，可以调整该参数。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155815.46455829001184763732561904018133:50001231000000:2800:737A847395488E616341389CAFD2D5EF21683F4116F7955A6435E15CED21F5DD.png)
    

**使用DevEco Studio 6.0.0 Release以下版本，按以下步骤操作：**

1. 在菜单栏点击**Tools > API Change Assistant**，编辑区下方的API Change Assistant页签中，支持按模块查看API变更情况，选择需要对比的SDK版本号范围，点击**Start Scan**开始扫描。
    
    说明
    
    API变更查询以选择的起始版本为基线，查询当前工程中所使用的API是否存在行为变更。如选择的SDK版本为5.0.0(12) Release 到 6.0.0(20) Release，查询的是5.0.1(13) Beta3到6.0.0(20) Release版本相比5.0.0(12) Release的API变更。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155815.79602746279938159138696208265267:50001231000000:2800:FD7597A64A9A17466A69382A198812CC1B901967C6290A2CB70A2C6A9BCED4CE.png)
    
2. 点击Code Location中的代码地址，跳转到相应的代码编写位置；如需更多指导，可点击Guidance link中的链接，跳转至版本说明文档中查看详情。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155815.05304521910626909959189944962660:50001231000000:2800:CCB8EB1A1DC524C11DB05258BAF893C4308C3EFA4D674B94C8D87FEF7F06EE7B.png)
    
3. 点击**Export**，选择API变更的存放位置后导出变更数据；点击**Scan Again**可重新进行扫描。通过右侧**Settings**按钮，可以设置在扫描API时，可使用的最大堆内存的大小，默认值为3072MB，当工程代码量较大导致扫描缓慢时，可以调整该参数。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155815.27515999406637827163195229590179:50001231000000:2800:AF4602A67C84A9A8C4C4E89A1F5C64C5C03FAE345D1B4EC7B58BEF943525B594.png)
    

## 父/子类快速跳转

编辑器支持快速跳转至当前接口、类、方法、属性的子类/父类。点击代码编辑区域左侧的Gutter Icons（装订线图标）可以跳转到对应的父/子接口或类。如有多个继承关系，在弹窗的文件列表中选择需要查看的接口/类即可。

- ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155815.21683369012155015225034754854779:50001231000000:2800:00C21AE782FD874F9B845740A49C8321A3C46195F9AF9D70F5750DB2C758F5F1.png)Implemented：支持跳转到对应的实现类或子接口及其对应的属性/方法。
- ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155815.96292990282831021323969438561427:50001231000000:2800:59FA7D5573CA1E362D65E2F4395AB49C55424DEEFB5586EF23C5F92A4851EF0C.png)Implementing：支持跳转到对应的父接口或父接口的属性/方法。
- ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155815.24943069327191330310420888302976:50001231000000:2800:00EABBD920B88131F3B7BC3E483F04006967F7A1ACFDAEA65A2FB071FDD3B68D.png)Overridden：支持跳转到对应的子类或子类的属性/方法。
- ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155815.79463949661524918363182171086985:50001231000000:2800:70A5A3EB3D24FB5E869A5836FB710B9DBA1E6839F8A7E1AB484F5574B08DB7C7.png)Overriding：支持跳转到对应的父类或父类的属性/方法。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155815.11325842705664198902482028877232:50001231000000:2800:86D2A77D43D08A1EC433E9032DA55C7E378FE3DB55B194A421F4FA7FBFE462C2.png "点击放大")

本功能默认开启，可以通过菜单栏进入**File > Settings**（macOS为****DevEco Studio > Preferences/Settings****） **> Editor > General > Gutter Icons**，通过勾选或取消勾选Implemented、Implementing、Overridden、Overriding四项可以开启或关闭该功能。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155815.83716898412222641798795820577325:50001231000000:2800:8BDA19919B0FC04FEE2DA342C130CE953C155F6A2A6688805FED6F200299ADFD.png)

## 查看接口/类的层次结构

编辑器支持查看当前接口/类父类或子类的层次结构。选中或将光标放置于类/接口名称处，使用**快捷键Ctrl+H**（macOS为**Control+H**），或在菜单栏**Navigate**页签下选择**Type Hierarchy**，在弹出的Hierarchy窗口中查看接口/类的继承关系结构。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155815.04338246410114482095317208952917:50001231000000:2800:CCC67C1D07B408C1CE67FD4B5F18261B57FA156D64F524B65805E8B5F9548CDE.png)

Hierarchy窗口按钮功能：

|图标|功能|
|:--|:--|
|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155815.20536200852929940431225431740909:50001231000000:2800:D41E4A064C74733B5E98F4A560887583DEEFFCD25506B577AE109AD212F052BC.png)|显示所选类的父类和子类。<br><br>该功能不支持查看接口的继承关系。|
|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155815.08083623997370497431944911922809:50001231000000:2800:81BE8A319005952EC2367021D2090D174816F83584EE21FD7770E1C2B4C7836B.png)|显示当前类/接口的父类。|
|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155815.34231208731692566463909827960950:50001231000000:2800:02D26ECC1535905AAC21790BBA6643FD818707A362447CD59FBE11E7B0625242.png)|显示当前类/接口的子类。|
|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155815.46310411411238333086126010538933:50001231000000:2800:E7281E30F4E28AAE6338697399214A119E3D098943A3581B3035BB1B5EA37A87.png)|按字母顺序对继承关系结构树中的所有同级元素进行排序。|
|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155816.67355044482673543915747781797907:50001231000000:2800:BC02CCEE1BEEF91E7C64C95446CBA113323A4A7620F9CE48063293D3D1F96E04.png)|更新显示所有的类/接口的继承关系结构。|
|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155816.79892156472793137454040903749974:50001231000000:2800:6DE82222446B750BA9B1E224876074F968E50FDBC38911DA3026727EAF4CB3CE.png)|默认双击结构树中类/接口名称时，编辑窗口将跳转至所选类/接口所在的代码位置。勾选该选项后，单击结构树中类/接口名称，即可跳转访问。|
|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155816.73804363673184752100436609457962:50001231000000:2800:1E2AAC1B7C438A4C6CEDC109D118BED0D0C025C53D70D1D424C5A7C71B5483BC.png)<br><br>![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155816.11574297128945582979053831515337:50001231000000:2800:1899BECFDBBF6589E7889D259E45948D1B39CAD88B0C435671EA47245766B360.png)|展开/折叠继承关系结构。|
|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155816.85711670832213670881175431976634:50001231000000:2800:55BDAD4DDAC8D68082484E05184233888A20149FE93EAFA8719B67698EEB0BE7.png)|锁定当前Hierarchy窗口显示于编辑窗口上。|
|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155816.33672365698734846408575870038966:50001231000000:2800:759F00880C4FA3DD5F137AF4B6667F07BBB2DA5E6AECE893F981E5C70F1114F7.png)|将类/接口的继承关系结构导出到文本文件中。|
|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155816.12204325865435859200851618849702:50001231000000:2800:0577256AA1713504BCAA0F4AA947428628A86A58BB84DD3D876DE83594D2A9C9.png)|关闭工具窗口。|

## 添加嵌入提示

从DevEco Studio 6.0.0 Beta2 版本开始，在编辑时启用Inlay Hints嵌入提示功能，可以提供有关参数名称、类型等代码说明信息，提升代码可读性。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155816.28212585779875942065092896083241:50001231000000:2800:B08659A75809705A47C647095D4E92C95086FBC4A2933BDD7E0BFB7F5B8DD4A1.png)

进入**File > Settings**（macOS为**DevEco Studio > Preferences****/Settings**） **> Editor >** **Inlay Hints**，配置勾选希望展示的变量名称、属性、参数、返回值类型，点击**OK**后生效。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155816.29130822285033714759026201689827:50001231000000:2800:F4E543EA5717381FEE367A612B65920E0BCFF4BC8EB4929BB0D48D0560578BE7.png)

## Copy Reference

从DevEco Studio 6.0.0 Beta2 版本开始，在编辑页面选中代码行或类、方法、参数、变量等名称，右键选择**Copy / Paste Special > Copy Reference**，将自动复制定义处的地址。复制成功的地址可以在双击**Shift**弹出的搜索框中进行搜索，帮助开发者快速找到该接口的定义位置。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155816.04131768213643987462643481600457:50001231000000:2800:CBFEC2635EE8689C961F17C36B54DFB85B724BF12A571C53790CE0F334C68CFD.gif)

[代码编辑](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-code-edit "代码编辑")

[代码生成/补全](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-code-completion "代码生成/补全")
# 代码生成/补全

更新时间: 2025-12-16 15:58

## 代码自动补全

提供代码的自动补全能力，编辑器工具会分析上下文，并根据输入的内容，提示可补全的类、方法、字段和关键字的名称等，支持模糊匹配。

自动补齐功能默认按最短路径进行排序，如仅需按照最近使用过的类、方法、字段和关键字等名称提供补全内容排序，可以在**File > Settings**（macOS为**DevEco Studio > Preferences/Settings**） **> Editor > General > Code Completion** 中勾选“Sort suggestions by recently used”。

说明

若已勾选代码补齐按最近使用排序但未生效，请检查**Code Completion**页面，确保“Sort suggestions alphabetically”已取消勾选。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155820.41462658947546364564569033761012:50001231000000:2800:C9736BA0A567DFF56C19080042522209C6C1318088355D03CC9035FB4DA1FB15.png)

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155820.53322605085139737106573327954588:50001231000000:2800:29C04A7C5C5D4C0A0214CDC042B66896226DE013E55745315F6BDC6F35C2B363.gif)

## 快速覆写父类

DevEco Studio提供Override Methods，辅助开发者根据父类模板快速生成子类方法，提升开发效率。将光标放于子类定义位置，使用**快捷键Ctrl+O**（macOS为**Control+O**），或右键单击**Generate**...，选择**Override Methods**，指定需要覆写的对象（方法、变量等），点击**OK**将自动生成该对象的覆写代码。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155820.72523851087964981001198374325590:50001231000000:2800:4A828A39E3944C876BA87CFFB97D744F24F08FD4F56CB2CB0724645F4CEBA30A.gif)

## 快速生成构造器

编辑器支持为类快速生成一个对应的构造函数。

在类中使用**快捷键Alt+Insert**（macOS为**Command+N**），或单击鼠标右键选择**Generate**...，在弹窗中选择**Constructor**，选择一个或多个需要生成构造函数的参数，点击**OK**。若选择**Select None**，则生成不带参数的构造器。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155820.87398985563013627368950953653217:50001231000000:2800:3109CECA6ACDBAAF3D64192EAEBC68B49FD8BBB82BC69754B95E70A93BB90F1F.gif)

## 快速生成get/set方法

编辑器支持为类成员变量或对象属性快速生成get和set方法。

将光标放置在当前类中，单击右键选择**Generate...>Getter and Setter**，或者使用快捷键**Alt+Insert**（macOS为**Command+N**），在菜单中选择**Getter and Setter**，完成方法快速生成。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155820.30879999937710712265106892869095:50001231000000:2800:74F9B9A54E1B160F17CA788F51619710B7589FA2F7F9865C1F6D3C0B9BFF357C.gif)

## 快速生成声明信息到Index文件

编辑器支持将HSP和HAR模块中变量、方法、接口、类等需要对外暴露的信息，通过**Generate...>Declarations**功能，批量在Index.ets文件中进行声明，便于其他模块调用。

在HSP或HAR模块内的文件编辑界面，单击右键选择**Generate...>****Declarations**，或者使用快捷键**Alt+Insert**（macOS为****Command+N****），在菜单中选择**Declarations**，按住快捷键Ctrl并选择需要声明的变量名、方法名、接口名、类名等，即可在模块的Index.ets文件中批量生成相应的声明信息。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155820.67153971327325989523251380782535:50001231000000:2800:FEF3966C673C52307E3848FF4FA2B03EAE9AA0384287980AD2D39AEAE20F2425.gif)

[代码阅读](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-editer-overview "代码阅读")

[代码检查](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-code-check "代码检查")
# 代码实时检查及快速修复

更新时间: 2025-12-16 15:58

## 实时检查

编辑器会实时的进行代码分析，如果输入的语法不符合编码规范，或者出现语义语法错误，将在代码中突出显示错误或警告，将鼠标放置在错误代码处，会提示详细的错误信息。

从DevEco Studio 4.0 Release版本开始，当compileSdkVersion≥10时，编辑器代码实时检查支持ArkTS性能语法规范检查。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155836.51644457988068556568716610339328:50001231000000:2800:5D120B30B1E10EAE158E3698D1CF814C0354B97B5F9DD178F50ED6ACD0A0CE24.png)

说明

当前compileSdkVersion≥10且arkTSVersion≥1.1(默认)时，ArkTS严格类型检查支持实时检查。

## 代码快速修复

DevEco Studio支持代码快速修复能力，辅助开发者快速修复ArkTS或C++代码问题。

**查看告警信息：**使用双击**Shift**快捷键打开文件查询框，输入**problems**打开问题工具面板；双击对应告警信息，可以查看告警的具体位置及原因。

**快速修复：**将光标放在错误告警的位置，可在弹出的悬浮窗中查看问题描述和对应修复方式；单击**M****ore actions**可查看更多修复方法。或是在页面出现灯泡图标时，可点击图标并根据相应建议，实现代码快速修复。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155836.02628668742678220436647154767731:50001231000000:2800:BEBE28DC70648A151ED1501354DC51FBF726A9B2E832C1AE4A8C618993A8D263.png)

## C++快速修复使用演示

下面通过示例展示C++代码中快速修复功能的使用方法。

### 填充switch语句

编辑器支持快速修复方式，对C++代码自动补齐switch条件表达式缺失的case条件，提升编码效率。

光标悬浮在switch表达式的条件变量处，点击灯泡图标，在下拉菜单中选择**Create missing switch cases**，完成缺失的case条件补充。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155836.70524785700756562786863956535535:50001231000000:2800:55F6EDF3F65CE5CE94BAEA0C4E1E917E77BE853F6ADA9FE20E76B39E8EE9DADD.gif)

### 使用auto替换类型

编辑器中可以用 auto 替换 iterator，new expression，cast expression的声明类型。光标悬浮在类型名称处，点击灯泡图标，在下拉菜单中选择**Replace the type with 'auto****'**完成替换。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155836.63977127721012003937395433181824:50001231000000:2800:24CFB8BF055CDCE5E21ED243671E5A1745E76127EA250558D4C965EC826F2911.gif)

### 用?:三元操作符替换if-else

编辑器中支持将if-else语句替换为?:三元操作符。光标放在if表达式的条件处，左侧出现黄色灯泡图标，点击灯泡图标，在下拉菜单中选择**Replace 'if else' with '?:'**完成替换。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155836.02531543582968147146358158176493:50001231000000:2800:62CF7A4012AF0BE047938B329EA204857D801B4F0ECAD8178D9062173E6BCB31.gif)

### 从使用处生成构造函数

如使用了未定义的构造函数，可通过quickfix方式快速生成相应的构造函数定义。点击构造函数名称，左侧出现红色灯泡后，点击灯泡图标选择**Create new constructor 'xxx'**生成构造函数。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155836.92155143344781087835313976631518:50001231000000:2800:1EF06ACA01DEE2DA473432D637487A85C2DA4E5103816A032302C8EFAF71A8A0.gif)

### 将变量拆分为声明和赋值

光标点击需要拆分的变量，左侧出现黄色灯泡后，点击灯泡图标选择**Split into declaration and assignment**，将变量的声明赋值语句拆分成声明语句和赋值语句。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155837.71386813896792568324685437189057:50001231000000:2800:FE5B5F8B4DBAA2E3B53ED87F2BFEEF3FE465C1968AA690F58DE509050839151E.gif)

[代码检查](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-code-check "代码检查")

[Code Linter代码检查](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-code-linter "Code Linter代码检查")
# Code Linter代码检查

更新时间: 2025-12-16 15:58

Code Linter支持对模块内文件或文件夹中的代码进行最佳实践/编程规范方面的检查。检查规则支持配置，配置方式请参考[配置代码检查规则](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-code-linter#section19310459444)。

开发者可根据扫描结果中告警提示手工修复代码缺陷，或者执行一键式自动修复，在代码开发阶段，确保代码质量。

## 配置代码检查规则

新建工程时，工程根目录下默认创建code-linter.json5配置文件，可对代码检查的范围及对应生效的检查规则进行配置。若使用历史工程进行开发，可在工程中右键选择**Code Linter > Generate Config File**创建code-linter.json5配置文件。

其中files和ignore配置项共同确定了代码检查范围，ruleSet和rules配置项共同确定了生效的规则范围。具体配置项功能如下：

**files**：配置待检查的文件名单，如未指定目录，将检查当前被选中的文件或文件夹中所有的.ets文件。

**ignore**：配置无需检查的文件目录，其指定的目录或文件需使用相对路径格式，相对于code-linter.json5所在工程根目录，例如：build/**/*。

**ruleSet**：配置检查使用的规则集，规则集支持一次导入多条规则。规则详情请参见[Code Linter代码检查规则](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-codelinter-rule)。目前支持的规则集包括：

- 通用规则@typescript-eslint
- 安全规则@security
- 性能规则@performance
- 预览规则@previewer
- 一次开发多端部署规则@cross-device-app-dev
- ArkTS代码风格规则@hw-stylistic
- 正确性规则@correctness
- 兼容性规则@compatibility
    
    说明
    
    - 以上规则集均分为all和recommended两种规则集。all规则集是规则全集，包含所有规则；recommended规则集是推荐使用的规则集合。all规则集包含recommended规则集。
    - 不在工程根目录新建code-linter.json5文件的情况下，Code Linter默认会检查@performance/recommended和@typescript-eslint/recommended规则集包含的规则。
    

**rules**：可以基于ruleSet配置的规则集，新增额外规则项，或修改ruleSet中规则默认配置，例如：将规则集中某条规则告警级别由warn改为error。

**overrides**：针对工程根目录下部分特定目录或文件，可配置定制化检查的规则。

**extRuleSet**：配置需要检查的自定义规则，具体请参考：[自定义规则开发指南](https://gitcode.com/openharmony-sig/homecheck/blob/master/document/developer/ExtRule%E8%87%AA%E5%AE%9A%E4%B9%89%E8%A7%84%E5%88%99%E5%BC%80%E5%8F%91%E6%8C%87%E5%8D%97.md)。该字段从DevEco Studio 5.1.0 Release版本开始支持。

1. {
2.   "files":   //用于表示配置适用的文件范围的 glob 模式数组。在没有指定的情况下，应用默认配置
3.   [
4.     "**/*.js", //字符串类型
5.     "**/*.ts"
6.   ],
7.   "ignore":  //一个表示配置对象不应适用的文件的 glob 模式数组。如果没有指定，配置对象将适用于所有由 files 匹配的文件
8.   [
9.     "build/**/*",    //字符串类型
10.     "node_modules/**/*"
11.   ],
12.   "ruleSet":       //设置检查待应用的规则集
13.   [
14.     "plugin:@typescript-eslint/recommended"    //快捷批量引入的规则集, 枚举类型：plugin:@typescript-eslint/all, plugin:@typescript-eslint/recommended, plugin:@cross-device-app-dev/all, plugin:@cross-device-app-dev/recommended等
15.   ],
16.   "rules":         //可以对ruleSet配置的规则集中特定的某些规则进行修改、去使能, 或者新增规则集以外的规则；ruleSet和rules共同确定了代码检查所应用的规则
17.   {
18.     "@typescript-eslint/no-explicit-any":  // ruleId后面跟数组时, 第一个元素为告警级别, 后面的对象元素为规则特定开关配置
19.     [
20.       "error",              //告警级别: 枚举类型, 支持配置为suggestion, error, warn, off
21.       {
22.         "ignoreRestArgs": true   //规则特定的开关配置, 为可选项, 不同规则其下层的配置项不同
23.       }
24.     ],
25.     "@typescript-eslint/explicit-function-return-type": 2,   // ruleId后面跟单独一个数字时, 表示仅设置告警级别, 枚举值为: 3(suggestion), 2(error), 1(warn), 0(off)
26.     "@typescript-eslint/no-unsafe-return": "warn"            // ruleId后面跟单独一个字符串时, 表示仅设置告警级别, 枚举值为: suggestion, error, warn, off
27.   },
28.   "overrides":      //针对特定的目录或文件采用定制化的规则配置
29.   [
30.     {
31.       "files":   //指定需要定制化配置规则的文件或目录
32.       [
33.         "entry/**/*.ts"   //字符串类型
34.       ],
35.       "excluded":
36.       [
37.         "entry/**/*.test.js" //指定需要排除的目录或文件, 被排除的目录或文件不会按照定制化的规则配置被检查; 字符串类型
38.       ],
39.       "rules":   //支持对overrides外公共配置的规则进行修改、去使能, 或者新增公共配置以外的规则; 该配置将覆盖公共配置
40.       {
41.         "@typescript-eslint/explicit-function-return-type":  // ruleId: 枚举类型
42.         [
43.           "warn",     //告警级别: 枚举类型, 支持配置为error, warn, off; 覆盖公共配置, explicit-function-return-type告警级别为warn
44.           {
45.              "allowExpressions": true    //规则特定的开关配置, 为可选项, 不同规则其下层的配置项不同
46.           }
47.         ],
48.         "@typescript-eslint/no-unsafe-return": "off"   // 覆盖公共配置, 不检查no-unsafe-return规则
49.       },
50.       "extRules": {     //支持对overrides外自定义规则集配置的规则进行修改、去使能; 该配置将覆盖自定义规则配置
51.         "@extrulesproject/foreach-args-check": "off"   // 覆盖自定义规则配置, 不检查@extrulesproject/foreach-args-check规则
52.       }
53.     }
54.   ],
55.   "extRuleSet": [     //自定义规则集的配置
56.     {
57.         "ruleSetName": "extrulesproject",     //自定义规则库的名称。格式为@group/packagename或者packagename，全局唯一。除@和/外，group和packagename只能包含小写字母、数字、下划线（_）和中划线(-)。总长度小于等于128个字符。另外，group和packagename必须以字母开头，不能作为ArkTS的保留关键字
58.         "packagePath": "D:\\checker\\extrulesproject-1.0.0.tgz",     //自定义规则安装包路径，需使用绝对路径
59.         "extRules": {     //自定义规则名称以及告警等级，枚举值为: 3(suggestion), 2(error), 1(warn), 0(off)
60.           "@extrulesproject/foreach-args-check": 1
61.         }
62.     }
63.   ]
64. }

## 通过DevEco Studio进行代码检查

### 操作方法

在已打开的代码编辑器窗口单击右键点击**Code Linter**，或在工程管理窗口中鼠标选中单个或多个工程文件/目录，右键选择**Code Linter** **> Full Linter**执行代码全量检查。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155839.47490233893867987363368971531769:50001231000000:2800:DFE09494630ADCF4B6BC7AEBC1118BACF43C526833046F0698330DCBFC27D850.png)

如只需对Git工程中增量文件（包含新增/修改/重命名）进行检查，可在commit界面右下角点击齿轮图标，选择**Incremental Linter**执行增量检查。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155839.64268922873188670973109422009006:50001231000000:2800:6497AF66E4CCE25C8BFBAFDC3C0FA183C2DCE121013522762817EAE725699E1F.png "点击放大")

说明

- 若未配置代码检查规则文件，直接执行Code Linter，将按照默认的编程规范规则对.ets文件进行检查。
- Code Linter不对如下文件及目录进行检查：
    - src/ohosTest文件夹
    - /src/test文件夹
    - node_modules文件夹
    - oh_modules文件夹
    - build文件夹
    - .preview文件夹
    - hvigorfile.ts文件
    - hvigorfile.js文件
    - BuildProfile.ets文件

### 查看和处理代码检查结果

扫描完成后，在底部工具面板查看检查结果。勾选**Defects**中不同告警等级，可分别查看对应告警级别的信息。点击**Filter by scene**下拉菜单，可以筛选不同规则的检查结果。双击某条告警结果，可以跳转到对应代码缺陷位置；选中告警结果时，可以在右侧**Defect Description窗口**查看告警对应的规则详细说明，其中包含正向和反向示例，并根据其中的建议修改代码；搜索规则时，可设定是否全词匹配和大小写敏感。

单击![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155839.93777549902695147390533091114765:50001231000000:2800:04EEACFDDB9950148FCA5686001E02845E579F136E105B56CFBD085534E1ABD9.jpg)图标，查看可修复的代码规则，点击![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155839.82774331669380336897910129325028:50001231000000:2800:4E6AEA3E9513451DC3AAECA90366EFA8789A1D6EB5A343346F00594C3081567C.png)代码修复图标，可以一键式批量修复告警，并刷新检查结果。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155839.92699980928420615289927680058351:50001231000000:2800:3660164F7C1407FDBFD4447CCC3E5C3149D703A477DC0CB428544BA18F03C674.png)

**屏蔽告警信息**：

- 在某些特殊场景下，若扫描结果中出现误报，点击单条告警结果后的![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155839.41916082364855691138081859881454:50001231000000:2800:AE19987348D57631B1EF20302FDA2B21F44351E3D0372B7653860ABB02A94FE8.jpg)**Ignore**图标**，**可以忽略对告警所在行的code linter检查；或勾选文件名称或多条待屏蔽的告警，点击左侧工具面板**Ignore**图标批量执行操作；
- 在文件顶部添加注释/* eslint-disable */可以屏蔽整个文件执行code linter检查，在eslint-disable 后加入一个或多个以逗号分隔的规则Id，可以屏蔽具体检查规则；
- 在需要忽略检查的代码块前后分别添加/* eslint-disable */和/* eslint-enable */添加注释信息，再执行**Code Linter，**将不再显示该代码块扫描结果；在待屏蔽的代码行前一行添加/* eslint-disable-next-line */，也可屏蔽对该代码行的Code Linter检查。

如需恢复忽略的报错信息，可以直接删除该行上方的注释，重新执行**Code Linter**检查。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155839.77135754907521365229523770254007:50001231000000:2800:9F492086FCE05076B9EDD9E5618CC465A8C34A0C7DEF3FB7463700CD2FC993BD.png)

**导出检查结果**：点击工具面板左侧![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155840.64679103406679925518123024218608:50001231000000:2800:E76D18DA6E85DA0FD0097BE67905B85D69C4215B3940C473D6DC12B816C926DE.jpg)导出按钮，即可导出检查结果到excel文件，包含告警所在行，告警明细，告警级别等信息。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155840.19099670782063087233834545846978:50001231000000:2800:C6896737D7F878798233C727C372278B35B18B1FFB60760FE9C5C7E7695AC3A6.png)

## 通过命令行进行代码检查

从DevEco Studio 6.0.1 Beta1开始，支持通过命令行方式进行代码检查。在DevEco Studio安装包\deveco-studio\plugins\codelinter\run目录下打开cmd或者bash窗口，执行如下命令：

1. node ./index.js [options] [dir] 

options：可选配置，具体请参考[表codelinter命令行配置](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-command-line-codelinter#table25697717185)。

dir：待检查的工程根目录，可选，默认为当前上下文目录。

说明

使用命令行检查时，需要依赖于Node.js环境，本地安装的Node.js版本和DevEco Studio中tools目录下的Node.js版本需要保持一致。

## 实践说明

以@typescript-eslint/no-restricted-syntax（使用某类语法时，codelinter告警）、@typescript-eslint/naming-convention（命名风格校验）和@hw-stylistic/file-naming-convention（检查代码文件的命名风格）三个规则为例，介绍codelinter配置文件的使用方法。

### 示例1：调用类Foo下bar方法时，Code Linter告警

**在配置文件中定义规则**

在ArkTS工程中，pages/Index.ets文件下增加以下用例：

1. class Foo {
2.   static bar() {}
3. }

4. Foo.bar();

在工程根目录下新建code-linter.json5文件（文件名不可修改），新增以下配置：

1. {
2.   "rules": {
3.     "@typescript-eslint/no-restricted-syntax": [
4.       // 告警级别: 枚举类型, 支持配置为error, warn, off
5.       "error",
6.       {
7.         // selector属性必选，配置要禁用的语法
8.         // 可通过特定DSL筛选待限制的语句，CallExpression表示方法调用表达式，后面的中括号里面是筛选条件（根据语法树Node节点来确定）
9.         // 其中callee.object.name根据指定的名称筛选调用方法的对象（class，namespace或module），以上示例中为"Foo"
10.         // callee.property.name则根据指定的名称筛选被调用的方法，以上示例中为"bar"
11.         "selector": "CallExpression[callee.object.name='Foo'][callee.property.name='bar']",
12.         // message属性可选，配置要展示的报错信息
13.         "message": "Foo.bar() is not allowed"
14.       }
15.     ]
16.   },
17. }

说明

如需在code-linter.json5文件中配置其他字段，请参见[配置代码检查规则](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-code-linter#section19310459444)。

**执行代码检查**

对pages/Index.ets文件执行代码检查，检查结果如下：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155840.84980670044908349910628089991199:50001231000000:2800:7C96BCDBA8CBA949ABFB866DC82BAE3ADC387AFB63CAC65D925536D8D552DB47.png)

### 示例2：对类名Foo的命名风格校验

**在配置文件中定义规则**

在ArkTS工程中，pages/Index.ets文件下增加以下用例：

1. class foo {    //此处构造一个命名风格错误的示例，foo为错误使用类名，正确类名应为Foo
2.   bar() {} 
3. }

在工程根目录下新建code-linter.json5文件，新增以下配置：

1. {
2.   "rules": {
3.     "@typescript-eslint/naming-convention": [
4.       "error",
5.       {
6.         // selector属性必选，配置要检查的语法，这里配置的class表示检查自定义组件名
7.         "selector": "class",
8.         // format属性必选，配置期望的命名风格，支持枚举值，这里配置的PascalCase表示大驼峰风格
9.         "format": ["PascalCase"],
10.         // custom属性可选，配置用户自定义的命名风格
11.         "custom": {
12.           // regex属性必选，配置具体的正则
13.           "regex": "^[a-zA-Z]+$",
14.           // match属性必选，配置为true表示正则未命中时报错；配置为false表示正则命中时报错
15.           "match": true
16.         }
17.       }
18.     ]
19.   },
20. }

**表1** 字段说明
|字段名称|参数说明|是否必选|类型|支持配置的参数|
|:--|:--|:--|:--|:--|
|selector|配置要检查的语法|是|字符串、字符串数组|- variable：变量<br>- function：函数<br>- parameter：参数<br>- parameterProperty：参数属性<br>- accessor：get/set方法<br>- enumMember：枚举成员<br>- classMethod：类方法<br>- structMethod：自定义组件中的方法<br>- objectLiteralMethod：对象方法<br>- typeMethod：接口方法<br>- classProperty：类属性<br>- structProperty：自定义组件中的属性<br>- objectLiteralProperty：对象属性<br>- typeProperty：接口属性<br>- class：类<br>- struct：自定义组件<br>- interface：接口<br>- typeAlias：类型别名<br>- enum：枚举<br>- typeParameter：泛型参数<br>- default：包含以上所有的类型<br>- variableLike：包含variable，function，parameter<br>- memberLike：包含classProperty，structProperty，objectLiteralProperty，typeProperty，parameterProperty ，enumMember，classMethod，objectLiteralMethod，typeMethod，accessor<br>- typeLike：包含class，struct，interface，typeAlias，enum，typeParameter<br>- method：包含classMethod，structMethod，objectLiteralMethod，typeMethod<br>- property：包含classProperty，objectLiteralProperty，typeProperty|
|format|配置期望的命名风格|是|字符串数组|- camelCase：小驼峰命名风格，比如getName，getID（支持连续大写字母），不支持下划线<br>- strictCamelCase：严格小驼峰命名风格，除了不支持连续大写字母（getID），其他的和camelCase相同<br>- PascalCase：大驼峰命名风格，比如Foo，CC，除了要求第一个字母大写，其他的和camelCase相同<br>- StrictPascalCase：大驼峰命名风格，除了不支持连续大写字母（CC），其他的和PascalCase相同<br>- snake_case：小写字母+下划线+小写字母的命名风格，比如a_a，不支持_a，a_a_<br>- UPPER_CASE：大写字母+下划线+大写字母的命名风格，比如A_A，不支持_A，A_A_|
|custom|配置用户自定义的命名风格|否|对象|- regex：属性必选，配置具体的正则<br>- match：属性必选，配置为true表示正则未命中时报错，配置为false表示正则命中时报错|
|leadingUnderscore/trailingUnderscore|配置是否允许以下划线开头/以下划线结尾的命名风格|否|字符串|- allow：允许以一个下划线开头/结尾的命名风格，比如_name<br>- allowDouble：允许以两个下划线开头/结尾的命名风格，比如__name<br>- allowSingleOrDouble：允许以一个或者两个下划线开头/结尾的命名风格（allow+allowDouble）<br>- forbid：禁止以下划线开头/结尾的命名风格，比如_name，__name<br>- require：必须是以下划线开头/结尾的命名风格，比如_name，__name<br>- requireDouble：必须是以两个下划线开头/结尾的命名风格，比如__name|
|prefix/suffix|配置固定前缀/后缀的命名风格。如果前缀/后缀未匹配则报错|否|字符串数组|用户自定义前缀/后缀|
|filter|过滤特定的命名风格，检查或者不检查正则命中的命名|否|对象|配置格式与custom相似<br><br>match：设置为true表示只检查正则命中的名字，设置为false表示不检查正则命中的名字<br><br>regex：设置过滤的正则<br><br>说明<br><br>支持直接配置一个字符串，这个字符串配置的是regex，此时match相当于配置的是true。|
|modifiers|匹配修饰符，只有包含特定修饰符的命名才会检查|否|字符串数组|- abstract：匹配abstract关键字<br>- override：匹配override关键字<br>- private：匹配private关键字<br>- protected：匹配protected关键字<br>- static：匹配static关键字<br>- async：匹配async关键字<br>- const：匹配const关键字<br>- destructured：匹配解构语法<br>- exported：匹配export关键字<br>- global：匹配全局声明<br>- #private：匹配私有符号#<br>- public：匹配public级别的访问修饰符<br>- requiresQuotes：匹配字符串类型的命名，并且 字符串中包含特殊字符<br>- unused：匹配未使用的声明|
|types|匹配类型，只有特定类型的名字才会检查|否|字符串数组|- array：数组类型<br>- boolean：布尔类型<br>- function：函数类型<br>- number：数字类型<br>- string：字符串类型|

说明

以上配置的参数有校验优先级：filter > types > modifiers > validate leading underscore > validate trailing underscore > validate prefix > validate suffix > validate custom > validate format。

**执行代码检查**

对pages/Index.ets文件执行代码检查，检查结果如下：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155840.80685508632458589785440438521836:50001231000000:2800:B79785E5529436F53EBF4F57E5759250D49F56B1D964A791D7B5C7E34A194F9D.png)

### 示例3：检查代码文件的命名风格

**在配置文件中定义规则**

在ArkTS工程中，pages目录下新建test.ets文件；

在工程根目录下新建code-linter.json5文件，新增以下配置：

1. {
2.   "rules": {
3.     "@hw-stylistic/file-naming-convention": [
4.       // 告警级别：枚举类型，支持配置为error，warn，off
5.       "error",
6.       {
7.         // selector属性可选，支持配置为code或者resources
8.         // code表示检查代码文件的命名风格
9.         // resources表示检查资源文件的命名风格
10.         "selector": "code"
11.       }
12.     ]
13.   },
14. }

说明

如果selector属性不配置，默认检查代码文件和资源文件的命名风格。

**执行代码检查**

对pages/test.ets文件执行代码检查，检查结果如下：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155840.74087431053028422253786277388507:50001231000000:2800:093A6727EA9D37EEB8EF3659396B5B16BE47FF16C0B504ED04BAA5083D7EC7EB.png)

[代码实时检查及快速修复](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-realtime-check "代码实时检查及快速修复")

[Code Linter代码检查规则](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-codelinter-rule "Code Linter代码检查规则")
# recommended推荐规则清单

更新时间: 2025-12-16 15:58

## 通用规则推荐规则集@typescript-eslint/recommended

|   |   |
|---|---|
|@typescript-eslint/await-thenable|不允许对不是“Thenable”对象的值使用await关键字（“Thenable”表示某个对象拥有“then”方法，比如Promise）。|
|@typescript-eslint/consistent-type-imports|强制使用一致的类型导入风格。|
|@typescript-eslint/explicit-function-return-type|函数和类方法需要显式的定义返回类型。|
|@typescript-eslint/explicit-module-boundary-types|导出到外部的函数和公共类方法，需要显式的定义返回类型和参数类型。|
|@typescript-eslint/no-dynamic-delete|不允许在computed key表达式上使用“delete”运算符。|
|@typescript-eslint/no-explicit-any|不允许使用“any”类型。|
|@typescript-eslint/no-for-in-array|禁止使用 for-in 循环来遍历数组元素。|
|@typescript-eslint/no-this-alias|禁止将“this”赋值给一个变量。|
|@typescript-eslint/no-unnecessary-type-constraint|不允许在泛型中使用不必要的约束条件。|
|@typescript-eslint/no-unsafe-argument|不允许将any类型的值作为函数的参数传入。|
|@typescript-eslint/no-unsafe-assignment|禁止将“any”类型的值赋值给变量和属性。|
|@typescript-eslint/no-unsafe-call|禁止调用“any”类型的表达式。|
|@typescript-eslint/no-unsafe-member-access|禁止成员访问“any”类型的值。|
|@typescript-eslint/no-unsafe-return|函数禁止返回类型为“any”的值。|
|@typescript-eslint/prefer-literal-enum-member|要求所有枚举成员都定义为字面量值。|

## 安全规则推荐规则集@security/recommended

|   |   |
|---|---|
|@security/no-commented-code|不使用的代码段建议直接删除，不允许通过注释的方式保留。|
|@security/no-unsafe-aes|该规则禁止在AES加密算法中使用不安全的ECB加密模式。|
|@security/no-unsafe-dh|该规则禁止使用不安全的DH密钥协商算法。|
|@security/no-unsafe-dh-key|该规则禁止使用不安全的DH密钥。|
|@security/no-unsafe-dsa|该规则禁止使用不安全的DSA签名算法。|
|@security/no-unsafe-dsa-key|该规则禁止使用不安全的DSA密钥。|
|@security/no-unsafe-ecdsa|该规则禁止在ECDSA签名算法中使用不安全的SHA1摘要算法。|
|@security/no-unsafe-hash|该规则使用禁止不安全的哈希算法。|
|@security/no-unsafe-mac|该规则禁止在MAC消息认证算法中使用不安全的哈希算法。|
|@security/no-unsafe-rsa-encrypt|该规则禁止使用不安全的RSA非对称加密算法。|
|@security/no-unsafe-rsa-key|该规则禁止使用不安全的RSA密钥。|
|@security/no-unsafe-rsa-sign|该规则禁止不安全的RSA签名算法。|
|@security/no-unsafe-3des|该规则禁止使用不安全的3DES加密模式。|

## 性能规则推荐规则集@performance/recommended

|   |   |
|---|---|
|@performance/foreach-args-check|建议在ForEach参数中设置keyGenerator。|
|@performance/high-frequency-log-check|不建议在高频函数中使用Hilog。|
|@performance/hp-arkts-no-use-any-export-current|避免使用export * 导出当前module中定义的类型和数据。|
|@performance/hp-arkts-no-use-any-export-other|避免使用export * 导出其他module中定义的类型和数据。|
|@performance/hp-arkui-avoid-update-auto-state-var-in-aboutToReuse|避免在aboutToReuse中对自动更新值的状态变量进行更新。|
|@performance/hp-arkui-combine-same-arg-animateto|建议动画参数相同时使用同一个animateTo。|
|@performance/hp-arkui-load-on-demand|建议使用按需加载。|
|@performance/hp-arkui-no-func-as-arg-for-reusable-component|避免使用函数作为复用的自定义组件创建时的入参。|
|@performance/hp-arkui-no-state-var-access-in-loop|避免在for、while等循环逻辑中频繁读取状态变量。|
|@performance/hp-arkui-no-stringify-in-lazyforeach-key-generator|在使用LazyForEach进行组件复用的key生成器函数里，不要使用stringify。|
|@performance/hp-arkui-replace-nested-reusable-component-by-builder|建议使用@Builder替代嵌套的自定义组件。|
|@performance/hp-arkui-set-cache-count-for-lazyforeach-grid|建议在Grid下使用LazyForEach时设置合理的cacheCount。|
|@performance/hp-arkui-suggest-cache-avplayer|建议缓存AVPlayer实例减少起播时延。|
|@performance/hp-arkui-suggest-reuseid-for-if-else-reusable-component|建议使用reuseId标记不同结构的组件构成。|
|@performance/hp-arkui-suggest-use-effectkit-blur|建议使用effectKit.createEffect实现模糊效果。|
|@performance/hp-arkui-use-grid-layout-options|建议在指定位置时使用GridLayoutOptions提升Grid性能。|
|@performance/hp-arkui-use-local-var-to-replace-state-var|建议使用临时变量替换状态变量。|
|@performance/hp-arkui-use-object-link-to-replace-prop|建议使用@ObjectLink代替@Prop减少不必要的深拷贝。|
|@performance/hp-arkui-use-onAnimationStart-for-swiper-preload|建议Swiper预加载机制搭配 OnAnimationStart 接口回调使用。|
|@performance/hp-arkui-use-reusable-component|建议复杂组件的定义，尽量使用组件复用。|
|@performance/hp-arkui-use-scale-to-replace-attr-animateto|建议组件布局改动时使用图形变换属性动画。|
|@performance/hp-arkui-use-transition-to-replace-animateto|建议组件转场动画使用transition。|
|@performance/hp-ffrt-no-use-std|禁止在FFRT worker中使用std::xxx等同步接口。|
|@performance/no-high-loaded-frame-rate-range|不允许锁定最高帧率运行。|
|@performance/start-window-icon-check|启动页图标分辨率建议不超过256 * 256。|
|@performance/waterflow-data-preload-check|建议对waterflow子组件进行数据预加载。|
|@performance/web-on-active-check|使用了Web预渲染技术的应用，建议在预渲染完成后（onFirstMeaningfulPaint），调用停止渲染接口（onInactive）。|
|@performance/gif-hardware-decoding-check|在使用@ohos/gif-drawable库解码gif图片时，建议开启硬解码，提升gif加载性能。|
|@performance/no-use-any-import|使用import的方式引入对应的模块时，建议按需引用使用到的变量代替“import *”的方式，以减少 .ets文件的执行耗时和文件中所有export变量的初始化过程。|
|@performance/avoid-overusing-custom-component-check|当在应用中使用自定义组件时，可以优先使用@Builder函数代替自定义组件，@Builder函数不会在后端FrameNode节点树上创建一个新的树节点，有助于缩短页面的加载和渲染时长。|
|@performance/bad-deep-clone-check|避免使用不合理深拷贝，如JSON.parse(JSON.stringify(foo))和_.cloneDeep(foo)。|
|@performance/reuse-date-instances-check|用于检测在循环或调用频繁的方法中重复创建Date对象，建议开发者重用现有实例或使用时间戳进行计算，减少创建Date成本。|
|@performance/crypto-replacement-check|对于三方库@ohos/crypto-js所提供的大部分接口，SDK（@ohos.security.cryptoFramework）中有对应的系统原生实现。建议使用系统原生接口。|
|@performance/monitor-invisible-area-in-image-animation|使用ImageAnimation实现帧动画时，建议显式调用monitorInvisibleArea接口。在动画组件不可见时，会停止动画播放，减少无效的冗余动画带来的负载恶化。|
|@performance/datashare-query-unrelease-check|建议使用DataShareHelper的query接口查询数据得到结果后，应及时关闭，避免造成内存泄露。|
|@performance/update-state-var-between-animatetos-check|如果多个animateTo之间存在状态更新，会导致执行下一个animateTo之前又存在需要更新的脏节点，可能造成冗余更新。因此不建议在两次animateTo之间进行状态变量更新。|

## 预览规则集@previewer/recommended

|   |   |
|---|---|
|@previewer/mandatory-default-value-for-local-initialization|如果组件的属性支持本地初始化，需要设置一个合法的不依赖运行时的默认值。|
|@previewer/no-page-method-on-preview-component|禁止在非路由组件上实例化onPageShow、onPageHide、onBackPress等页面级方法。|
|@previewer/no-unallowed-decorator-on-root-component|对于@Entry组件，不允许使用@Consume、@Link、@ObjectLink、@Prop注解；对于@Preview组件，建议使用一个定义了完整的、合法的、不依赖运行时的默认值的父组件作为预览该组件的容器。|

## 一次开发多端部署规则推荐规则集@cross-device-app-dev/recommended

|   |   |
|---|---|
|@cross-device-app-dev/color-contrast|文本和背景之间的颜色对比度至少为4.5:1以确保可读性。|
|@cross-device-app-dev/color-value|颜色值应当使用“$r”从color.json中引用，以适配不同的系统颜色模式，禁止使用固定的值。|
|@cross-device-app-dev/font-size|字体大小要求至少为8fp以便于阅读。|
|@cross-device-app-dev/font-size-unit|字体大小单位建议使用fp，以适配系统字体设置。|
|@cross-device-app-dev/grid-columns-span|不推荐开发者将栅格中所有的GridCol子组件只设置span属性，且值与父组件的columns属性相等。|
|@cross-device-app-dev/grid-span-value|在栅格布局组件GridCol中，span和offset不建议使用小数。|
|@cross-device-app-dev/sidebar-navigation|对于2in1和tablet设备，应将Tabs组件设置为侧边导航栏。|
|@cross-device-app-dev/size-unit|组件通用属性width、height和size，应当使用vp作为单位，以适配不同设备屏幕宽度。|
|@cross-device-app-dev/touch-target-size|组件通用属性responseRegion点击热区需满足最小尺寸要求。|
|@cross-device-app-dev/one-multi-breakpoint-check|一多特性必须使用系统断点判断是否开启，不能通过设备类型、设备方向或是否可折叠等属性来判断。|

## ArkTS代码风格规则推荐规则集@hw-stylistic/recommended

|   |   |
|---|---|
|@hw-stylistic/array-bracket-spacing|强制数组“[”之后和“]”之前加空格。该规则仅检查.ets文件类型。|
|@hw-stylistic/brace-style|强制大括号和语句位于同一行。该规则仅检查.ets文件类型。|
|@hw-stylistic/comma-spacing|强制数组元素和函数中多个参数之间的逗号后面加空格，逗号前不加空格。该规则仅检查.ets文件类型。|
|@hw-stylistic/curly|条件语句和循环语句的逻辑代码必须写在大括号中。该规则仅检查.ets文件类型。|
|@hw-stylistic/file-naming-convention|强制代码文件和资源文件保持一致的命名风格。|
|@hw-stylistic/indent|强制switch语句中的case和default缩进一层。该规则仅检查.ets文件类型。|
|@hw-stylistic/keyword-spacing|在关键字前后强制加空格。该规则仅检查.ets文件类型。|
|@hw-stylistic/max-len|强制代码行最大长度为120个字符。该规则仅检查.ets文件类型。|
|@hw-stylistic/no-multi-spaces|不允许出现连续多个空格，除非是换行。该规则仅检查.ets文件类型。|
|@hw-stylistic/no-tabs|禁止使用tab作为缩进，推荐使用空格。该规则仅检查.ets文件类型。|
|@hw-stylistic/object-property-newline|强制对象属性换行。|
|@hw-stylistic/one-var-declaration-per-line|变量声明时，要求一次仅声明一个变量。该规则仅检查.ets文件类型。|
|@hw-stylistic/operator-linebreak|强制运算符位于代码行末。|
|@hw-stylistic/quotes|强制字符串使用单引号。|
|@hw-stylistic/semi-spacing|强制分号之前不加空格。|
|@hw-stylistic/space-before-blocks|强制在“{”之前加空格。|
|@hw-stylistic/space-before-function-paren|在函数名和“(”之间强制不加空格。该规则仅检查.ets文件类型。|
|@hw-stylistic/space-infix-ops|强制运算符前后都加空格。|

[规则变更说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-codelinter-rules-change "规则变更说明")

[通用规则@typescript-eslint](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-typescript-eslint "通用规则@typescript-eslint")
# @typescript-eslint/adjacent-overload-signatures

更新时间: 2025-12-16 15:59

建议函数重载的签名保持连续。

## 规则配置

1. // code-linter.json5
2. {
3.   "rules": {
4.     "@typescript-eslint/adjacent-overload-signatures": "error",
5.   }
6. }

## 选项

该规则无需配置额外选项。

## 正例

1. export declare function bar(): void;
2. export declare function foo(a: string): void;
3. export declare function foo(a: number, b: number): void;
4. export declare function foo(a: number, b: string, c?: string): void;

## 反例

1. export declare function foo(a: string): void;
2. export declare function bar(): void;
3. export declare function foo(a: number, b: number): void;
4. export declare function foo(a: number, b: string, c?: string): void;

## 规则集

1. plugin:@typescript-eslint/all

Code Linter代码检查规则的配置指导请参考[Code Linter代码检查](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-code-linter)。

[通用规则@typescript-eslint](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-typescript-eslint "通用规则@typescript-eslint")

[@typescript-eslint/array-type](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide_array-type "@typescript-eslint/array-type")
# @typescript-eslint/array-type

更新时间: 2025-12-16 15:59

定义数组类型时，建议使用相同的样式。比如都使用T[]或者都使用Array<T>。

## 规则配置

1. // code-linter.json5
2. {
3.   "rules": {
4.     "@typescript-eslint/array-type": "error"
5.   }
6. }

## 选项

详情请参考[typescript/array-type 选项](https://typescript-eslint.nodejs.cn/rules/array-type#options)。

## 正例

1. const x: string[] = ['a', 'b'];
2. const y: readonly string[] = ['a', 'b'];

3. export { x, y };

## 反例

1. const x: Array<string> = ['a', 'b'];
2. const y: ReadonlyArray<string> = ['a', 'b'];

3. export { x, y };

## 规则集

1. plugin:@typescript-eslint/all

Code Linter代码检查规则的配置指导请参考[Code Linter代码检查](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-code-linter)。

[@typescript-eslint/adjacent-overload-signatures](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide_adjacent-overload-signatures "@typescript-eslint/adjacent-overload-signatures")

[@typescript-eslint/await-thenable](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide_await-thenable "@typescript-eslint/await-thenable")
# @performance/avoid-overusing-custom-component-check

更新时间: 2025-12-16 15:59

当在应用中使用自定义组件时，可以优先使用@Builder函数代替自定义组件，@Builder函数不会在后端FrameNode节点树上创建一个新的树节点，有助于缩短页面的加载和渲染时长。

## 规则配置

1. // code-linter.json5
2. {
3.   "rules": {
4.     "@performance/avoid-overusing-custom-component-check": "warn",
5.   }
6. }

## 选项

该规则无需配置额外选项。

## 正例

1. // 1. 自定义@Builder函数组件
2. @Builder
3. function UserCardBuilder(name: string, age?: number, avatarImage?: ResourceStr) {
4.   Row() {
5.     Row() {
6.       Image(avatarImage)
7.         .size({ width: 50, height: 50 })
8.         .borderRadius(25)
9.         .margin(8)
10.       Text(name)
11.         .fontSize(30)
12.     }

13.     Text(`年龄：${age?.toString()}`)
14.       .fontSize(20)
15.   }
16.   .backgroundColor(DEFAULT_BACKGROUND_COLOR)
17.   .justifyContent(FlexAlign.SpaceBetween)
18.   .borderRadius(8)
19.   .padding(8)
20.   .height(66)
21.   .width('80%')
22. }

23. @Component
24. export struct UserCardList {
25.   @State users: User[] = getUsers();

26.   aboutToAppear(): void {
27.     let message = 'hello world';
28.   }

29.   build() {
30.     List({ space: 8 }) {
31.       ForEach(this.users, (item: User) => {
32.         ListItem() {
33.           // 2. 使用@Builder函数
34.           UserCardBuilder(item.name, item.age, item.avatarImage)
35.         }
36.       }, (item: User) => item.id)
37.     }
38.     .alignListItem(ListItemAlign.Center)
39.   }
40. }

## 反例

1. import { util } from '@kit.ArkTS';

2. interface User {
3.   id: string;
4.   name: string;
5.   age?: number;
6.   avatarImage?: ResourceStr;
7.   // introduction: string;
8.   // ...
9. }

10. // 构造数据
11. const DEFAULT_BACKGROUND_COLOR = Color.Pink;
12. const getUsers = () => {
13.   const USERS: User[] = [{
14.     id: '1',
15.     name: '张三',
16.   }, {
17.     id: '2',
18.     name: '李四',
19.   }, {
20.     id: '3',
21.     name: '王五',
22.   }];
23.   return Array.from(Array(30), (item: User, i: number) => {
24.     return {
25.       id: util.generateRandomUUID(),
26.       name: USERS[i%3].name,
27.       avatarImage: $r('app.media.avatar'),
28.       age: 18 + i
29.     } as User;
30.   });
31. }

32. // 用户卡片列表组件
33. @Component
34. export struct UserCardList {
35.   @State users: User[] = getUsers();

36.   build() {
37.     List({ space: 8 }) {
38.       ForEach(this.users, (item: User) => {
39.         ListItem() {
40.           UserCard({ name: item.name, age: item.age, avatarImage: item.avatarImage })
41.         }
42.       }, (item: User) => item.id)
43.     }
44.     .alignListItem(ListItemAlign.Center)
45.   }
46. }

47. // 用户卡片自定义组件
48. @Component
49. struct UserCard {
50.   @Prop avatarImage: ResourceStr;
51.   @Prop name: string;
52.   @Prop age: number;

53.   build() {
54.     Row() {
55.       Row() {
56.         Image(this.avatarImage)
57.           .size({ width: 50, height: 50 })
58.           .borderRadius(25)
59.           .margin(8)
60.         Text(this.name)
61.           .fontSize(30)
62.       }

63.       Text(`年龄：${this.age.toString()}`)
64.         .fontSize(20)
65.     }
66.     .backgroundColor(DEFAULT_BACKGROUND_COLOR)
67.     .justifyContent(FlexAlign.SpaceBetween)
68.     .borderRadius(8)
69.     .padding(8)
70.     .height(66)
71.     .width('80%')
72.   }
73. }

## 规则集

1. plugin:@performance/recommended
2. plugin:@performance/all

Code Linter代码检查规则的配置指导请参考[Code Linter代码检查](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-code-linter)。

[性能规则@performance](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-performance "性能规则@performance")

[@performance/bad-deep-clone-check](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-bad-deep-clone-check "@performance/bad-deep-clone-check")
# 代码重构

更新时间: 2025-12-16 15:58

## ArkTS/TS代码重构

### Refactor-Extract代码提取

在编辑器中支持将函数内、类方法内等区域代码块或表达式，提取为新方法/函数（Method）、常量（Constant）、接口（Interface）、变量（Variable）或类型别名（Type Alias）。准确便捷的将所选区域代码从当前作用域内进行提取，提升编码效率。选中所需要提取的代码块，右键单击**Refactor**，选择需要提取的类型。

说明

Refactor-Extract代码提取为类型别名（Type Alias）能力仅TS语言支持。

方法/函数（Method）支持选中代码块或完整语句进行提取：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155826.49022535093655416612873057744047:50001231000000:2800:BB86021E9B699BF40870741353AC44371767580FF1D68715A91F6821D0000F44.gif "点击放大")

在ArkTS语言中，支持将组件调用代码块提取为@Builder装饰器装饰的方法，组件属性调用表达式可提取为@Styles或@Extend装饰器装饰的方法。

**使用方式**：选中需要提取的组件或属性，右键单击**Refactor**，选择**Extract Method...**，组件私有属性可提取为@Extend装饰的方法，通用属性可提取为@Styles或@Extend装饰的方法。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155826.73452895376985694816662106846887:50001231000000:2800:3F4F0E470FAF62895F5B33DDF4EEF0586CD48E9BEA30AE1E0E32730F0B2E7B5D.gif "点击放大")

常量（Constant）支持选中单行表达式进行提取：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155826.60116824233546059101907897644125:50001231000000:2800:FD9070C4BEDC10FD60CB08FD1B8EBE4C992A093871ED9CC9AD7BB7E48188C4F7.gif "点击放大")

接口（Interface）支持选中对象自变量进行提取：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155827.16285274227542455425799190239872:50001231000000:2800:B278A4DE7A2B444672EBC7B30F3F9F0039F1BFCDABCC48741E698A65B7C7C29B.gif "点击放大")

支持选中表达式提取为变量（Variable）：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155827.68349739984860553407929253737559:50001231000000:2800:49109AB7CA3FCF5E4DAF2C4AEDAD6CB789C41B15EA490FBEDBF4DE7B89C9D174.gif "点击放大")

### Refactor-Convert代码转换

编辑器内提供Convert重构能力，支持Convert between named imports and namespace imports等高频转换操作，辅助开发者高效重构代码，提升代码质量。

**表1** Refactor-Convert功能支持清单
|功能|说明|使用方法|支持转换的源码类型|
|:--|:--|:--|:--|
|Convert to class|将JS源码中的function转换为符合ES6标准的类|点击或选中function名，右键单击**Refactor** > **Convert**，或使用快捷键**Ctrl+Alt+Shift+R**（macOS为**Option+Shift+Command+R**），在弹窗中选择转换的方式。<br><br>说明<br><br>若当前工程中已引用该方法，执行Convert to class后，在Find Usages中可查看引用的具体位置，点击**Do Refactor**可忽略冲突并执行转换；也可以逐条修改引用位置的代码后，重新执行上述操作。|JS|
|Convert to anonymous function|将箭头函数转换为匿名函数|选中箭头函数赋值变量，右键单击**Refactor** > **Convert**，或使用快捷键**Ctrl+Alt+Shift+R**（macOS为**Option+Shift+Command+R**），在弹窗中选择转换的方式。|JS/TS|
|Convert to named function|将箭头函数转换为普通函数|选中箭头函数赋值变量，右键单击**Refactor** > **Convert**，或使用快捷键**Ctrl+Alt+Shift+R**（macOS为**Option+Shift+Command+R**），在弹窗中选择转换的方式。|JS/TS/ArkTS|
|Convert to arrow function|将匿名函数转换为箭头函数|选中匿名函数赋值变量，右键单击**Refactor** > **Convert**，或使用快捷键**Ctrl+Alt+Shift+R**（macOS为**Option+Shift+Command+R**），在弹窗中选择转换的方式。|JS/TS/ArkTS|
|Convert default export to named export|支持named export和default export相互转换|完整选中export default语句，右键单击**Refactor** > **Convert**，或使用快捷键**Ctrl+Alt+Shift+R**（macOS为**Option+Shift+Command+R**），在弹窗中选择转换的方式。|JS/TS/ArkTS|
|Convert named export to default export|完整选中export语句，右键单击**Refactor** > **Convert**，或使用快捷键**Ctrl+Alt+Shift+R**（macOS为**Option+Shift+Command+R**），在弹窗中选择转换的方式。|
|Convert named imports to namespace import|支持在命名import和命名空间import形态间转换|完整选中import语句，右键单击**Refactor** > **Convert**，或使用快捷键**Ctrl+Alt+Shift+R**（macOS为**Option+Shift+Command+R**），在弹窗中选择转换的方式。|JS/TS/ArkTS|
|Convert namespace import to named imports|完整选中命名空间import语句，右键单击**Refactor** > **Convert**，或使用快捷键**Ctrl+Alt+Shift+R**（macOS为**Option+Shift+Command+R**），在弹窗中选择转换的方式。|
|Convert to template string|将字符串转换为模板字面量|选中字符串或完整表达式，右键单击**Refactor** > **Convert**，或使用快捷键**Ctrl+Alt+Shift+R**（macOS为**Option+Shift+Command+R**），在弹窗中选择转换的方式。|JS/TS/ArkTS|
|Convert to optional chain expression|将判空逻辑转换为可选链式调用|选中连续判空表达式，右键单击**Refactor** > **Convert**，或使用快捷键**Ctrl+Alt+Shift+R**（macOS为**Option+Shift+Command+R**），在弹窗中选择转换的方式。|JS/TS/ArkTS|

### Refactor-Rename代码重命名

代码编辑支持Rename功能，可以快速更改变量、方法、对象属性等相关标识符及文件、模块的名称，并同步到整个工程中对其进行引用的位置。

**使用方式**：选中需要重新命名的标识符（变量、类、接口、自定义组件等），右键单击**Refactor**，选择**Rename...**（或使用**快捷键Shift+F6**），在弹框中输入新的标识符名称，并在**Scope**中选择替换的范围，点击**Refactor**完成重新命名。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155827.14273555172832627488801407784255:50001231000000:2800:DE9F56A594C0C9BED6B95EBEE69348C517B19AFABAD3EEAB992F1B5610488386.png "点击放大")

代码编辑支持筛选并过滤不需要rename的引用位置。在**Rename...**弹窗中点击**Preview**，在弹出预览窗口中，用户选中无需Rename的选项，单击右键菜单**Exclude****/Remove**进行过滤/删除，完成筛选后点击左下角**Do Refactor**，重新执行Rename操作。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155827.46555380986117187177514818473986:50001231000000:2800:BAAE590B910492E7C47F1B9C2E18B00F0DA965EB22F8FA375761C74439869C7C.png)

说明

若ArkTS文件中存在C++接口调用，使用Rename进行重命名时，C++文件中涉及的函数名也会被重命名。

### Move File

在文件中单击右键，选择**Refactor > Move File...**，在弹窗中输入或点击**...**选择指定的目录，点击**Refactor**，可将当前文件移动至该目录下。勾选**Search for references**，可查找并更新工程中对该文件的引用；勾选**Open in editor**，可在编辑器中查看移动的文件。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155827.02331824426647524008535864577034:50001231000000:2800:837B076B93BC2BE1BBF3F38766A526ECD2183E55609B8A99A0E976333F18072D.png)

### Safe Delete

编辑器支持Safe Delete功能，帮助您安全地删除代码中的标识符对象（变量、函数或类等）或删除指定文件。在删除前，编辑器将先在代码中搜索对该对象的引用，如果存在引用，编辑器将提示您进行必要的检查和调整。

**使用方式**：在编辑器内选中需要删除的标识符对象或在工程目录选择待删除的文件，右键单击**Refactor**，选择**Safe Delete**，单击**OK**将自动检查当前对象在代码中被引用的情况，点击**View Usages**可查看具体使用的代码内容，点击**Delete Anyway**将直接删除该对象的定义。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155827.77508326582698788012554990324108:50001231000000:2800:5E3BC1476701436005BCEFBCE4E354FE07886F9B4F1F9E5687AF1B39B9A1E6BA.png)

## C++代码重构

编辑器提供C++代码重构能力，当前支持展开宏、交换if分支、移动函数体到声明处等使用场景下的重构能力，提升开发效率。

### 展开宏

支持在当前宏引用处展开宏。将光标移动至需要展开的宏，右键单击**Refactor**，选择**Inline**，展开此处引用的宏。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155827.13928331545671811889587250413089:50001231000000:2800:56B6EE8C1387EAAB2EF6A11690600C8EB600ED8676B9B94033142DF43C2CE529.gif)

### 交换if分支

编辑器支持在选中if-else完整代码块的情况下，实现对if-else代码块的位置交换，并对条件取反。

**使用约束**

- 需要重构的代码块必须为完整的if-else代码结构，{}不能省略；
- if-else中的statement包含嵌套if-else语句时，只反转最外层的if-else语句。对于if() -else if()-else() 结构，仅支持对最后一层if-else结构进行交换；
- 不支持赋值语句的判断条件取反。

**使用方式**

编辑器内选择需要转换的代码区域，右键单击**Refactor**，选择**Swap If Branches**，对原有if条件取反，并交换if-else原代码块顺序。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155827.28255951378684252142163205613681:50001231000000:2800:1541B74CB1AF89C844B929C6C76EB47383FFC5FF2D46CC3A6B23E820DABADA0C.gif "点击放大")

### 移动函数体到声明处

编辑器支持将函数体从源文件移动到头文件中，提高代码可读性。编辑器内选中函数名，右键单击**Refactor**，选择**Move to Declaration**，源文件中的函数实现将移动至头文件中。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155827.65641361127853246153815383140606:50001231000000:2800:5B3547B56C3D94E99035B16B56BBB1AFE2D7FDCC7B9ACC417FF9778A2EECC413.gif)

### 移动函数体到实现处

在编辑器内将光标放在或选中函数名，右键单击**Refactor**，选择**Move to Implementation**，选择移动到的文件，将函数定义移动到该文件。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155827.88541307712326242695005643690369:50001231000000:2800:84944F1AB7703AB0275C173A6DD3FF580648D7C7FD70885C00F0F967CC27CE94.gif)

### 将语句转为原始字符串

编辑器提供重构能力，支持将带有 \n, \t, \", \\, \'五类转义字符的字符串转换为原始字符串。当前仅支持标准字符串，不支持 u8""等其他字符串。

在编辑器内选择字符串代码区域，右键单击**Refactor**，选择**Convert To Raw String**，将语句转换为原始字符串。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155827.24250375005446060852397256899911:50001231000000:2800:FFC0F490D957F719B14F5DDAB4D5737D57B156CF932E1EF661FD0473D6E9F7F4.gif "点击放大")

### 定义构造函数

编辑器提供重构能力，支持为类的成员变量生成默认的构造函数。

**规格限制**

1. 不支持未初始化成员变量的类
2. 不支持在(class标识符，类名，大括号)以外的位置触发
3. 不支持类已存在有入参的构造函数

**使用方法：**在类的定义的类名处，右键单击**Generate****...**，选择**Constructor**，在弹框中点击**Define**，为成员变量定义一个构造函数。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155827.30651038603470256838317742690156:50001231000000:2800:5355B0EE828E1D1587E11D63D91EBD504371CE44B152626860F5FB0752A80500.gif)

### 提取表达式到变量

在编辑器内，选中需要提取的表达式范围，右键单击**Refactor**，选择**Extract Variable**，支持提取表达式到变量。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155827.37890255211998637795786338220407:50001231000000:2800:0FC2715D51B14DBCD8E75459B81D23E895D8E2CB3376AA7A7B25E3EAF2700097.gif "点击放大")

### 移除namespace

光标停留在需要移除的namespace处，右键单击**Refactor**，选择**Remove Using Namespace**进行移除，可以避免命名冲突，提高代码可读性。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155827.32081974922383203616066452341737:50001231000000:2800:C1BF9DE43DFDFAA601BE2DC7E239DE9BE27FDDC70D7D59019B3D7F120CB65982.gif)

### 添加using声明

编辑器内，光标停留在需要添加using声明处，右键单击**Refactor**，选择**Add Using**完成使用using定义类型别名。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155827.85794539507220706442713279369505:50001231000000:2800:9EB0D8DB3D5ADCA087CF07C58E97D7B74C9599157A431A9A276C6E3CEE6BEE71.gif)

### auto自动展开

在auto关键字处右键单击**Refactor**，选择**Expand Auto Type**，可以使用推断类型替换auto类型。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155827.84905912206252110704814497031184:50001231000000:2800:2E756D1490351FCE288D2BD1D29706F64F3095E3928D36462D0A9ABB9C2C8A7A.gif)

### 声明隐式成员

编辑器支持在类中声明隐式复制/移动成员。光标停留在需要生成的类处，右键单击**Generate**..., 选择**Copy/Move Members**。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155827.98366212492452129567436272916642:50001231000000:2800:40DD5A5A1E8A18F2FCA65B2154F53328F66032DD7A712C81A345A336D544A0AF.gif)

[@compatibility/api-compatibility-check](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-api-compatibility-check "@compatibility/api-compatibility-check")

[生成ArkTSDoc文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-arktsdoc "生成ArkTSDoc文档")
# 文档生成

更新时间: 2025-12-16 15:58

DevEco Studio支持通过Generate ArkTSDoc功能，将代码文件中变量、方法、接口、类等需要对外暴露的信息快速生成相应的参考文档。

说明

- 当前支持对工程或目录下.ets/.ts/.js/.md格式文件生成ArkTSDoc文档。
- 文件中export的变量、方法、接口、类等将生成相应的ArkTSDoc文档，未export的对象不支持生成。
- 若选择对工程/目录整体导出ArkTSDoc文档，生成后的ArkTSDoc文档目录和原目录结构一致。

## ArkTSDoc生成步骤

1. 在菜单栏选择**Tools >** **Generate ArkTSDoc...**进入ArkTSDoc生成界面。
2. 设置生成ArkTSDoc的范围，可选择整个工程、某个模块或目录、单个文件进行导出。在Output directory中指定导出ArkTSDoc的存储路径。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155837.99954337472192475316632370457663:50001231000000:2800:57E13244D8F6F848EEC472668097B4C1C3BE60B949E6C3BD141A894FC72BBF34.png)
    
3. 若勾选**Open generated documentation in browser**选项，在生成ArkTSDoc后，将自动打开相应页面查看生成的文档。配置完毕后点击Generate，开始扫描并生成ArkTSDoc文档。
    
    生成的ArkTSDoc左侧文档目录和原工程目录结构一致，右侧可点击跳转到当前文件包含的某个变量、方法、接口或类的文档位置。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155837.87426465960446058547178862104505:50001231000000:2800:229045D0645BEEC43378D15012A3D6DBA3FF12618DAB7921E0D4FA46A6518940.png "点击放大")
    
    若没有勾选**Open generated documentation in browser**选项，在生成ArkTSDoc后，DevEco Studio右下角弹出对应提示框，可以点击Go to Folder跳转到生成的ArkTSDoc文件夹，用浏览器打开文件夹中index.html文件即可查看ArkTSDoc文档。
    

## 生成效果示例

**注释格式要求：**当前仅支持“/** */”文档注释格式；支持param等[标准标签](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-arktsdocs-standard-label)和myTag等自定义标签生成相应文档。

1. /**
2.  * Prints "log" logs.
3.  *
4.  * @param { string } message - Text to print.
5.  * @myTag
6.  * @since 11
7.  */

**代码示例：**

1. /**
2.  * Defines the demo class
3.  *
4.  * @since 11
5.  */
6. export class Demo {
7.     /**
8.      * Prints "log" logs.
9.      *
10.      * @param { string } message - Text to print.
11.      * @myTag
12.      * @since 11
13.      */
14.     static log(message: string): void {

15.     }
16. }

**ArkTSDoc文档生成结果：**

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155837.76205190042778908656080672074238:50001231000000:2800:EB070C992DEC405453B0B73800AA7B153739A6C14685A0B15BEE1112221025BA.png "点击放大")

[生成ArkTSDoc文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-arktsdoc "生成ArkTSDoc文档")

[标准标签](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-arktsdocs-standard-label "标准标签")
# 快速插入场景化代码片段

更新时间: 2025-12-16 15:58

DevEco Studio提供Kit Assistant能力，支持通过拖拽方式将基础的场景化的控件/代码片段插入ArkTS工程中，减少高频场景代码的编写时间。

1. 在菜单栏点击**View > Tool Windows > Kit Assistant**，或使用快捷键**Alt + K**（macOS为**O****ption + K**），进入Kit Assistant页面。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155832.12230800685510099307764188651059:50001231000000:2800:87A1BE141AFEE411FA275156DF8BFEF47B8265B159EA0DF725C578C382D9868D.png)
    
2. 在左侧目录中支持搜索、查看不同Kit提供的场景化控件或代码片段。Kit Assistant面板右侧展示该控件的使用约束、适用场景等详细信息。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155832.93575197090796849944374495624278:50001231000000:2800:490CC6725ED466B7093F4CAF949F26BE25588A3A9AFECA6F1BC5C11473846090.png)
    
3. 在目录中点击选中需要的控件或功能代码，并拖拽至.ets文件中适当位置，即可在当前位置插入相应的代码片段。
    
    说明
    
    若当前编辑器打开的文件或所在的模块，存在某些Kit能力不支持的设备类型/API版本/工程模型，或某些Kit能力或控件不支持在元服务工程中使用，则Kit Assistant目录中该Kit能力或控件将置灰并无法成功拖拽。
    

[{@link}](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-arktsdoc-link "{@link}")

[跨语言代码编辑](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-cross-language-code-editing "跨语言代码编辑")
# 跨语言代码编辑

更新时间: 2025-12-16 15:58

## 生成胶水代码函数框架

DevEco Studio提供跨语言代码编辑功能。当开发者需要使用NAPI封装暴露给ArkTS/JS的接口时，在Cpp头文件内，通过右键Generate > NAPI，快速生成当前函数或类的胶水代码函数框架。

1. 检查当前Cpp工程entry > src > main > cpp路径下，是否已包含napi_init.cpp文件。如不存在该文件，请在头文件（头文件支持类型：.hpp，.hxx，.hh，.h）中，将光标放置在任意函数名/类名处（当前支持bool，int，string，void，float，double，std::array，std::vector等参数类型），单击右键选择Generate > NAPI，生成胶水代码框架文件napi_init.cpp。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155834.43362592170512304396284955907345:50001231000000:2800:D5F4CCB2264C92C3CE31A0005A5C4C4C43ED642273B12F8159C6AFD9EC7BF3F6.png "点击放大")
    
2. 若工程中已存在或创建完成napi_init.cpp文件，请在头文件中需要被调用的函数/类名处，单击右键选择Generate > NAPI，将在napi_init.cpp文件napi_property_descriptor字段中分别注册对应的函数/类的信息。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155834.36819935608805017435718568257266:50001231000000:2800:3D82FE05551CCC785C5F067116043368CF1E50F88F238103FFDC6445A4BD2261.png)
    
3. 在napi_init.cpp文件中TODO位置，补充相应的功能实现代码。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155834.96339174745906713645396482675607:50001231000000:2800:F92A7B3E64EE1EDE72473D0AF253353FC3ECDF45E34119D90A8AAE5F34DF30FA.png)
    

## 跨语言快速生成函数定义

当前支持在跨语言的d.ts文件中，通过Generate native implementation功能，一键生成C++文件中对应函数定义。

将光标悬浮在未定义的函数名处，在悬浮窗中点击**Generate native implementation**，或点击页面上出现的红色灯泡图标，选择**Generate native implementation**，生成函数定义。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155834.76230325134255389739941420933678:50001231000000:2800:9EC87736D3DD114B15847EC22F815F5725C42C0CCD796992E620F188A4A22E08.gif)

[快速插入场景化代码片段](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-kit-assistant "快速插入场景化代码片段")

[界面预览](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-previewer-01 "界面预览")
# 查看ArkTS/JS预览效果

更新时间: 2025-12-16 15:58

预览器支持ArkTS/JS应用/元服务“实时预览”和“动态预览”。

说明

- 预览支持Phone、Tablet、2in1、Car、Wearable、TV设备的ArkTS工程，支持LiteWearable和Wearable设备的JS工程。
- 预览器功能依赖于电脑显卡的OpenGL版本，OpenGL版本要求为3.2及以上。
- 预览时将不会运行Ability生命周期。
- 从DevEco Studio 6.0.0 Beta3版本开始，HAP/HSP引用HSP时支持预览，HAR模块引用HSP不支持预览，请直接在HSP内预览或为该HSP[设置Mock实现](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-previewer-mock)。
- 预览场景下，不支持通过相对路径及绝对路径的方式访问resources目录下的文件。
- 预览不支持组件拖拽。
- 部分API不支持预览，如Ability、App、MultiMedia等模块。
- Richtext、Web、Video、XComponent组件不支持预览。
- 不支持调用C++库的预览。
- har在被应用/元服务使用时真机效果有区别，真机上实际效果应用不显示menubar，元服务显示menubar，但预览器都以不显示menubar为准。若开发har模块时，请注意被元服务使用时预览器效果与真机效果的不同。

- **实时预览**：在开发界面UI代码过程中，如果添加或删除了UI组件，您只需**Ctrl+S**进行保存，然后预览器就会立即刷新预览结果。如果修改了组件的属性，则预览器会实时（亚秒级）刷新预览结果，达到极速预览的效果（当前版本极速预览仅支持ArkTS组件。支持部分数据绑定场景，如@State装饰的变量）。实时预览默认开启，如果不需要实时预览，请单击预览器右上角![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155825.57952324375102495685401349773931:50001231000000:2800:3281D6F2FC0F38CF85E86BE4FBD11F861E92E4AF9E075A13B5C4779D1E913047.png)按钮，关闭实时预览功能。
    
    说明
    
    开发者修改resources/base/profile目录下的配置文件（如main_pages.json/form_config.json），不支持触发实时预览，开发者需要点击重新加载![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155825.89029645711339110154970820557918:50001231000000:2800:A44428850141A9F71564E3451A230F6591310333B32D380DA32EEC41B3CF7AD0.png)。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155825.09577558805742612600307217215358:50001231000000:2800:4DB06DA16982FFD468E7C4F27F95571801554BDD6DA846B0507CB3E06D82B621.gif)
    
- **动态预览**：在预览器界面，可以在预览器中操作应用/元服务的界面交互动作，如单击、跳转、滑动等，与应用/元服务运行在真机设备上的界面交互体验一致。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155825.34754623138989995591975404797916:50001231000000:2800:2CB592BF2A72B5783CCBF0742F3EED6C0A3903CC77909212A6498EC51AC43FC0.gif)
    

以ArkTS为例，使用预览器的方法如下：

1. 创建或打开一个ArkTS应用/元服务工程。本示例以打开一个本地ArkTS Demo工程为例。
2. 在工程目录下，打开任意一个.ets文件（JS工程请打开.hml/.css/.js页面）。
3. 可以通过如下任意一种方式打开预览器，启动预览。
    
    - 通过菜单栏，单击**View > Tool Windows > Previewer**打开预览器。
    - 在编辑窗口右上角的侧边工具栏，单击**Previewer**，打开预览器。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155825.14138994215834983207655200521878:50001231000000:2800:4A5291C4000A8571586DD24172D13306CCF443CE0562069EF878A87641EF75F5.png)
    
4. 点击按钮![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155825.98342904309917652415098803569710:50001231000000:2800:6ADBFA87E7CE90EDD2C49233223FE8E748CA656010B20CE200AC111C8C263678.png)，停止预览。

[PreviewChecker检测规则](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-previewer-previewchecker "PreviewChecker检测规则")

[查看ArkUI预览效果](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-previewer-arkui "查看ArkUI预览效果")
# 查看ArkUI预览效果

更新时间: 2025-12-16 15:58

ArkUI预览支持页面预览、组件预览和卡片预览，下图中左侧图标![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155828.74226791156821072030714282449822:50001231000000:2800:17AB498808D90BB1DEC7D51061F1C109D653B17C19A15568669B10E16F94BD7B.png)为页面预览，右侧图标![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155828.21942530265117851118839826760568:50001231000000:2800:D807B490D88D890C38CC61BB3819CC71CC8D7C56EC7AC8C8F54509C074FD9ECE.png)为组件预览，卡片预览在创建卡片文件后可直接预览。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155828.63931149790118592246216115187482:50001231000000:2800:34963B93E125A3CF03D8FE9C4293ABEB35D8066A7805E64675A0A9D1AED540F7.png)

## 页面预览

ArkTS应用/元服务支持页面预览。页面预览通过在工程的ets文件头部添加@Entry实现。

@Entry的使用参考如下示例：

1. @Entry
2. @Component
3. struct Index {
4.   @State message: string = 'Hello World'

5.   build() {
6.     Row() {
7.       Column() {
8.         Text(this.message)
9.           .fontSize(50)
10.           .fontWeight(FontWeight.Bold)
11.       }
12.       .width('100%')
13.     }
14.     .height('100%')
15.   }
16. }

## 组件预览

ArkTS应用/元服务支持组件预览。组件预览支持实时预览，不支持动态图和动态预览。组件预览通过在组件前添加注解@Preview实现，在单个源文件中，最多可以使用10个@Preview装饰自定义组件。

@Preview的使用参考如下示例：

1. @Preview({
2.   title: 'ContentTable'
3. })
4. @Component
5. struct ContentTablePreview {
6.   build() {
7.     Flex() {
8.       ContentTable({ foodItem: getDefaultFoodData() })
9.     }
10.   }
11. }

以上示例的组件预览效果如下图所示：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155828.34917648690192618803043253665045:50001231000000:2800:02C7197248BE9B345F3B901193EFD00EB1B61C129DB3CF7B695E745BF8E83FC1.gif)

组件预览默认的预览设备为Phone，若您想查看不同的设备，或者不同的屏幕形状，或者不同设备语言等情况下的组件预览效果，可以通过设置@Preview的参数，指定预览设备的相关属性。若不设置@Preview的参数，默认的设备属性如下所示：

1. @Preview({
2.   title: 'Component1',  //预览组件的名称
3.   deviceType: 'phone',  //指定当前组件预览渲染的设备类型，默认为Phone
4.   width: 1080,  //预览设备的宽度，单位：px
5.   height: 2340,  //预览设备的长度，单位：px
6.   colorMode: 'light',  //显示的亮暗模式，当前支持取值为light
7.   dpi: 480,  //预览设备的屏幕DPI值
8.   locale: 'zh_CN',  //预览设备的语言，如zh_CN、en_US等
9.   orientation: 'portrait',  //预览设备的横竖屏状态，取值为portrait或landscape
10.   roundScreen: false  //设备的屏幕形状是否为圆形
11. })

请注意，如果被预览的组件是依赖参数注入的组件，建议的预览方式是：定义一个组件片段，在该片段中声明将要预览的组件，以及该组件依赖的入参，并在组件片段上标注@Preview注解，以表明将预览该片段中的内容。例如，要预览如下组件：

1. @Component
2. struct Title {
3.   @Prop context: string; 
4.   build() {
5.     Text(this.context)
6.   }
7. }

建议按如下方式预览：

1. @Preview
2. @Component    //定义组件片段TitlePreview
3. struct TitlePreview {
4.   build() {
5.     Title({ context: 'MyTitle' })    //在该片段中声明将要预览的组件Title，以及该组件依赖的入参 {context: 'MyTitle'}
6.   }
7. }

## 卡片预览

创建卡片并选中卡片文件后，点击右侧边栏**Previewer**按钮即可预览卡片。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155828.50446976110614185771895109399039:50001231000000:2800:47C6350DB9C19EFBF96A811DC4DAEF3945F9E9C5D53ACA9D20E11BCD6B894397.png)

[查看ArkTS/JS预览效果](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-previewer-arkts-js "查看ArkTS/JS预览效果")

[Profile Manager](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-previewer-profile-manager "Profile Manager")
# Profile Manager

更新时间: 2025-12-16 15:58

由于真机设备有丰富的设备型号，不同设备型号的屏幕分辨率可能不一样。因此，在HarmonyOS应用/元服务开发过程中，由于设备类型繁多，可能需要查看在不同设备上的界面显示效果。对此，DevEco Studio的预览器提供了Profile Manager功能，支持开发者自定义预览设备Profile（包含分辨率和语言），从而可以通过定义不同的预览设备Profile，查看HarmonyOS应用/元服务在不同设备上的预览显示效果。当前支持自定义设备分辨率及系统语言。

定义设备后，可以在Previewer右上角，单击![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155828.42461707720224380251414240022099:50001231000000:2800:4DC1E9A004EE5CC5AF11DC64C43142879EB5E34B26A1D0796E06643684F874DD.png)按钮，打开Profile管理器，切换预览设备。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155829.32020922217389250338659814377416:50001231000000:2800:6A68E69BF9690543D635D1D798E5E12680C4500A79BBE96046AFD3A0134DE9A7.png)

同时，Profile Manager还支持多设备预览功能，具体请参考[查看多端设备预览效果](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-previewer-multi-profile)。

下面以自定义一款Phone设备为例，介绍设备Profile Manager的使用方法。

1. 在预览器界面，打开Profile Manager界面。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155829.75906976839946202435655074220267:50001231000000:2800:6EE50375A5F6CC0CA335EDEBA59A01890C2E456DB724499F236E82AC554C6688.png)
    
2. 在Profile Manager界面，单击**+ New Profile**按钮，添加设备。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155829.60659943425424056451481666129946:50001231000000:2800:7796C1E30749ECFB8609283FE38F9812FB3D52F29760DA01DB93C89D1227EA04.png)
    
3. 在**Create Profile**界面，填写新增设备的信息，如**Profile ID**（设备型号）、**Device type**（设备类型）、**Resolution**（分辨率）和**Language and region**（语言和区域）等。其中Device type只能选择module.json5中deviceTypes字段已定义的设备。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155829.55292636190606290748353460959319:50001231000000:2800:35661A5E72ED30C665A1B90C1D207907843385FDC84F872276C4D159E27CBC9E.png)
    
4. 设备信息填写完成后，单击**OK**完成创建。

[查看ArkUI预览效果](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-previewer-arkui "查看ArkUI预览效果")

[查看多端设备预览效果](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-previewer-multi-profile "查看多端设备预览效果")
# 查看多端设备预览效果

更新时间: 2025-12-16 15:58

DevEco Studio支持HarmonyOS分布式应用/元服务开发，同一个应用/元服务可以运行在多个设备上。在HarmonyOS分布式应用/元服务的开发阶段，因不同设备的屏幕分辨率、形状、大小等不同，开发者需要在不同的设备上查看应用/元服务的UI布局和交互效果，此时便可以使用多端设备预览器功能，方便开发者在应用/元服务开发过程中，随时查看不同设备上的界面显示效果。

说明

多端设备预览最多同时支持4个设备的预览。

前面介绍了DevEco Studio支持ArkTS、JS应用/元服务的预览器功能，多端设备预览器支持ArkTS、JS应用/元服务在不同设备上的同时预览。如果两个设备支持的编码语言不同，就不能使用多端设备预览功能。

下面以ArkTS应用/元服务为例，介绍多端设备预览器的使用方法，JS应用/元服务的多端设备预览器使用方法相同。

1. 在工程目录中，打开任意一个ets文件（JS请打开hml/css/js文件）。
2. 可以通过如下任意一种方式打开预览器开关，显示效果如下图所示：
    
    - 通过菜单栏，单击**View > Tool Windows > Previewer**，打开预览器。
    - 在编辑窗口右上角的侧边工具栏，单击**Previewer**，打开预览器。
    
3. 在Previewer窗口中，打开Profile Manager中的**Multi-profile preview**开关，同时查看多设备上的应用/元服务运行效果。
    
    说明
    
    多端设备预览不支持动画的预览，如果需要查看动画在设备上的预览效果，请关闭Multi-profile preview功能后在单设备预览界面进行查看。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155832.54818615727278666924638279357992:50001231000000:2800:64BC2C3135A8088836A5611402FEB66321B868896935DFA7DE033E2118AAA79E.png)
    
    多设备预览效果如下图所示：
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155832.37151739077561908373400242145596:50001231000000:2800:FFB9F489B05F811E6DB40EE92565ACF43A816AD39651029B910CEF07ADABBFB1.gif)
    

[Profile Manager](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-previewer-profile-manager "Profile Manager")

[Inspector双向预览](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-previewer-inspector "Inspector双向预览")
# Inspector双向预览

更新时间: 2025-12-16 15:58

DevEco Studio提供HarmonyOS应用/元服务的UI预览界面与源代码文件间的双向预览功能，支持ets文件与预览器界面的双向预览。使用双向预览功能时，需要在预览器界面单击![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155834.66532853828847730111098131631777:50001231000000:2800:FE05EC1F3BDB9BEE9D435483F455D0040A3FE013FBC77C2CB04A901FE2716D0D.png)图标打开双向预览功能。

说明

不支持服务卡片的双向预览功能。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155834.27523625731752152331030901547607:50001231000000:2800:E9DDE75A59B1B59D152F5A4879B8A61E8889B773E89E221FE9C361EFA6FF0445.png)

开启双向预览功能后，支持代码编辑器、UI界面和Component Tree组件树三者之间的联动：

- 选中预览器UI界面中的组件，则组件树上对应的组件将被选中，同时代码编辑器中的布局文件中对应的代码块高亮显示。
- 选中布局文件中的代码块，则在UI界面会高亮显示，组件树上的组件节点也会呈现被选中的状态。

- 选中组件树中的组件，则对应的代码块和UI界面也会高亮显示。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155834.17008042405700900456122960156893:50001231000000:2800:9472A80F6FC555BC103AAC364B201EDE13801030160A4866DA5FBB3F45F105FD.png "点击放大")

在预览界面还可以通过组件的属性面板修改可修改的属性或样式，在预览界面修改后，预览器会自动同步到代码编辑器中修改源码，并实时的刷新UI界面；同样的，如果在代码编辑器中修改源码，也会实时刷新UI界面，并更新组件树信息及组件属性。

说明

- 如果组件有做数据绑定，则其属性不支持在属性面板修改。
- 如果界面有使用动画效果或者带动画效果组件，则其属性不支持在属性面板修改。
- 多设备预览时，不支持双向预览。

[查看多端设备预览效果](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-previewer-multi-profile "查看多端设备预览效果")

[预览数据模拟](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-previewer-mock "预览数据模拟")
# 预览数据模拟

更新时间: 2025-12-16 15:58

说明

仅API 11及以上版本的Stage工程支持。

在预览场景中，由于代码的运行环境与真机设备上的运行环境不同，调用部分接口时无法获取到有效的返回值（例如获取电池电量信息等，在预览场景下batteryInfo.voltage返回的是一个固定的值0），这样开发者就无法在预览时查看到不同返回值带来的界面变化。因此，Hamock提供了预览场景的模拟功能，在不改变业务运行逻辑的同时，开发者可以模拟UI组件上的属性或方法，或模拟import的模块接口。

## 使用前提

使用Hamock在预览场景模拟，需要在工程或模块的oh-package.json5中添加该依赖，然后重新同步工程。

1. "devDependencies": {
2.     "@ohos/hamock": "1.0.0"
3. }

## UI组件上的Mock

Hamock提供了@MockSetup用于修饰Mock方法，仅支持声明式范式的组件。当开发者预览该组件时，预览运行时将在组件初始化时执行被@MockSetup修饰的方法。因此，开发者可以在这个被修饰的方法内重定义组件的方法或重赋值组件的属性，其将在预览时生效。

说明

@MockSetup修饰的方法仅在预览场景会自动触发，并先于组件的aboutToAppear执行。

### UI组件的方法

1. 在ArkTS页面代码中引入Hamock。
    
    1. import { MockKit, when, MockSetup } from '@ohos/hamock';
    
2. 在目标组件中定义一个方法，并用@MockSetup修饰该方法。在这个方法中，使用MockKit模拟目标方法。
    
    1. import { MockKit, when, MockSetup } from '@ohos/hamock';
    
    2. @Entry
    3. @Component
    4. struct Index {
    5.  ...
    6.  @MockSetup
    7.  randomName() {
    8.   let mocker: MockKit = new MockKit();
    9.   let mockfunc: Object = mocker.mockFunc(this, this.method1);
    10.   // mock 指定的方法在指定入参的返回值
    11.   when(mockfunc)('test').afterReturn(1);
    12.  }
    13.  ...
    14.  // 业务场景调用方法
    15.  const result = this.method1('test'); // in previewer, result = 1
    16. }
    

### UI组件的属性

1. 在ArkTS页面代码中引入Hamock。
    
    1. import { MockSetup } from '@ohos/hamock';
    
2. 在目标组件中定义一个方法，并用@MockSetup修饰该方法。在这个方法中，对于需要Mock的属性，可以重新赋值。
    
    1. import { MockSetup } from '@ohos/hamock';
    
    2. @Component
    3. struct Person {
    4.  @Prop species: string;
    5.  // 在@MockSetup片段中，定义对象属性
    6.  @MockSetup
    7.  randomName() {
    8.   this.species = 'primates'
    9.  }
    10.  ...
    11.  // 业务场景调用属性（如果从初始化到调用期间，该属性无变化）
    12.  const result = this.species // in previewer, result = primates
    13. }
    

说明

- ArkUI部分类型属性不支持Mock，如readonly、@ObjectLink。
- 被@Link/@Consume/@Prop/@BuilderParam装饰器修饰的变量，ArkUI语法要求父容器需要有对应属性的定义，因此更推荐开发者通过定义⼀个预览场景父容器（并通过父容器传递合适的数据）来预览这⼀类的组件。

## 模块的Mock

模块的Mock支持对系统模块、依赖模块及本地模块的Mock，通过新建ArkTS文件定义Mock实现代码，并在mock-config.json5配置文件中定义目标模块与Mock实现代码文件的映射关系。目标模块与Mock实现代码文件为一对一的关系，即对于同一目标模块，仅支持一份Mock实现代码，预览运行时，所有页面import目标模块都将指向这一份Mock实现代码。

### 系统模块/依赖的模块

1. 在src/mock目录下新建一个ArkTS文件，在这个文件内定义目标模块的Mock实现。
    
    1. // src/mock/MeasureText.mock.ets
    2. import MeasureText from '@ohos.measure'
    
    3. // 类的mock使用继承(extends)的方式实现
    4. class MockMeasureText extends MeasureText {
    5.   // 定义mock实现
    6.   static measureText(): number {
    7.     console.log('Return value of the mock measureText function')
    8.     return 100;
    9.   }
    10. };
    
    11. export default MockMeasureText;
    
    说明
    
    用户在对类定义Mock的实现时，需要使用继承(extends)的方式实现。
    
2. 在Mock配置文件src/mock/mock-config.json5中定义目标模块与Mock实现的替换关系。该替换关系会在预览场景下生效。
    
    1. {
    2.   "@ohos.measure": { // 待替换的moduleName
    3.     "source": "src/mock/MeasureText.mock.ets" // Mock代码的路径，相对于模块根目录
    4.   },
    5.  ...
    6. }
    
3. 在原调用处中添加Hilog日志，方便在预览时，在Log中打印获取返回值，从而验证Mock是否生效。
    
    1. hilog.debug(DomainNumber, logTag, 'Mock %{public}s', `${MeasureText.measureText({textContent: 'Hello World'})}`)
    

### 本地模块

1. 在src/mock目录下新建一个ArkTS文件，在这个文件内定义目标模块的Mock实现。
    
    1. // src/mock/module/utils/CommonUtils.mock.ts
    2. // import local module
    3. import LibDefaultExport from '../../../main/ets/utils/CommonUtils'; // get origin default export
    4. import { methodA, ObjectB } from '../../../main/ets/utils/CommonUtils'; // get origin export on demand
    
    5. class DefaultExportMock extends LibDefaultExport {
    6.   // 定义mock实现
    7.   public static getName(): String {
    8.     return "Mocked Name";
    9.   }
    10. };
    
    11. export {
    12.   methodA,
    13.   ObjectB,
    14. }
    
    15. export default DefaultExportMock;
    
    其中CommonUtils.ets文件示例如下：
    
    16. export default class CommonUtils {
    17.   public static getName(): String {
    18.     return "origin name";
    19.   }
    
    20.   public static getTitle(): String {
    21.     return "origin title";
    22.   }
    23. }
    
    24. export const methodA = (): string => {
    25.   return "methodA"
    26. }
    
    27. export const ObjectB: Object = new Object();
    
    说明
    
    本地模块的Mock仅支持src/main/ets目录下的ArkTS或TS文件。
    
2. 在Mock配置文件src/mock/mock-config.json5中定义目标模块与Mock实现的替换关系。该替换关系会在预览场景下生效。
    
    1. {
    2.  "utils/CommonUtils.ets": { // 本地模块只支持ets/xxx的相对路径，并需明确文件后缀
    3.   "source": "src/mock/module/utils/CommonUtils.mock.ts"
    4.  },
    5.  ...
    6. }
    
3. 在原调用处中添加Hilog日志，方便在预览时，在Log中打印获取返回值，从而验证Mock是否生效。
    
    1. hilog.debug(DomainNumber, logTag, 'Mock %{public}s', CommonUtils.getName());
    

[Inspector双向预览](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-previewer-inspector "Inspector双向预览")

[使用预览器调试应用](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-previewer-debug "使用预览器调试应用")
# 使用预览器调试应用

更新时间: 2025-12-16 15:58

使用真机或模拟器进行调试时，修改后的代码需要经过较长时间的编译和安装过程，才能刷新至调试环境。使用预览器进行调试，可快速地修改代码和运行应用，在DevEco Studio中直接查看修改后的界面显示效果。

开发者可以使用预览器运行调试Ability生命周期代码和界面代码，预览器调试支持基础调试能力，包括断点、调试执行、变量查看等。

## 使用约束

- 一个工程内不支持启动多个预览调试任务。
- 一个预览器只能支持普通预览或预览调试模式，不可同时支持两种模式。
- 使用预览器进行调试不支持以下场景：
    - 不支持Attach调试。
    - 不支持跨Ability调试。
    - 不支持C++调试。
    - 不支持Hot Reload。
    - 不支持多进程和worker/taskpool调试。

## 普通预览与预览调试能力对比

|   |   |   |   |
|---|---|---|---|
**表1** 普通预览与预览调试能力对比
|**功能**|**普通预览**|**预览调试**|   |
|**页面预览**|**运行模式**|**调试模式**|
|ets页面预览|支持|支持|支持|
|动态预览|支持|支持|支持|
|指定页面文件预览|支持|不支持|不支持|
|Inspector双向预览|支持|从DevEco Studio 6.0.0 Beta2版本开始支持|从DevEco Studio 6.0.0 Beta2版本开始，支持查看，不支持修改|
|实时预览|支持|支持|断点中断时不支持|
|极速预览|支持|从DevEco Studio 6.0.0 Beta2版本开始支持|不支持|
|组件预览|支持|不支持|不支持|
|多语言切换|支持|从DevEco Studio 6.0.0 Beta2版本开始支持|从DevEco Studio 6.0.0 Beta2版本开始支持，但断点中断时不支持|
|动态修改分辨率|支持|从DevEco Studio 6.0.0 Beta2版本开始，支持横竖屏切换|从DevEco Studio 6.0.0 Beta2版本开始，支持横竖屏切换，但断点中断时不支持|
|引用HSP|从DevEco Studio 6.0.0 Beta3版本开始支持|   |   |

[预览数据模拟](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-previewer-mock "预览数据模拟")

[支持使用预览器的API清单](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-previewer-api-list "支持使用预览器的API清单")
# 支持使用预览器的API清单

更新时间: 2025-12-16 15:58

## 组件

### ArkTS组件

|组件|API|
|:--|:--|
|基础组件|AlphabetIndexer|
|Blank|
|Button|
|Checkbox|
|CheckboxGroup|
|DataPanel|
|DatePicker|
|Divider|
|Gauge|
|Image|
|ImageAnimator|
|ImageSpan|
|LoadingProgress|
|Marquee|
|Menu|
|MenuItem|
|MenuItemGroup|
|Navigation|
|NavRouter|
|NavDestination|
|PatternLock|
|Progress|
|QRCode|
|Radio|
|Rating|
|ScrollBar|
|Search|
|Select|
|Slider|
|Span|
|Stepper|
|StepperItem|
|Text|
|TextArea|
|TextClock|
|TextInput|
|TextPicker|
|TextTimer|
|Toggle|
|容器组件|Badge|
|Column|
|ColumnSplit|
|Counter|
|Flex|
|FlowItem|
|GridCol|
|GridRow|
|List|
|ListItem|
|ListItemGroup|
|Navigator|
|Panel|
|Refresh|
|RelativeContainer|
|Row|
|RowSplit|
|Scroll|
|SideBarContainer|
|Stack|
|Swiper|
|Tabs|
|TabContent|
|WaterFlow|
|绘制组件|Circle|
|Ellipse|
|Line|
|Polyline|
|Path|
|Rect|
|Shape|
|画布组件|Canvas|
|CanvasGradient|
|CanvasPattern|
|CanvasRenderingContext2D|
|ImageBitmap|
|ImageData|
|Matrix2D|
|OffscreenCanvasRenderingContext2D|
|Path2D|

### JS组件

|组件|API|
|:--|:--|
|基础组件|button|
|chart|
|divider|
|image|
|image-animator|
|input|
|label|
|marquee|
|menu|
|option|
|picker|
|picker-view|
|piece|
|progress|
|qrcode|
|rating|
|search|
|select|
|slider|
|span|
|switch|
|text|
|textarea|
|toolbar|
|toolbar-item|
|toggle|
|容器组件|badge|
|dialog|
|div|
|form|
|list|
|list-item|
|list-item-group|
|panel|
|popup|
|refresh|
|stack|
|stepper|
|stepper-item|
|swiper|
|tabs|
|tab-bar|
|tab-content|
|画布组件|canvas|
|CanvasRenderingContext2D|
|Image|
|CanvasGradient|
|ImageData|
|Path2D|
|ImageBitmap|
|OffscreenCanvas|
|OffscreenCanvasRenderingContext2D|
|栅格组件|grid-container|
|grid-row|
|grid-col|
|svg组件|svg|
|rect|
|circle|
|ellipse|
|path|
|line|
|polyline|
|polygon|
|text|
|tspan|
|textPath|
|animate|
|animateMotion|
|animateTransform|

## 接口

### UI界面

|模块|API|
|:--|:--|
|@ohos.animator (动画)|Animator|
|AnimatorResult|
|AnimatorOptions|
|@ohos.mediaquery (媒体查询)|matchMediaSync|
|MediaQueryResult|
|MediaQueryListener|
|@ohos.promptAction (弹窗)|showToast|
|showDialog|
|showActionMenu|
|ShowToastOptions|
|Button|
|ShowDialogSuccessResponse|
|ShowDialogOptions|
|ActionMenuSuccessResponse|
|ActionMenuOptions|
|@ohos.router (页面路由)|pushUrl|
|replaceUrl|
|back|
|clear|
|getLength|
|getState|
|enableAlertBeforeBackPage|
|disableAlertBeforeBackPage|
|getParams|
|RouterMode|
|RouterOptions|
|RouterState|
|EnableAlertOptions|

### 网络管理

|模块|API|
|:--|:--|
|@ohos.net.http (数据请求)|http.createHttp<br><br>如果Http请求需要配置代理才能访问，API 12及以上的预览器支持使用系统的http_proxy/https_proxy/no_proxy环境变量。|

### 数据管理

|模块|API|
|:--|:--|
|@ohos.data.preferences (用户首选项)|data_preferences.getPreferences|
|data_preferences.deletePreferences|
|data_preferences.removePreferencesFromCache|
|Preferences|
|ValueType|

### 文件管理

从DevEco Studio 6.0.0 Beta5版本开始，仅支持在预览/预览调试Stage模型的HAP/HSP时，使用文件管理的相关API，并且需要先打开**Enable file operation**开关。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155836.18279119716189057183090535272472:50001231000000:2800:6C852E1CEEAC5DCA9DBBCF2AE041DACA5670CD849B59DDE4944D90EC7CB097BD.png)

|模块|API|
|:--|:--|
|@ohos.file.fs (文件管理)|fs.open|
|fs.close|
|fs.fdatasync|
|fs.fsync|
|fs.read|
|fs.write|
|fs.mkdir|
|fs.mkdtemp|
|fs.rename|
|fs.rmdir|
|fs.unlink|
|fs.stat|
|fs.truncate|

[使用预览器调试应用](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-previewer-debug "使用预览器调试应用")

[配置调试签名](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing "配置调试签名")
# 使用仿真器运行轻量级穿戴应用

更新时间: 2025-12-16 15:58

DevEco Studio提供的**Simulator**可以运行和调试Lite Wearable设备上的HarmonyOS应用，兼容签名与不签名两种类型的HAP。

## 操作步骤

1. 在DevEco Studio右上角的设备框中选择**Huawei Lite Wearable Simulator。**
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155812.42102936304212653386209335837007:50001231000000:2800:723186763962839348C8C8E0A622525FB5221D20619889278F638AECAB28FD96.png)
    
2. 点击**Run** ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155812.08084707982390229750097840579555:50001231000000:2800:9A48F240955BEF5B593BC9E2C7AB25F4AD317DEE362D5AED9585B39C1748584E.png)或**Debug** ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155813.08103934683018527486121364226255:50001231000000:2800:F515A2DC7DA954232013DBA634B7D318B49E2CBA72E863C32CFCE4424DD69B88.png)按钮，在弹框中选择设备形状和分辨率，点击**OK**按钮，开始运行或调试应用。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155813.01251819743178912389935756879672:50001231000000:2800:F12436E05E9D3B24E37A4C522C4A1D3DE3B6E3FC9B76C16C9BF8BDFB87D88DC8.png "点击放大")
    
3. DevEco Studio会启动编译构建和安装，完成后应用即可运行在Simulator上。

## 功能介绍

在Simulator界面中，点击设备上方的**More**可展开更多功能。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155813.11955936062531119325997947546605:50001231000000:2800:33C7847EC26EE48ABF0695A36CAB8B202567C84F7E0F1A1A44C956C79EDC949A.png "点击放大")

### 屏幕

- **Turn screen on：**控制屏幕开关。
- **Keep screen on：**控制屏幕是否保持常亮状态。关闭开关时，息屏计时结束后，屏幕自动关闭，同时**Turn screen on**开关自动关闭。开启屏幕后，打开**Keep screen on**开关才能使屏幕常亮。
- **Brightness adjustment mode：**调节屏幕亮度。
    - **Manual：**手动调节，可拖动滑动条，或直接输入亮度。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155813.81891681890448868055195615278134:50001231000000:2800:5FEE018D239B3908E12B465C35109B7C960BA98E10B3AE738F69E041E688E71B.png)
        
    - **Automatic：**自动调节。
- **Resolution：**运行/调试模式下暂不支持调整分辨率，如需调整，请停止运行后，按照[操作步骤](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-run-simulator#section1332819367496)选择分辨率。

### 传感器

仿真器提供了虚拟传感器来模拟硬件传感器的能力。在该界面，您可以调节不同的传感器来测试您的应用，使用[@system.sensor](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-system-sensor)模块监听传感器值的变化，使用[@system.geolocation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-system-location)模块监听地理位置的变化。仿真器提供以下虚拟传感器：

- **On-body status**：传感器所在设备穿戴状态，包括已穿戴和未穿戴。
- **Barometer：**气压传感器用于测量环境气压，单位为Pa。
- **Heart rate：**心率传感器用于测量心率数值，拖动滑动条，或直接输入心率大小。
- **Step count：**计步传感器用于统计行走步数，拖动滑动条，或直接输入步数。
- **Geographic location：**输入经度、纬度，模拟设备所处的地理位置。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155813.50770284466856789189063059715280:50001231000000:2800:343686F004C82EA033CB7816520590F8B7F775902B4BD7C7581636577697EE89.png)

### 电池

您可以通过仿真器模拟不同的电池状态，包括以下三种充电状态，也可以手动输入或拖动滑动条来改变电量大小。在应用中，您可以通过[@system.battery](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-system-battery)模块查询仿真器的剩余电量以及充电状态。

- Not charging：未充电。
- Charging：正在充电。
- Wireless charging：无线充电。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155813.84188326877619990071507581433662:50001231000000:2800:862DF011B71C9F46E8B714C32CF4F637B9A8CD4E3C2BC02DF782B7279BBCEFD2.png)

### 设备设置

您可以更改设备的语言和地区，当前仅运行模式可以更改，调试模式暂不支持。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155813.76424311131264936105981369406736:50001231000000:2800:44B71E485662D80D0036B041924295D5ECAD48D051882B491D56E7E47ADBB09A.png)

### 调试

- **Screen coordinate system****：**开启屏幕坐标系后，将光标移动到表盘上时，会显示屏幕坐标。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155813.32422772720459637309632360270579:50001231000000:2800:1585C31EEC850B0FC6D8773274C0ABC05CED5F118A7A036154EECB3DAADA60B4.gif "点击放大")
    
- **Show device mask****：**关闭开关后，表盘周围的表冠颜色淡化。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155813.32575327342751054639988654194064:50001231000000:2800:B77C3022417FAE16DCFF6B940942A70C640FE6A25642244A274BE4A6486967E5.gif "点击放大")
    

[使用本地真机运行应用](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-run-device "使用本地真机运行应用")

[使用模拟器运行应用](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-run-emulator "使用模拟器运行应用")
# 使用环境

更新时间: 2025-12-16 15:58

模拟器在本地计算机上创建和运行，在运行和调试应用/元服务时可以保持良好的流畅性和稳定性，但是需要耗费一定的计算机资源，具体的运行环境要求如下。

Windows运行环境：

|类别|最低要求|推荐|
|:--|:--|:--|
|操作系统|Windows 10企业版、专业版或教育版及以上，且操作系统版本不低于10.0.18363|最新的64位Windows|
|CPU|- 具有二级地址转换 (SLAT) 的64位处理器<br>- CPU支持AES指令集<br>- CPU支持VM监视器模式扩展（Intel CPU的VT-c技术）<br>- 不支持在虚拟机系统中运行模拟器<br>- 不支持采用ARM CPU的Windows计算机<br>- 2017年以后CPU型号。|- 最新的Intel Core i5、i7、i9系列CPU<br>- 最新的AMD Ryzen 5、6、7、9系列CPU<br>- CPU后缀为H/HK/HX的笔记本电脑或后缀为S/F/K的台式机<br><br>由于性能不足，不推荐使用 Intel® Core™ N 系列和 U 系列处理器|
|RAM|16GB|32GB及以上|
|磁盘空间|16GB|32GB及以上|
|屏幕|屏幕分辨率1280*800像素以上|屏幕分辨率1920*1080像素以上|
|GPU|支持OpenGL版本4.1<br><br>从DevEco Studio 6.0.0 Release版本开始，AMD的GPU显示驱动要求不低于24.1.1版本|支持OpenGL版本4.1及以上<br><br>AMD的GPU显示驱动版本24.1.1及以上|

Mac运行环境：

|类别|最低要求|推荐|
|:--|:--|:--|
|操作系统|macOS系统为12.5及以上版本|最新的64位macOS|
|CPU|- 不支持在虚拟机系统中运行模拟器<br>- Apple Silicon芯片|最新的Apple Silicon|
|RAM|8GB|16GB及以上|
|磁盘空间|16GB|32GB及以上|
|屏幕|屏幕分辨率1280*800像素以上|屏幕分辨率1920*1080像素以上|
|GPU|支持OpenGL版本4.1|支持OpenGL版本4.1及以上|

[概述](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-emulator-overview "概述")

[设备支持类型](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-emulator-devicetype "设备支持类型")
# 设备支持类型

更新时间: 2025-12-16 15:58

模拟器在不同系统上支持的设备类型见下表。

|系统类型|设备类型|备注|
|:--|:--|:--|
|Windows(X86)<br><br>macOS(ARM)|Phone（包括折叠屏）|仅支持在中国境内（香港特别行政区、澳门特别行政区、中国台湾除外）使用。|
|Tablet|仅支持在中国境内（香港特别行政区、澳门特别行政区、中国台湾除外）使用。|
|PC/2in1（包括折叠屏）|从DevEco Studio 5.0.13.200版本开始，支持在中国境内（香港特别行政区、澳门特别行政区、中国台湾除外）使用PC/2in1设备。<br><br>从DevEco Studio 6.0.0.456版本开始，支持在中国境内（香港特别行政区、澳门特别行政区、中国台湾除外）使用折叠屏PC/2in1设备。|
|Wearable|从DevEco Studio 6.0.0.828版本开始，支持在中国境内（香港特别行政区、澳门特别行政区、中国台湾除外）使用。<br><br>从DevEco Studio 6.0.1.249版本开始，支持在所有国家/地区使用。|
|TV|从DevEco Studio 5.1.1.840版本开始，支持在中国境内（香港特别行政区、澳门特别行政区、中国台湾除外）使用。|

说明

使用x86模拟器时，C++工程及三方库需要编译出x86_64版本的so，请在工程级或模块级build-profile.json5的externalNativeOptions/abiFilters的值中增加"x86_64"，具体编译配置请参见[externalNativeOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-cpp#section0721057575)。

[使用环境](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-emulator-requirements "使用环境")

[模拟器与真机的差异](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-emulator-specification "模拟器与真机的差异")
# 模拟器与真机的差异

更新时间: 2025-12-16 15:58

模拟器是开发和调试HarmonyOS应用/元服务的便捷工具，例如不需要配置服务器域名即可开发和调试元服务，在大多数情况下，模拟器上推包调试不需要签名，但部分Kit仍需签名后才能正常运行，具体要求请参考Kit的开发指南。

由于模拟器和真机在硬件和能力上存在差异，部分功能场景仍需在真机上进行开发。您可以通过阅读本文档来决定哪些功能在模拟器中测试，哪些功能在真机上测试。

## 通用差异

模拟器是运行在Mac或Windows电脑上的虚拟机应用，会使用电脑的硬件资源，包括CPU、内存和网络连接等。这些资源在容量和速度上可能与真机存在显著差异。因此，模拟器不适合用于测试应用/元服务的性能（如数据处理、图形渲染、网络速度）、资源占用（如内存、CPU、功耗），模拟器的性能测试结果仅能用于评估应用功能的相对差异。如需获取真实场景下的用户体验数据，建议在真机上进行测试。

## 显示效果差异

- 模拟器使用电脑的显示器，与真机屏幕不同，可能会导致文本和图像在模拟器上出现边缘锯齿。放大模拟器窗口比例可以使文字和图像更清晰。
- 电脑屏幕的色域范围可能与移动设备不同，从而导致颜色显示不准确。
- 模拟器不支持屏幕亮度调节。

## 图形接口差异

- 不支持OpenGL ES 3.1、3.2接口
- 不支持Vulkan接口

## Kit能力差异

当前部分Kit不支持在模拟器上使用，具体参考以下说明。部分Kit能力有设备类型和使用地区限制，具体请参考对应Kit指南。

如遇到因Kit能力不支持导致的应用闪退问题，可以使用[动态引入Kit](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-dynamic-import#%E5%8A%A8%E6%80%81import%E5%AE%9E%E7%8E%B0%E6%96%B9%E6%A1%88%E4%BB%8B%E7%BB%8D)的方式规避此异常问题。

Kit不支持导致的报错信息如：

1. LastFatalMessage:[default] [LoadJSPandaFile:00] resolveBufferCallback get hsp buffer failed，hsp path:/data/storage/el1/bundle/com.huawei.hmos.{KitName}.kit

### 应用框架

以下Kit和场景暂不支持模拟器。

- Ability Kit（程序框架服务）：不支持拉起垂类应用面板，不支持使用App Linking实现应用间跳转，不支持以免安装方式拉起元服务。
- Accessibility Kit（无障碍服务）：不支持屏幕朗读以外的其他功能。
- Background Tasks Kit（后台任务开发服务）：模拟器短时任务不会被挂起。
- Data Augmentation Kit（数据增强服务）
- UI Design Kit（UI设计套件）：不支持侧边栏样式设置，不支持侧边栏菜单样式，不支持底部页签设置图标出血样式，不支持即时操作设置，不支持核心操作栏设置，不支持列表设置，不支持应用加载自定义Symbol，不支持视效。

### 安全

以下Kit和场景暂不支持模拟器。

- Data Protection Kit（数据保护服务）
- Device Security Kit（设备安全服务）
- Enterprise Data Guard Kit（企业数据保护服务）
- Online Authentication Kit（在线认证服务）
- 不支持安全GPS、人脸识别、设备证书等。

### 网络

以下Kit暂不支持模拟器。

- Distributed Service Kit（分布式管理服务）
- NearLink Kit（星闪服务）
- Network Boost Kit（网络加速服务）
- Service Collaboration Kit（协同服务）
- Telephony Kit（蜂窝通信服务）

### 基础功能

- Input Kit（多模输入服务）：不支持对鼠标光标的样式修改等操作。
- 不支持MDM Kit（企业设备管理服务）

### 硬件

以下Kit暂不支持模拟器。

- Car Kit（车服务）
- Driver Development Kit（驱动开发服务）
- Mechanic Kit（机械体设备控制器）
- Multimodal Awareness Kit（多模态融合感知服务）
- Pen Kit（手写笔服务）
- Sensor Service Kit（传感器服务）：支持部分传感器，参见[虚拟传感器](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-emulator-more-features#section830415558395)。
- Wear Engine Kit（穿戴服务）

### 媒体

以下Kit和场景暂不支持模拟器。

- Camera Kit（相机服务）：不支持预览、拍照以外的其他功能。
- DRM Kit（数字版权保护服务）
- Scan Kit（统一扫码服务）：不支持码图生成，不支持识别图像数据。
- 不支持heif格式的图片
- 视频播放：仅支持h264文件格式、RGBA像素格式的视频文件。
- 不支持视频录制/转码/处理、屏幕录像。

### 图形

以下Kit暂不支持模拟器。

- AR Engine（AR引擎服务）
- ArkGraphics 3D（方舟3D图形）
- Graphics Accelerate Kit（图形加速服务）
- Spatial Recon Kit（空间建模服务）
- XEngine Kit（GPU加速引擎服务）

### 应用服务

以下Kit和场景暂不支持模拟器。

- AppGallery Kit（应用市场服务）：不支持数字商品服务、应用市场推荐、生态查询服务、应用市场更新功能、应用评论服务、图标管理服务，不支持端云交互。
- App Linking Kit（应用链接服务）
- Call Service Kit（通话服务）
- Cloud Foundation Kit（云开发服务）：不支持预加载。更多关于如何在模拟器上调试Cloud Foundation Kit，请参考[使用模拟器调试](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-emulator)。
- Enterprise Space Kit（企业数字空间服务）
- Game Service Kit（游戏服务）
- Health Service Kit（运动健康服务）
- IAP Kit（应用内支付服务）
- Location Kit（位置服务）：不支持地理围栏。
- Map Kit（地图服务）：不支持3D地图、地图截图。
- Payment Kit（华为支付服务）
- PDF Kit（PDF服务）：X86版本不支持。
- Preview Kit（文件预览服务）：不支持.pdf/.pptx/.xlsx/.docx文件格式预览。
- Push Kit（推送服务）：不支持推送授权订阅消息、推送通知扩展消息、推送实况窗消息、推送应用内通话消息。
- Reader Kit（阅读服务）
- Scenario Fusion Kit（融合场景服务）：具体请参考[模拟器支持范围](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/scenario-fusion-introduction#section1901742183715)。
- Share Kit（分享服务）：不支持跨端分享、基于意图框架的分享。
- Wallet Kit（钱包服务）
- Weather Service Kit（天气服务）

### AI

以下Kit和场景暂不支持模拟器。

- CANN Kit（CANN 服务）
- Core Vision Kit（基础视觉服务）
- Agent Framework Kit（智能体框架服务）
- Intents Kit（意图框架服务）
- MindSpore Lite Kit（昇思推理框架服务）：不支持图像分类之外的其他功能。
- Natural Language Kit（自然语言理解服务）
- Neural Network Runtime Kit（Neural Network运行时服务）
- Speech Kit（场景化语音服务）
- Vision Kit（场景化视觉服务）

## 其他差异

**表1**
|模拟器和真机的其他重要差异|影响场景|
|:--|:--|
|SIM卡|不支持拨打电话、发送短信|
|USB|不支持连接、数据传输|
|蓝牙|不支持蓝牙设备扫描、连接、数据传输|
|星闪|不支持星闪设备扫描、连接、数据传输、分布式能力|
|NFC|不支持NFC卡片读写、刷卡|
|TEE（Trusted Execution Environment，可信执行环境）|部分安全相关Kit暂不支持，详情参考[Kit能力差异](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-emulator-specification#section147193483010)|
|NPU|部分AI相关Kit暂不支持，详情参考[Kit能力差异](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-emulator-specification#section1155211435325)|
|生物识别|不支持指纹、人脸认证|
|摄像头/麦克风|依赖电脑设备，不支持多摄像头切换（广角/长焦）、闪光灯、降噪算法等|
|电源|模拟电源，不支持亮灭屏、温控、快充等场景|

## Kit支持情况变更说明

### DevEco Studio 6.0.1 Release

- 支持Ringtone Kit（铃声服务）

### DevEco Studio 6.0.0 Beta5

以下Kit支持在模拟器上使用：

- Ads Kit（广告服务）
- AppGallery Kit（应用市场服务）：支持产品特性按需分发、应用归因服务、隐私管理中不涉及端云交互的接口。
- Cloud Foundation Kit（云开发服务）：支持云函数、云数据库、云存储。具体调试方式请参考[使用模拟器调试](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-emulator)。

### DevEco Studio 6.0.0 Beta3

- 支持Screen Time Guard Kit（屏幕时间守护服务）

### DevEco Studio 6.0.0 Beta2

- Accessibility Kit（无障碍服务）：支持屏幕朗读。

### DevEco Studio 6.0.0 Beta1

以下Kit支持在模拟器上使用：

- Core Speech Kit（基础语音服务）
- Scan Kit（统一扫码服务）：支持使用电脑摄像头扫码。

### DevEco Studio 5.1.1 Beta1

- NDK：X86版本支持JSVM。

### DevEco Studio 5.1.0 Release

以下Kit支持在模拟器上使用：

- PDF Kit（PDF服务）：支持在ARM版本上使用。
- Map Kit（地图服务）：支持除3D地图和地图截图以外的其他功能。
- Camera Kit（相机服务）：支持预览、拍照。
- Share Kit（分享服务）：支持除了跨端分享、基于意图框架的分享以外的其他功能。

[设备支持类型](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-emulator-devicetype "设备支持类型")

[管理模拟器](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-emulator-management "管理模拟器")
