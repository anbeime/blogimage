# 外部平台导入

更新时间: 2025-12-16 15:02

外部平台导入创建步骤：

1，【注册方式】选择【外部平台导入】，【选择平台】选择【魔搭平台】。

2，填写API Key，可以点击【访问令牌】进行获取。

3，点击【开始同步】按钮。

4，插件列表同步完成后点击创建。

点击创建后会自动逐步完成插件创建、工具拉取、插件发布（仅支持发布到智能体渠道）。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216150258.04225435145419963961818273998586:50001231000000:2800:2747902031DA82E4E869669291BDD66ECA52AF04953B0B4E398E30DF19616452.png "点击放大")

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216150258.64811588098615305021411031715734:50001231000000:2800:C59752DE21E19E503F5B8B054129BB054770D1837E0C5B52F1966E39D3417630.png "点击放大")

**FAQ**

问题1、外平台导入方式注册MCP插件，输入访问令牌同步完成后，未同步到插件信息？

答：仅支持导入在魔搭平台自部署的**长期有效**的MCP插件，请先在该访问令牌对应魔搭账号下部署符合要求的插件。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216150258.26943688953105662651562855503953:50001231000000:2800:DD607BAB7CB7214FA53513E087BCBA5C63834264F1F47384CB9C15DC5FB35121.png "点击放大")

问题2、外平台导入方式注册MCP插件创建后，同步回来的插件未全部创建？

答：已同步并创建到插件列表中的MCP插件，再次导入时虽然会在同步的插件列表中展示，但点击创建后自动过滤掉已创建插件（根据MCP服务配置中的配置地址判断插件是否重复）； 如有需要，可下架并删除重复插件后重新同步。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216150258.53474547966605234265862610434308:50001231000000:2800:0FD6F8CA0C026E80E79481438932AFCA42E66578C61477E78EFB2FD31E84A709.png "点击放大")# 发布插件

更新时间: 2025-12-16 15:02

点击【发布】-【提交审核】，勾选待发布渠道点击【确认】后即可发布，MCP插件有三种发布渠道：

智能体：发布到智能体，可以在创建智能体和工作流时，在工作空间中选择此插件；发布后即可上架成功，无需人工审核。

小艺对话：发布到小艺对话，可以在技能服务中使用此插件；发布后需联系华为侧人员进行审核。

插件市场：选择发布到插件市场后，经过审核后可以将此插件开放到插件市场中被其他开发者发现和使用；发布后需联系华为侧人员进行审核公开。
# 智能体场景开发案例

更新时间: 2025-12-17 20:59

## 简介

智能体作为一个由用户通过角色指令精心设计的具有明确身份和目标的虚拟实体，其核心价值在于能够像人一样使用自然语言对话，理解用户需求，运用预设的知识、能力和逻辑进行思考与推理，并主动生成恰当的响应或执行相应操作（任务完成、信息提供、服务实施），以满足用户需求或实现预设目标。通过用户友好的交互界面、简便的接入方式及广泛的应用场景，满足消费者在日常生活中对智能助手、信息检索、推荐等功能的需求。同时，智能体还可服务于多个垂直行业和业务场景，有效拓展市场覆盖面与增强用户粘性，用户亦可直接与智能体独立对话，以获得场景化的连贯知识与服务。

[小艺开放平台](https://developer.huawei.com/consumer/cn/hag/hagindex.html#/)是小艺结合了意图框架与华为AI大模型能力面向开发者的能力开放平台。基于该平台的[小艺智能体平台](https://developer.huawei.com/consumer/cn/hag/hagindex.html?isInFrame=true&lang=zh_CN#/agentHome/square)允许开发者构建智能体，为用户提供大模型时代的智能新体验，同时实现业务增长。开发者可以基于小艺智能体平台开发专属智能体。

本文主要介绍如何基于[智能问答场景](https://developer.huawei.com/consumer/cn/doc/best-practices/bpta-agent#section2907103562520)和[音频播放场景](https://developer.huawei.com/consumer/cn/doc/best-practices/bpta-agent#section15781420152616)，在小艺智能体平台上快速搭建智能体并适配相应需求场景。

智能体从创建到上架主要包含以下五个步骤：

1. [智能体创建](https://developer.huawei.com/consumer/cn/doc/best-practices/bpta-agent#section524618504324)：开发者需在[小艺开放平台](https://developer.huawei.com/consumer/cn/hag/hagindex.html#/)完成企业/个人账号注册，获取HarmonyOS生态的开发权限，基于智能体平台快速初始化项目，自定义开发专属智能体。
2. [模式选择](https://developer.huawei.com/consumer/cn/doc/best-practices/bpta-agent#section59501510153311)：不同模式的智能体，适配的场景也有所不同，开发者可按照业务需求选择合适模式的智能体，开发构建智能场景的智能体。
3. [智能体编排](https://developer.huawei.com/consumer/cn/doc/best-practices/bpta-agent#section109683238339)：可视化流程的编排框架，自定义智能体能力点，优化完善智能体场景。
4. [功能验证](https://developer.huawei.com/consumer/cn/doc/best-practices/bpta-agent#section864165923316)：实时性、可视化、场景化的验证模式，可实时交互验证，或真实场景验证。
5. [上架/升级](https://developer.huawei.com/consumer/cn/doc/best-practices/bpta-agent#section74742275511)：通过[上架审核规范](https://developer.huawei.com/consumer/cn/doc/service/audit-specifications-0000002469548113)的审核上架，保障对外发布信息的安全与合规，进一步提升用户体验。

## 开发步骤

### 智能体创建

登录[小艺开放平台](https://developer.huawei.com/consumer/cn/hag/hagindex.html#/)，点击【立即体验】按钮，进入小艺智能体平台页面。点击左上角【+创建智能体】按钮，即可进入智能体创建流程。可自行设定智能体的相关信息，包括它的名称、头像、智能体描述、智能体分类和运行设备等信息。具体内容可参考开发者指导文档[快速创建智能体](https://developer.huawei.com/consumer/cn/doc/service/quick-start-0000002469548009)。

准备条件：真机调试及端插件开发需在HarmonyOS 5.1.0 Release及以上版本的设备上进行。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251217205908.25694620529753597799723277494455:50001231000000:2800:123D3BE87F2D083714A4D4AF988FECCF7D22642CC28782B13823FD0611216550.png "点击放大")

### 模式选择

智能体分为LLM模式、工作流模式和A2A模式三种，对于不同的场景，适配的智能体模式也会有所不同。

LLM模式智能体主要依靠大语言模型的能力，如语言理解、生成、推理等，来处理任务和回答问题。它通常直接根据用户输入，利用大语言模型内部的知识和算法生成响应。

工作流模式智能体是通过预定义的代码路径，协调智能体与工具的交互。它将任务按照特定顺序或规则分解为多个步骤，每个步骤有明确的输入和输出，智能体按照预设流程依次执行，以实现任务目标。这种模式强调可预测性和一致性，适合任务明确、流程固定的场景。

A2A模式是一种三方智能体接入小艺开放平台的高效编排方式。开发者可通过该模式基于鸿蒙Agent通信协议快速、便捷地将成熟的第三方智能体对接至小艺开放平台，实现分发与调用，提升平台的场景覆盖能力。该模式适用于同时具备鸿蒙端应用与云侧智能体能力的企业开发者。

|模式|LLM模式（Agent）|工作流模式（Workflow）|A2A模式|
|:--|:--|:--|:--|
|核心逻辑|基于内部知识直接生成回答，由大模型决策进行工具调用|按预设流程分步执行（如数据查询→格式转换→结果整合）|通过标准化通信协议，实现鸿蒙生态中智能体跨设备协作与端云协同。|
|智能问答场景适用性|适合知识型、交互型问答（如常识咨询、客服答疑、教育辅导）|适合多步骤流程化任务（如报销申请审批、物流跟踪）|适合整合多源动态知识、融合多模态响应并跨服务生成连贯交互的场景（如医疗咨询）|
|音频播放场景适用性|适合处理用户语音指令（如 “播放周杰伦的歌”），需调用外部工具处理音频解码、渲染等底层操作|适合音频播放的全链路处理（从资源获取到设备输出）|通过协议扩展第三方播控能力、设备间播放状态同步及低时延优化策略，实现无缝跨端音频流转与场景化音质适配。|

不同编排模式的智能体，能力拓展部分的功能点也会有所区别。各编排模式的区别可参考开发者指导文档[智能体分类](https://developer.huawei.com/consumer/cn/doc/service/differences-in-arrangement-modes-0000002471344117)，开发者可根据不同模式的区别，考虑使用场景应该适配何种编排模式的智能体，选择对应的编排模式，并设定智能体相关信息，便可创建对应模式的智能体。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251217205908.12920947950049829995696334704728:50001231000000:2800:AA23758106406144866BC457D91A7EE30E745BAA84B6BFFD989475696306D268.png "点击放大")

### 智能体编排

智能体创建后，进入智能体的编排页面，开始智能体的编排，给智能体添加各种能力，优化完善智能体。其中，开场对话可以让用户快速了解你的智能体功能或场景设定故事背景，预置问题可以让用户通过点击快速体验智能体的能力，角色指令（prompt）直接决定你所创造的智能体的效果。更多能力点，开发者可参考[编排-能力拓展](https://developer.huawei.com/consumer/cn/doc/service/ability-expansion-function-introduction-0000002437625858)，自定义智能体的背景、能力等。

以下为LLM模式和工作流模式的编排页面：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251217205908.42016500040556942948648755663423:50001231000000:2800:28309766036F84E5915E8743E0F0690BBCBC0038D4D67E65A9B204A086F96976.png "点击放大")

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251217205908.11028228686026942457668359371252:50001231000000:2800:BD5E01BBE49AF55086F3EBDC44B72FB8228CCEED427F8A1AF3C7EE89974F601D.png "点击放大")

### 功能验证

在搭建完成智能体后，开发者可以在调试与预览区域与智能体进行对话，测试该智能体功能是否与预期相同，并根据智能体执行过程及响应信息对智能体配置进行优化与调整，具体调试过程可参考开发者指导文档[调试与预览](https://developer.huawei.com/consumer/cn/doc/service/real-machine-testing-0000002471344145)，包括真机测试与调试两种功能验证方式。

### 上架/升级

功能测试完成后，点击【保存】【上架】即可将智能体提交到上架审核阶段，具体流程可参考开发者指导文档[上/下架、升级流程介绍](https://developer.huawei.com/consumer/cn/doc/service/process-introduction-0000002509696971)。为了方便开发者的智能体能够顺利通过审核，可参考[上架审核规范](https://developer.huawei.com/consumer/cn/doc/service/audit-specifications-0000002469548113)排查检视自开发的智能体。待通过审核上架后，即可在小艺平台使用完整的智能体。

## 智能问答场景

### 场景描述

智能问答系统凭借其高效、便捷的交互特性，已广泛应用于多个领域。依托知识库，智能问答能够精准匹配用户需求，提供准确且专业的回答。例如，医疗场景中，用户描述 “咳嗽 + 发热”，系统结合症状库推荐科室并提示 “可能的流感风险”。智能问答的核心价值在于通过自然语言交互解决信息获取效率问题，它通常直接根据用户输入，利用开发者上架的知识库或大语言模型内部的知识和算法生成响应，实现更精准、个性化的服务。具有准确与规范的答案（所有回答基于企业预设的知识库或官方数据，避免人工客服因理解偏差或记忆错误导致答案不一致）和服务质量的可控性（企业可随时更新知识库，保证答案同步最新政策，如税法调整、产品更新等）。

### 场景开发

**模式选择**

智能问答场景主要为简单的语言交互（如闲聊、知识查询），无需外部工具调用，因此优先选择LLM模式，可基于内部知识直接生成回答。LLM 模式主要有自然语言处理能力、知识整合效率、交互体验等方面的核心优势，凭借这些原生优势，成为智能问答的主流选择，尤其适合知识型、交互型、跨领域的问答场景。

|模式|LLM 模式|工作流模式|
|:--|:--|:--|
|核心逻辑|基于内部知识直接生成回答，由大模型决策进行工具调用|按预设流程分步执行（如数据查询→格式转换→结果整合）|
|智能问答场景适用性|适合知识型、交互型问答（如常识咨询、客服答疑、教育辅导）|适合多步骤流程化任务（如报销申请审批、物流跟踪）|
|智能问答场景局限性|依赖训练数据时效性（需定期更新知识库）；复杂计算任务需结合工具|流程固定，难以应对灵活的问答需求；需人工配置大量流程节点|

问答智能体主要基于开发者提供的知识库，智能整合内部知识，生成所需回答。因此，除了需要选择LLM模式的智能体外，还需要自定义所需场景的知识库。

**知识库创建上架**

1. 创建知识库：在小艺开放平台工作空间的知识库界面点击【新建知识库】，进入新建知识库页面，填写知识库信息后点击【新建】按钮，新建知识库成功。
2. 配置知识库：从知识库列表点击新建的知识库名称进入知识列表页面，点击【新建知识】，导入相应知识类型的文件，并填写相关信息后，点击【确定】，知识添加成功。具体流程可参考开发者指导文档[创建知识库](https://developer.huawei.com/consumer/cn/doc/service/create-a-knowledge-base-0000002471344153)。
3. 上架知识库：点击相应知识的【上架】按钮，等待知识库审核上架即可。文档类型的知识要等待数据校验完成后才能上架。

**LLM模式智能体创建**

1. 创建智能体：参考上述[开发步骤](https://developer.huawei.com/consumer/cn/doc/best-practices/bpta-agent#section369116225258)，创建一个LLM模式的智能体。
2. 编排智能体：进入智能体编排页面，编辑智能体的开场对话，并添加上架完成的知识库，开发者也可按照实际业务需求自行编排。

**功能验证**

可调试测试或真机测试，真机测试需添加白名单，设置白名单手机或账号，发布至手机智能体，方可真机测试。

1. 调试测试：调试与预览界面可以进行交互测试，预览实际交互场景，也可点击右上角调试按钮，进入调试详情页，查看详细的调测信息。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251217205908.63029490658106983090126244677093:50001231000000:2800:963AD9CB2E89CDC440A939EE077452C6C72FC56EFC51697F521925A97D1484CE.png "点击放大")
    
2. 真机测试：点击调试与预览页面右上角的真机测试，可发布真机测试。真机测试前需配置白名单，开发者（团队账户需管理员权限）可通过新增组来管理真机调试用户，每个团队最多可创建100个用户组，每个用户组最多可添加100个用户。 开发者在服务发布至真机调试后，处于真机调试用户白名单中的用户可以访问到该开发测试服务，详见开发者指导文档[真机测试](https://developer.huawei.com/consumer/cn/doc/service/list-of-user-groups-for-real-machine-testing-0000002471264273)。

**上架升级**

功能测试完成后，点击【保存】【上架】即可将智能体提交到上架审核阶段，具体流程可参考开发者指导文档[上/下架、升级流程介绍](https://developer.huawei.com/consumer/cn/doc/service/process-introduction-0000002509696971)。

## 音频播放场景

### 场景描述

音频播放的应用场景广泛，可根据使用场景、设备类型及功能需求分为多种适用类型，不同场景下的音频播放均围绕：实时性、音质、设备适配、离线能力、隐私安全等方面展开。

### 场景开发

**模式选择**

音频播放场景APP一般包括跳转播放页、播放音频、获取歌曲名称等功能，对于涉及到存在音频播放场景的项目，想要通过语音、文字等操作智能化实现上述功能，则需使用端插件和工作流模式的智能体架构。该架构不仅解决了音频播放场景智能化交互（语音 / 文字指令），还提供了高效的本地执行载体，形成本地化处理与流程协同的高效架构。结合工作流模式，设置节点控制（如音频播放、页面跳转、信息获取），端插件可本地协调多模块交互，运行在设备本地的功能模块。

|模式|工作流模式（Workflow）|LLM 模式|
|:--|:--|:--|
|核心逻辑|按预设流程分步执行（如数据查询→格式转换→结果整合）|基于内部知识直接生成回答，由大模型决策进行工具调用|
|音频播放场景适用性|适合音频播放的全链路处理（从资源获取到设备输出）|适合处理用户语音指令（如 “播放周杰伦的歌”），但无法直接处理音频解码、渲染等底层操作|
|音频播放场景局限性|灵活性较低，需人工配置所有流程节点|不具备音频编解码、设备驱动等底层能力，需依赖外部工具支持|

音频播放场景，主要基于音频编解码等功能，需要外部工具的支持，可在端插件实现音频播放功能。同时，音频播放场景一般涉及页面跳转、音频播放、获取信息等功能，通过设计流程节点，可搭建业务所需的整体流程。因此，除了需要选择工作流模式的智能体外，还需要实现适配流程节点的端插件。

**端插件创建上架**

1. 创建端插件：在小艺开放平台工作空间的插件界面点击【新建插件】，选择端插件，填写对应的APP包名和名称。点击【保存】后，创建端插件成功，进入端插件的编辑页面。
2. 配置端插件：点击【新建工具】，在工具信息页填写工具名称后点击【创建】，可新增一条工具。点击【添加版本】，按页面提示填写参数后，点击【创建】，进入工具信息页，按需求可添加输入输出参数，点击【保存】，端插件的一个工具配置完成。按照上述操作方法，可添加多条工具，开发者可按需配置。具体配置方式也可参考开发者指导文档[创建端插件](https://developer.huawei.com/consumer/cn/doc/service/create-side-plug-in-0000002437625930)。
    
    本场景涉及三个功能，包括获取歌曲名称、跳转播放页、播放音频，因此配置了三个对应功能的工具。具体配置信息如下图所示：
    
    |获取信息|跳转页面|播放音频|
    |:--|:--|:--|
    |![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251217205908.22222441379764847866765529926155:50001231000000:2800:78DE5E0102D53362328F2FFEC9A8E6CFB33211E30C01E9005283E19B360FB0E6.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251217205909.18926770485521873528589508216850:50001231000000:2800:65BDFA1FC71221575AD364DBA79511F6121323B32B659C749152FA0BA31D7F11.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251217205909.95834629763006823917578424613783:50001231000000:2800:69485B485649B329AC89C5B4DD09F762BCEF714FD6E4302C350A10BE98A7E748.png)|
    
3. 上架：配置完端插件信息后，点击【上架】按钮，填写版本信息后，点击【确认】，端插件进入上架审核中，待审核上架成功后，即可在其他场景使用已上架的端插件。

**端插件开发**

端插件作为设备本地运行的功能模块，提供能力的服务在HarmonyOS设备侧，需要在端侧进行代码实现。对于音频播放场景的实现有以下几步：

1. 在端侧应用工程根目录下新建entry/src/main/resources/base/profile/insight_intent.json文件，用来绑定上一步实现的端插件中对应的工具。
    
    intentName对应工具名称，intentVersion对应工具版本号，srcEntry为基于意图框架[InsightIntentExecutor](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-app-ability-insightintentexecutor#insightintentexecutor)类方法的业务逻辑处理文件。
    
    1. {
    2.   "insightIntents": [
    3.     {
    4.       "domain": "",
    5.       "intentName": "PlayHiddenAudio",
    6.       "intentVersion": "1.0.0",
    7.       "srcEntry": "./ets/entryability/InsightIntentExecutorImpl.ets",
    8.       "uiAbility": {
    9.         "ability": "EntryAbility",
    10.         "executeMode": [
    11.           "background"
    12.         ]
    13.       }
    14.     },
    15.     {
    16.       "domain": "",
    17.       "intentName": "GetAudioName",
    18.       "intentVersion": "1.0.0",
    19.       "srcEntry": "./ets/entryability/InsightIntentExecutorImpl.ets",
    20.       "uiAbility": {
    21.         "ability": "EntryAbility",
    22.         "executeMode": [
    23.           "background"
    24.         ]
    25.       }
    26.     },
    27.     {
    28.       "domain": "",
    29.       "intentName": "OpenSecondPage",
    30.       "intentVersion": "1.0.0",
    31.       "srcEntry": "./ets/entryability/InsightIntentExecutorImpl.ets",
    32.       "uiAbility": {
    33.         "ability": "EntryAbility",
    34.         "executeMode": [
    35.           "background",
    36.           "foreground"
    37.         ]
    38.       }
    39.     }
    40.   ]
    41. }
    
2. 绑定的端插件被调用时的业务逻辑处理。
    
    1. import { insightIntent, InsightIntentExecutor } from '@kit.AbilityKit';
    2. import { BusinessError } from '@kit.BasicServicesKit';
    3. import { window } from '@kit.ArkUI';
    4. import AudioPlayHandler from './intentHandlers/AudioPlayHandler';
    5. import TextGetHandler from './intentHandlers/TextGetHandler';
    6. import PageNavigateHandler from './intentHandlers/PageNavigateHandler';
    7. import { hilog } from '@kit.PerformanceAnalysisKit';
    
    8. export default class InsightIntentExecutorImpl extends InsightIntentExecutor {
    9.   // Instruction implementation class.
    10.   private audioHandler = new AudioPlayHandler();
    11.   private textHandler = new TextGetHandler();
    12.   private pageHandler = new PageNavigateHandler();
    
    13.   // Intention execution method for backend execution.
    14.   async onExecuteInUIAbilityBackgroundMode(
    15.     intentName: string,
    16.     params: Record<string, object>
    17.   ): Promise<insightIntent.ExecuteResult> {
    
    18.     try {
    19.       switch (intentName) {
    20.         // Play audio intention.
    21.         case 'PlayHiddenAudio':
    22.           const stringParam: Record<string, string> = this.convertToRecord(params);
    23.           return this.audioHandler.execute(stringParam);
    
    24.         // Obtain audio name intent.
    25.         case 'GetAudioName':
    26.           return this.textHandler.execute();
    
    27.         default:
    28.           return {
    29.             code: -1,
    30.             result: {
    31.               'status': 'failed',
    32.               'message': `not valid intent name, ${intentName}`
    33.             }
    34.           };
    35.       }
    36.     } catch (error) {
    37.       return {
    38.         code: -2,
    39.         result: {
    40.           'status': 'failed',
    41.           'message': `Intent execution failed: ${(error as BusinessError).message}`
    42.         }
    43.       };
    44.     }
    45.   }
    
    46.   private convertToRecord(origin: Record<string, object>): Record<string, string> {
    47.     const result: Record<string, string> = {};
    48.     Object.keys(origin).forEach(key => {
    49.       result[key] = String(origin[key]);
    50.     });
    
    51.     return result;
    52.   }
    
    53.   // Execution method of backend execution intention.
    54.   async onExecuteInUIAbilityForegroundMode(name: string, param: Record<string, Object>, pageLoader: window.WindowStage):
    55.     Promise<insightIntent.ExecuteResult> {
    56.     switch (name) {
    57.       // Open the second page intention.
    58.       case 'OpenSecondPage':
    59.         return this.pageHandler.execute();
    60.       default:
    61.         pageLoader.loadContent('pages/MainPage')
    62.           .catch((error: BusinessError) => {
    63.             hilog.error(0x000, 'testTag', `loadContent failed. code=${error.code}, message=${error.message}`);
    64.           })
    65.         break;
    66.     }
    67.     return Promise.resolve({
    68.       code: -1,
    69.       result: {
    70.         message: 'unknown intent'
    71.       }
    72.     } as insightIntent.ExecuteResult)
    73.   }
    74. }
    
    [InsightIntentExecutorImpl.ets](https://gitee.com/harmonyos_samples/BestPracticeSnippets/blob/master/XiaoyiAgentDemo/entry/src/main/ets/entryability/InsightIntentExecutorImpl.ets#L17-L99)
    
3. 功能开发。
    - 实现获取歌曲名称的功能，并返回读取结果。
        
        1. import { insightIntent } from '@kit.AbilityKit';
        2. import { BusinessError } from '@kit.BasicServicesKit';
        3. import { MediaService } from '../../utils/audioplayer/MediaService';
        
        4. export default class TextGetHandler {
        5.   async execute(): Promise<insightIntent.ExecuteResult> {
        6.     try {
        7.       // Execute the method of obtaining the name of the played audio.
        8.       const audioName: string = MediaService.getInstance().getAudioFileName();
        
        9.       // Return result.
        10.       return {
        11.         code: 0,
        12.         result: {
        13.           status:'success',
        14.           audioName: audioName,
        15.           message: 'get audio name success'
        16.         }
        17.       };
        18.     } catch (error) {
        19.       throw new Error(`get audio name failed: ${(error as BusinessError).message}`);
        20.     }
        21.   }
        22. }
        
        [TextGetHandler.ets](https://gitee.com/harmonyos_samples/BestPracticeSnippets/blob/master/XiaoyiAgentDemo/entry/src/main/ets/entryability/intentHandlers/TextGetHandler.ets#L17-L40)
        
    - 使用[Deep Linking](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/deep-linking-startup#%E6%8B%89%E8%B5%B7%E6%96%B9%E5%BA%94%E7%94%A8%E5%AE%9E%E7%8E%B0%E5%BA%94%E7%94%A8%E8%B7%B3%E8%BD%AC)实现跳转播放页的功能。
        
        配置module.json5文件中的[skills标签](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#skills%E6%A0%87%E7%AD%BE)，标识跳转场景。
        
        1. "skills": [
        2.   {
        3.     "entities": ["entity.system.browsable"],
        4.     "actions": [
        5.       "ohos.want.action.viewData"
        6.     ],
        7.     "uris": [
        8.       {
        9.         "scheme": "demo",
        10.         "host": "aiagentdemo.com",
        11.         "path": "SecondPage"
        12.       }
        13.     ]
        14.   }
        15. ]
        
        [module.json5](https://gitee.com/harmonyos_samples/BestPracticeSnippets/blob/master/XiaoyiAgentDemo/entry/src/main/module.json5#L25-L39)
        
        在EntryAbility.ets文件中的onNewWant()生命周期回调中，获取、解析拉起方传入的应用链接，开发者可自定义后续的业务处理。
        
        16. onNewWant(want: Want, launchParam: AbilityConstant.LaunchParam): void {
        17.   hilog.info(DOMAIN, 'testTag', 'Received URI:', want.uri);
        18.   const uri = want.uri;
        19.   let pathname = '';
        20.   if (uri) {
        21.     try {
        22.       const urlObj = url.URL.parseURL(uri);
        23.       pathname = urlObj.pathname;
        24.     } catch (error) {
        25.       let err = error as BusinessError;
        26.       hilog.error(0x000, 'testTag', `getUIContext failed. code=${err.code}, message=${err.message}`);
        27.     }
        28.     uiContext?.getRouter().pushUrl({ url: 'pages' + pathname })
        29.       .catch((error: BusinessError) => {
        30.         hilog.error(0x000, 'testTag', `pushUrl failed. code=${error.code}, message=${error.message}`);
        31.       })
        32.   }
        33. }
        
        [EntryAbility.ets](https://gitee.com/harmonyos_samples/BestPracticeSnippets/blob/master/XiaoyiAgentDemo/entry/src/main/ets/entryability/EntryAbility.ets#L75-L92)
        
        执行页面跳转并返回跳转结果。
        
        34. import { insightIntent } from '@kit.AbilityKit';
        35. import { BusinessError } from '@kit.BasicServicesKit';
        36. import { hilog } from '@kit.PerformanceAnalysisKit';
        
        37. export default class PageNavigateHandler {
        38.   async execute(): Promise<insightIntent.ExecuteResult> {
        39.     try {
        40.       // Execute page redirection.
        41.       let uiContext: UIContext | null | undefined = null;
        42.       uiContext = AppStorage.get('uiContext');
        43.       uiContext?.getRouter().pushUrl({ url: 'pages/SecondPage' })
        44.         .catch((err: BusinessError) => {
        45.         hilog.error(0x0000, 'testTag',`pushUrl failed, Code:${err.code}, message:${err.message}`);
        46.       })
        
        47.       return {
        48.         code: 0,
        49.         result: {
        50.           status: 'success',
        51.           message: 'Navigation successful',
        52.           targetPage: 'SecondPage'
        53.         }
        54.       };
        55.     } catch (error) {
        56.       throw new Error(`Page navigation failed: ${(error as BusinessError).message}`);
        57.     }
        58.   }
        59. }
        
        [PageNavigateHandler.ets](https://gitee.com/harmonyos_samples/BestPracticeSnippets/blob/master/XiaoyiAgentDemo/entry/src/main/ets/entryability/intentHandlers/PageNavigateHandler.ets#L17-L44)
        
    - 音频播放功能的实现，开发者可根据实际业务需求自定义实现该功能。
        
        1. import { insightIntent } from '@kit.AbilityKit';
        2. import { BusinessError } from '@kit.BasicServicesKit';
        3. import { MediaService } from '../../utils/audioplayer/MediaService';
        
        4. export default class AudioPlayHandler {
        
        5.   async execute(param: Record<string, string>): Promise<insightIntent.ExecuteResult> {
        6.     try {
        7.       // Analyze the parameters passed in by the plugin on the parsing end.
        8.       const rawAudioName = param.audioName;
        9.       const audioName = rawAudioName.toString();
        
        10.       // The method of playing audio can be customized by developers according to their actual business needs.
        11.       MediaService.getInstance().initAudioPlayer(audioName);
        
        12.       // Return the result to the end plugin.
        13.       return {
        14.         code: 0,
        15.         result: {
        16.           status: 'success',
        17.           message: `play audio ${audioName} started`,
        18.         }
        19.       };
        20.     } catch (error) {
        21.       throw new Error(`Audio play failed: ${(error as BusinessError).message}`);
        22.     }
        23.   }
        24. }
        
        [AudioPlayHandler.ets](https://gitee.com/harmonyos_samples/BestPracticeSnippets/blob/master/XiaoyiAgentDemo/entry/src/main/ets/entryability/intentHandlers/AudioPlayHandler.ets#L17-L44)
        

**工作流创建上架**

1. [创建工作流](https://developer.huawei.com/consumer/cn/doc/service/create-workflow-0000002471344157)：在小艺开放平台工作空间的工作流界面点击【新建工作流】，填写工作流对应信息后，点击【确定】，创建工作流成功并进入工作流编辑页面。
2. [编排工作流](https://developer.huawei.com/consumer/cn/doc/service/arrange-workflow-0000002471264285)：
    1. 创建工作流后，在画布中点击【添加节点】后，选择【插件】按钮，在工作空间中选择已上架的端插件点击【添加】，即可将所需插件添加至画布中。
    2. 获取歌曲名称、跳转播放页、播放音频三个功能场景为并列关系，可在画布中点击【添加节点】，添加【选择器】，点击添加好的选择器，在右侧的选择器编辑页面设定不同分支对应的条件，条件成立则下一步运行对应的分支（点击条件分支右侧的+号，可添加一条分支）。
        
        |创建选择器|选择器条件分支|
        |:--|:--|
        |![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251217205909.50893862953730247013563589176562:50001231000000:2800:81A1574320F0E89E8D8D9C52AEDB7D27F9449CDFD3F73E54DA52A4571F5C92F6.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251217205909.87409475087035414851677325413723:50001231000000:2800:D383BF286A557681304F4A8EE82BB9E3A6A64AAE692F55E1FF03A58B4B177AA0.png "点击放大")|
        
    3. 按照任务执行顺序连接对应节点
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251217205909.63136002932377686071760062079043:50001231000000:2800:A5CEBE6F2685472D6934395C9C96EF198BE36C3E1262D6098C38198FC878F6FD.png "点击放大")
        
3. 测试上架：点击【试运行】后，进入调试页面，可自行测试整体流程（无法在小艺开放平台调试端插件适配情况，只能测试工作流整体流程）。测试无误后，点击【上架】，进入上架审核阶段，待审核通过，即可在智能体中添加插件。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251217205909.84444551048366278972772310312014:50001231000000:2800:4A7A10A94466ECF2522356A8E16872CD4B2A2919FEC053E6CCD49EE910FDB5D2.png "点击放大")
    

**工作流模式智能体编排**

音频播放场景所需的端插件、工作流都已经开发完成，并成功上架成功后，接下来就是智能体的搭建过程了。

1. 创建智能体：可参考上述[开发步骤](https://developer.huawei.com/consumer/cn/doc/best-practices/bpta-agent#section369116225258)，创建一个工作流模式的智能体；
2. 编排智能体：进入智能体编排页面，编排智能体的开场对话，添加上架完成的工作流，开发者可按照实际业务需求自行搭建；

**功能验证**

1. 调试与测试：调试与预览界面可以进行交互测试，预览实际交互场景，也可点击右上角调试按钮，进入调试详情页，查看详细的调试信息。
    
    |调试与预览|调试详情|
    |:--|:--|
    |![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251217205909.16098699644518117606728631837453:50001231000000:2800:BB9D37DEB72DDE491DF43D15913611105457BC27F07E4237D6FED1FFA8283017.png "点击放大")|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251217205909.39812292094778864598782712400552:50001231000000:2800:A394D3694E1847694CAAD199B0743613E55D945F3A75401BC9BC441F51B718BD.png "点击放大")|
    
2. 真机测试：端插件涉及到端侧的应用，故平台调试无法与端侧应用联调，只能在端侧设备上进行智能体使用效果的真实体验。具体测试流程详见开发者指导文档[真机测试](https://developer.huawei.com/consumer/cn/doc/service/list-of-user-groups-for-real-machine-testing-0000002471264273)。

**上架升级**

功能测试完成后，点击【保存】【上架】即可将智能体提交到上架审核阶段，具体流程可参考开发者指导文档[上/下架、升级流程介绍](https://developer.huawei.com/consumer/cn/doc/service/process-introduction-0000002509696971)。上架完成后，可在端侧小艺的智能体页面搜索查询到创建的智能体并使用。效果如下：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251217205909.09510997935892250760500386845565:50001231000000:2800:0DD0ADFDDA680D1245BCEE2F0600CB6E3C49C3C96AB6D9075BC71E45AAE889B3.png "点击放大")

## 总结

智能体具有拟人化交互与智能决策、多场景需求覆盖的特点，通过 “交互智能化 + 场景定制化” 满足用户与行业需求。[小艺智能体平台](https://developer.huawei.com/consumer/cn/hag/hagindex.html?isInFrame=true&lang=zh_CN#/agentHome/square)依托华为技术生态，为开发者提供从创建到上架的全流程工具支持，助力专属智能体的快速落地与实现。