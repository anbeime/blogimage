# Agent Framework Kit简介

更新时间: 2025-12-16 16:27

Agent Framework Kit（智能体框架服务）提供了拉起指定智能体的能力。

应用在[小艺开放平台](https://developer.huawei.com/consumer/cn/hag/hagindex.html?isInFrame=true&lang=zh_CN#/)上线智能体后，向用户提供应用+智能体组合的服务，让用户可以在适当的场景下通过Agent Framework Kit的UI控件能力主动拉起智能体。

Agent Framework Kit主要包含Function组件。

## Kit场景介绍

- Agent Framework Kit 通过标准化组件，满足应用在不同场景、不同界面下的智能体入口诉求。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162745.32046710520182996201640650927211:50001231000000:2800:776C25AFD396A219268B3ED483301853EBC16FCF028CDD17EFE7CE5665A818C9.png)![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162745.69248043715842235436193074408635:50001231000000:2800:440402FC1C9EA15E35C2187F838B26132FBBE785D484C6F1E6E1FCC50CC04929.png)
    

## 约束与限制

### 支持的设备

当前支持Phone和Tablet设备。

### 支持的国家/地区

仅适用于中国境内（不包含中国香港、中国澳门、中国台湾）。

## 模拟器支持情况

本Kit暂不支持模拟器。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/harmony-agent-framework-kit-guide "Agent Framework Kit（智能体框架服务）")
# 通过Function组件拉起智能体

更新时间: 2025-12-16 16:27

## 场景介绍

- Function组件分为图标组件和按钮组件，无标题时默认显示图标组件，有标题时默认显示按钮组件。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162746.27976277259769394779013878584306:50001231000000:2800:9A173CF9B485BD0B1D9C7A3D8FD270983620D8823AD8222DA5AD1F48EEBDA559.png)
    
- Function图标组件效果：综合型入口。不带用户意图，可作为应用内智能体主入口。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162746.60620769182444049220402398097449:50001231000000:2800:6D9B5B8379B8356C605193B8F7D1ED2542229C692247F567EA286780C555E03F.png)
    
- Function按钮组件：允许应用自定义功能描述的组件。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162746.55825104793899203161180568491155:50001231000000:2800:8AA5E9233F738EEB0B01A325590FE2BB8B30EF6FE98E419131034AA60EC1D1AB.png)
    

## 开发前准备

- 创建智能体，具体请参见[快速创建智能体](https://developer.huawei.com/consumer/cn/doc/service/quick-start-0000002469548009)。
- 关联应用，具体请参见[关联应用](https://developer.huawei.com/consumer/cn/doc/service/related-applications-0000002437785706)。
- 确保已在终端设备上登录华为账号，并且处于联网状态。

## 开发步骤

1. 从项目根目录进入/src/main/ets/pages/Index.ets文件，将FunctionComponent及相关其它类引入到工程。
    
    1. import { FunctionComponent, FunctionController } from '@kit.AgentFrameworkKit';
    2. import { BusinessError } from "@kit.BasicServicesKit";
    3. import { hilog } from "@kit.PerformanceAnalysisKit";
    4. import { common } from '@kit.AbilityKit'
    
2. （可选）可以在组件加载前通过[isAgentSupport](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/hmaf-function-component#section123851974413)来判断当前的AgentId是否可用，若agentId有效且Agent功能支持时再加载组件。
    
    1.   @State isAgentSupport: boolean = false;
    
    2.   aboutToAppear() {
    3.      this.checkAgentSupport()
    4.   }
    5.   async checkAgentSupport() {
    6.     try {
    7.       let context = this.getUIContext()?.getHostContext() as common.UIAbilityContext;
    8.       this.isAgentSupport = await this.controller.isAgentSupport(context, this.agentId)
    9.     } catch (err) {
    10.       hilog.error(0x0001, 'AgentExample', `err code: ${err.code}, message: ${err.message}`)
    11.     }
    12.   }
    
    13.   build() {
    14.     Column() {
    15.       if (this.isAgentSupport) {
    16.         FunctionComponent({
    17.           agentId: this.agentId,
    18.           onError: (err: BusinessError) => {},
    19.           options: {
    20.               title: '智能创建',
    21.               queryText: '创建一个新的模式'
    22.           }
    23.         })
    24.       }
    25.     }
    26.   }
    
3. 构建一个简单配置的页面，在页面中引入FunctionComponent组件，并传入对应的参数。其中agentId、onError是必填参数。其他可选参数可参见[FunctionComponent（功能组件）](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/hmaf-function-component)。Function组件布局可参考[组件布局](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-layout-development)。
    
    1. @Entry
    2. @Component
    3. export struct AgentExample {
    4.     private controller: FunctionController = new FunctionController();
    5.     private agentId: string = 'agentproxy65481da1fa2293a8482d45';
    6.     build() {
    7.         Column() {
    8.             FunctionComponent({
    9.                 agentId: this.agentId,
    10.                 onError: (err: BusinessError) => {},
    11.                 options: {
    12.                     title: '',
    13.                     queryText: ''
    14.                 },
    15.                 controller: this.controller
    16.             })
    17.         }
    18.     }
    19. }
    
4. 添加订阅事件。
    
    1.  aboutToAppear() {
    2.      this.initListeners()
    3.   }
    4.   initListeners() {
    5.     this.controller?.on('agentDialogOpened', this.onAgentOpenedCallback)
    6.     this.controller?.on('agentDialogClosed', this.onAgentClosedCallback)
    7.   }
    8.   onAgentOpenedCallback = () => {
    9.     hilog.info(0x0001, 'AgentExample', 'agent dialog opened callback')
    10.   }
    11.   onAgentClosedCallback = () => {
    12.     hilog.info(0x0001, 'AgentExample', 'agent dialog closed callback')
    13.   }
    14.   aboutToDisappear() {
    15.     this.controller?.off('agentDialogOpened')
    16.     this.controller?.off('agentDialogClosed')
    17.   }
    
    18.   build() {
    19.     Column() {
    20.       FunctionComponent({
    21.         agentId: this.agentId,
    22.         onError: (err: BusinessError) => {
    23.           hilog.error(0x0001, 'AgentExample', `err: ${JSON.stringify(err)}, message: ${err.message}`)
    24.         },
    25.         controller: this.controller
    26.       })
    27.     }
    28.   }
    

## 开发实例

点击按钮，打开智能体对话框。

1. import { BusinessError } from "@kit.BasicServicesKit";
2. import { hilog } from "@kit.PerformanceAnalysisKit";

3. import {
4.   FunctionComponent,
5.   FunctionController
6. } from "@kit.AgentFrameworkKit";

7. @Entry
8. @Component
9. export struct AgentExample {
10.   private controller: FunctionController = new FunctionController();
11.   private agentId: string = 'agentproxy65481da1fa2293a8482d45';

12.   aboutToAppear() {
13.     this.initListeners()
14.   }
15.   initListeners() {
16.     this.controller?.on('agentDialogOpened', this.onAgentOpenedCallback)
17.     this.controller?.on('agentDialogClosed', this.onAgentClosedCallback)
18.   }
19.   onAgentOpenedCallback = () => {
20.     hilog.info(0x0001, 'AgentExample', 'agent dialog opened callback')
21.   }
22.   onAgentClosedCallback = () => {
23.     hilog.info(0x0001, 'AgentExample', 'agent dialog closed callback')
24.   }
25.   aboutToDisappear() {
26.     this.controller?.off('agentDialogOpened')
27.     this.controller?.off('agentDialogClosed')
28.   }

29.   build() {
30.     Column() {
31.       FunctionComponent({
32.         agentId: this.agentId,
33.         onError: (err: BusinessError) => {
34.           hilog.error(0x0001, 'AgentExample', `err: ${JSON.stringify(err)}, message: ${err.message}`)
35.         },
36.         options: {
37.           title: '智能创建',
38.           queryText: '创建一个新的情景',
39.           isShowShadow: true
40.         },
41.         controller: this.controller
42.       })
43.     }
44.   }
45. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/hmaf-introduction "Agent Framework Kit简介")
# CANN Kit简介

更新时间: 2025-12-16 16:27

CANN（Compute Architecture for Neural Networks）是华为面向AI推出的端云一致的异构计算架构。在HarmonyOS设备上，CANN Kit面向Kirin芯片平台为各种人工智能模型和算法提供统一的接入和运行环境。开发者的应用程序使用CANN Kit的API和开发者数据，在设备端实现智能推理、模型训练以及模型优化等操作，充分发挥设备的本地智能处理能力。

模型是将人工智能算法应用于大量训练数据后得到的结果。开发者可以使用模型依据新的输入数据进行智能推理和预测。模型能够完成许多用常规代码实现起来难度较大或效率较低的复杂任务。例如，你可以训练模型对图像进行语义分割，识别图像中的不同物体类别并精确划分其区域或者对语音数据进行处理，实现语音唤醒、语音识别以及语音合成等功能。

开发者可以使用华为昇腾提供的[CANN](https://www.hiascend.com/software/cann)开发平台进行模型的构建和训练。将训练好的模型转换为适合CANN Kit的模型格式，以便集成到开发者的应用中。此外，开发者也可以基于其他开源或自研的机器学习框架进行模型开发，然后借助CANN Kit提供的工具链将模型适配到HarmonyOS生态中。

CANN Kit通过协同调度设备的NPU（神经网络处理单元）、CPU等硬件资源，实现高效的设备端智能计算性能优化。在提升计算效率的同时，尽可能降低对内存和电量的消耗。在设备端直接运行模型，减少了对网络的依赖，不仅保障了开发者数据的隐私安全，还使应用程序在各种网络环境下都能保持快速响应，为开发者提供流畅的智能交互体验。

CANN Kit构建在底层的硬件驱动和优化的计算库之上，面向华为自研的达芬奇架构NPU的计算核心，与云侧昇腾芯片统一支持AscendC自定义算子编程语言和相关工具链，确保开发者面向NPU的开发优化可以一次开发、多端运行。

CANN Kit是HarmonyOS智能生态的重要基石，为众多领域的智能应用提供核心支撑。例如：支持图像视觉相关的Core Vision Kit、用于自然语言处理的Natural Language Kit等AI计算加速能力，同时支持HarmonyOS的MindSpore Lite Kit、Neural Network Runtime Kit，三方的MNN、PaddleLite等推理框架能力，共同打造丰富的智能应用场景。

## 场景

### 模型优化

- Model Zoo：模型库和工具包，为开发者提供海量模型结构及算子，助力开发者选择硬件能效更优的模型结构。
- 模型轻量化：优化模型大小，降低计算量，降低空间占用与算力需求。

### 模型转换

- 离线模型转换：CANN Kit通过OMG工具可以把神经网络各种算子，比如卷积、池化、激活、全连接等离线编译成硬件专用的AI指令序列，同时将数据和权重重新排布，指令与数据融合在一起生成离线模型。
- AIPP（AI Pre-Process）：AI预处理，支持输入数据硬件预处理，包括图像裁剪、通道交换、色域转换、图片缩放、数据类型转换、旋转和图片补边。由于AIPP硬件专用，可以获得更好的推理性能收益。通过模型转化配置文件生成动静态AIPP模型，及完成AIPP功能参数设置。
- 可变data_type：用于模型输入输出数据类型多样性的场景，无需修改训练好的模型，在使用OMG工具进行[模型转换](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-overall-parameter)时，通过指定输入、输出数据类型使得同一个模型适用于不同输入输出的场景。

### 端侧部署

- 模型推理：主要包含模型编译和推理，是其它端侧部署的基础场景。
- AIPP部署：端侧AIPP部署主要为动态AIPP功能提供支持，即同一动态AIPP模型可以支持不同输入且使能不同AIPP功能的推理场景。

- 异构：CANN Kit能够自动识别运行环境上的计算能力，对神经网络进行自适应的子图拆分和设备协同调度能力。能够支持NPU、CPU的计算加速，在没有NPU的情况下，也能通过CPU提供更广泛的硬件适应能力。
- 内存零拷贝：将存放数据的ION内存封装为输入输出张量，直接进行推理，不需要进行输入张量和输出张量的数据拷贝，以便节省内存以及推理时间。
- 深度融合：模型推理时结合硬件深度融合，减少对DDR的访问，提升能效比。

### 单算子

在三方应用框架加载其原始模型阶段，根据算子的输入、输出、权重信息等参数创建相应的单算子执行器对象并完成加载。三方应用框架执行模型推理时，在其中算子计算过程中调用单算子推理接口，完成算子计算。

### AscendC自定义算子开发

AscendC 是CANN Kit针对算子开发场景推出的编程语言，支持C和C++标准规范，最大化匹配开发者开发习惯；通过多层接口抽象、自动并行计算、孪生调试等关键技术，提高算子开发效率，助力AI开发者低成本完成算子开发和模型调优部署。

## 基本概念

在进行CANN Kit开发前，开发者应了解以下基本概念：

- NPU
    
    NPU（Neural-network Processing Unit，神经网络处理器）是一种专门用于进行深度学习计算的芯片。
    
- 算子
    
    深度学习算法由一个个计算单元组成，我们称这些计算单元为算子（Operator，简称OP）。
    
- 异构计算
    
    异构计算（Heterogeneous Computing），又译异质运算，主要是指使用不同类型指令集或体系架构的计算单元组成系统的计算方式。CANN Kit使用到的计算单元类别包括CPU、NPU等。
    
- AIPP
    
    AIPP是针对AI推理的输入数据进行预处理的模块。CANN Kit模型推理一般需要标准化输入数据格式，而一般模型推理场景数据是一张图片，在格式上存在多样性，AIPP可实现不同格式图片数据到NPU标准输入数据格式的转换。对已训练好的模型，不用重新训练匹配推理计算平台需要的数据格式，而只通过AIPP参数配置或者在软件上调用AIPP接口即可完成适配。由于AIPP硬件专用，可以获得较好的推理性能收益，又可以称为“硬件图像预处理”。
    
- 量化蒸馏
    
    是一种结合模型压缩技术的方法，旨在通过在量化过程中引入教师模型的知识来指导学生模型的学习，从而减少量化带来的精度损失。这种方法的核心目标是在降低模型大小和计算复杂度的同时，尽可能保留模型的性能。
    

## 约束与限制

- 设备限制
    
    本Kit仅适用于带有Kirin NPU的Phone、Tablet、PC/2in1、TV设备。从5.1.0(18)版本开始，新增支持TV设备。
    

## 模拟器支持情况

本Kit暂不支持使用模拟器运行调试。

## 与相关Kit的关系

HarmonyOS AI开放层次由上层到底层分别为：

- MindSpore Lite Kit：HarmonyOS内置的轻量化AI引擎，提供统一推理接口和多后端硬件加速能力，使能手机、PC/2in1、TV等全场景智能应用。
- Neural Network Runtime Kit：面向AI领域的跨芯片推理计算运行时，作为中间桥梁连通上层AI推理框架和底层加速芯片，实现AI模型的跨芯片推理计算。
- CANN Kit：海思AI硬件统一开放计算架构，支持AscendC NPU自定义编程、端云协同复用，擅长偏重载AI计算、需深度优化性能功耗场景。

Neural Network Runtime Kit可支持系统内置的MindSpore Lite推理框架（MindSpore Lite Kit），MindSpore Lite Kit已开放了配置NNRt的Native接口。

MindSpore Lite Kit对接NNRt可无需构图，两者共享同一份模型图格式（MindIR），因此使用MindSpore Lite在NNRt上加载模型将快于其他AI推理框架。此外，MindSpore Lite也支持通用硬件CPU/GPU与NNRt AI加速硬件之间的模型异构推理功能。

CANN Kit作为麒麟平台的后端接入Neural Network Runtime Kit，支撑Neural Network Runtime Kit于麒麟平台的AI计算能力。CANN Kit构建在底层的硬件驱动和优化的计算库之上，与云侧昇腾芯片统一支持AscendC自定义算子编程语言和相关工具链，是HarmonyOS智能生态的重要基石，为众多领域的智能应用提供核心支撑。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cann-kit-guide "CANN Kit（CANN 服务）")
# 开发准备

更新时间: 2025-12-16 16:27

## 环境准备

- 使用Ubuntu 64位运行[Tools下载](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-preparations#section152959341125)中tools_omg模型转换工具。
- 推荐使用[Ubuntu 22.04](https://mirrors.ustc.edu.cn/ubuntu-releases/22.04/)及以上版本、MacOS 10.14及以上版本、Windows 10及以上版本安装应用开发环境[DevEco Studio](https://developer.huawei.com/consumer/cn/deveco-studio/)。
- 准备训练好的tools_omg模型转换工具生成的[离线模型](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-overall-parameter)或者从[Model Zoo](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-model-zoo)中选择合适的模型。

## Tools下载

|Tools名称|Tools说明|Tools下载|SHA256校验码|
|:--|:--|:--|:--|
|轻量化工具<br><br>包名：tools_dopt|对原始模型进行轻量化，以减少模型体积及加快模型推理速度。|[DDK-tools-5.1.1.1](https://contentcenter-vali-drcn.dbankcdn.cn/pvt_2/DeveloperAlliance_package_901_9/c0/v3/Evg84kYpQlOkQvRT-Th0tw/DDK-tools-next-5.1.1.1.zip?HW-CC-KV=V1&HW-CC-Date=20251015T082207Z&HW-CC-Expire=315360000&HW-CC-Sign=8D8CE92B39E6A5353B8A43EB6779C1D79C346C40776F2242593CBD751BE87EE4)|327ce5ccbd46b065ad51374b9ae0ccc0bb40885cd7c812e7fdb5ffcc56ebc821|
|OMG工具<br><br>包名：tools_omg|模型转换工具。|
|AscendC工具<br><br>包名：tools_ascendc|为AscendC算子开发提供的算子功能、性能调测集成工具。|
|平台插件包<br><br>包名：<br><br>kirin9020<br><br>kirinx90|AscendC工具提供不同平台的差异化能力，使用AscendC工具前需要将对应的平台安装到platform目录下。|[kirin9020-plugin-5.1.1.1](https://contentcenter-vali-drcn.dbankcdn.cn/pvt_2/DeveloperAlliance_package_901_9/ba/v3/OT4f_UBMQ12GwDLT3BLq3w/kirin9020-plugin-next-5.1.1.1.zip?HW-CC-KV=V1&HW-CC-Date=20251015T082401Z&HW-CC-Expire=315360000&HW-CC-Sign=7CAFE06F0BE3434038FAB97747F7572B274B066C319269409A113C500C39EBD7)|8bc78d6b01406607586da3b3e3b08df42a9851a1487eae4d920ac6fa144a6e2f|
|[kirinx90-plugin-5.1.1.1](https://contentcenter-vali-drcn.dbankcdn.cn/pvt_2/DeveloperAlliance_package_901_9/ec/v3/Rt5xiuz6TCW9d2WfgR298w/kirinx90-plugin-next-5.1.1.1.zip?HW-CC-KV=V1&HW-CC-Date=20251015T082301Z&HW-CC-Expire=315360000&HW-CC-Sign=DB886FA5CD77C3AE802DC8BCD1BC84A8F0B8831B532412314E29D9CCCC096DC0)|93ffd9458f56189c4c2446f1e063ffacfc9fea892880341655828740deb9c4a6|

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-introduction "CANN Kit简介")
# Model Zoo

更新时间: 2025-12-16 16:27

## 概述

Model Zoo提供了可直接调用的硬件最优模型库，集成图片分类、目标检测、语义分割、超分等典型场景的网络模型，包含CANN性能调优使用指导、性能友好模型结构和推荐指数。帮助开发者快速了解算子的参数取值如何在硬件上获得更好的性能和能效收益，以及如何优化模型结构可以实现高性能与低功耗。

## Model Zoo模型下载

在模型下载中，.caffemodel、.pb、.onnx文件是原始浮点模型，基于相关论文实现，并进行了NPU硬件亲和性调整。因此，这些模型的输入尺寸可能与论文中描述的尺寸有所差异。

.om是标准IR算子构建的OM模型文件，其中quant8_8.om是量化生成的OM模型文件，所有模型可通过[Netron工具](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-visualization-tool-usage)可视化。

Model Zoo中模型的名称、性能、模型下载信息如下表所示。

|场景|网络模型（单batch）|浮点性能[1]（耗时ms）|量化性能[1]（耗时ms）|模型下载|SHA256校验码|参考[2]|
|:--|:--|:--|:--|:--|:--|:--|
|图片分类|Alexnet|9.92|4.49|CAFFE&OM|7b01980acf0d16dadc6c9c326cdf757d2166928ae49cfd4091df154a5c512640|[论文&实现](https://arxiv.org/abs/1404.5997)|
|Resnet18|2.63|1.24|CAFFE&OM|4aa7caaa112f5280cb5c0ab5eed6edf84a16fe9a0b92b9ee333a808c9f07e886|[论文&实现](https://arxiv.org/abs/1512.03385)|
|VGG16|16.56|8.55|TF&OM|f9193765889077e5997ddc8c1e75a563c8a1205e613da9634d3d83277962dd42|[论文&实现](https://arxiv.org/abs/1409.1556)|
|VGG19|18.34|8.73|TF&OM|d19f363602740ff5859380c40ca6f0bed0cb3744f469873cdf862c71c7007a94|[论文&实现](https://arxiv.org/abs/1409.1556)|
|Resnet50|5.15|3.54|TF&OM|6dedf4b5c3bfdaf70410236f1f73d942a5231f217e18c51918ba39b3b740b2df|[论文&实现](https://arxiv.org/abs/1512.03385)|
|Inception_v3|6.56|3.76|TF&OM|d06c88a79acd19b10d5f7eddaae6aba3c02372cfdb036296b845aa3a9ccf46be|[论文&实现](https://arxiv.org/abs/1512.00567)|
|Inception_v4|11.90|7.29|TF&OM|e042f489e6915eb6de5daa4b3200462e76f1bedca7147e2a19e8311a4b05afde|[论文&实现](https://arxiv.org/abs/1602.07261)|
|Inception_Resnet_v2|15.91|5.59|TF&OM|229164e49753126357f4a587694ca925afa60d1bfec184dba00085d69b5fc47b|[论文&实现](https://arxiv.org/abs/1602.07261)|
|Mobilenet_v1|2.16|0.52|TF&OM|864ef1d651e7f2cb9de69ce34d81e40783bdac47069b6db22aefb6f4ae17f24b|[论文&实现](https://arxiv.org/abs/1704.04861)|
|Mobilenet_v2|2.49|1.18|TF&OM|362c0169917122e45f4c5aed69ad3b9c8509b51a0531e6912360eff6c8b81cbc|[论文&实现](https://arxiv.org/abs/1801.04381)|
|Mobilenet_v2_1.4|3.16|1.67|TF&OM|8f1a05a83e813fac16e958ad5436569fe83f75f88137819d52ce2e268ad04126|[论文&实现](https://arxiv.org/abs/1704.04861)|
|Mobilenet_v3_Large|3.29|2.33|TF&OM|086640ff192629b6dba33d905ddb0925d612e395703948c6c7221f2e4126b85d|[论文&实现](https://arxiv.org/abs/1905.02244)|
|Googlenet|34.69|1.64|ONNX&OM|97ef0325be2c3b8824a903abaeea943260d2f349da63d193168c96eff735ad0e|[论文&实现](https://arxiv.org/abs/1409.4842)|
|Squeezenet_v1|2.13|1.24|ONNX&OM|e20be44bdaa30b9fa4a22ef876c1e7bd88db49b5d063992ef1595b34d3544997|[论文&实现](https://arxiv.org/abs/1602.07360)|
|目标检测|SSD_mobilenetv2_voc|5.02|2.84|CAFFE&OM|1d273130a07a6f888f6df1088b478049da9a961a3dbeaca7bfa92e616f0f01e9|[论文1&实现1](https://arxiv.org/abs/1801.04381)、[论文2&实现2](https://arxiv.org/abs/1512.02325)|
|Yolo_v5|4.74|4.33|ONNX&OM|83a205d70fcd9b31c13530da0b8752a6976b125b02ac07091fd088f58cd5a80f|[论文&实现](https://arxiv.org/abs/1804.02767)|
|语义分割|FCN|131.23|62.76|CAFFE&OM|0cd87a51c1ea978a68e9cd4790106e99d910f78d5e68ec06e2bdd637aae5a73c|[论文&实现](https://arxiv.org/abs/1605.06211)|
|DeepLab_v3|17.40|13.87|TF&OM|381f830f6b0154bf086dbc5b15575465a34c1b3d233a6d27bc417077832697c7|[论文&实现](https://arxiv.org/abs/1706.05587)|
|超分|VDSR|17.71|10.67|CAFFE&OM|bf5a699ea55b2d2e42ac40884f2697d807b5b3f37e655ecb342e873c6ba6b844|[论文&实现](https://arxiv.org/abs/1511.04587)|
|FSRCNN|17.24|17.02|TF&OM|03775c806d8d166fd29753ea8eaa3db377246fa469487b7e161a9e405a6ffa1c|[论文&实现](https://arxiv.org/abs/1608.00367)|

说明

- [1] 此性能数据测试基于kirin 9000芯片的华为手机。
- [2] 原始模型文件是参考论文和实现中的模型训练而来。

除Model Zoo中推荐的网络模型，还可以构建自定义的网络模型。性能优势的算子和计算结构如下。

## CANN算子性能指导

从易用性角度上来说，提供的算子功能不存在限制，但是从性能的使用角度上来说，是基于算子实现方式给出对应的性能使用指导。

### NN算子

|IR算子|性能使用指导|推荐使用指数|
|:--|:--|:--|
|Activation|当前性能硬件最优。|☆☆☆☆☆|
|HardSwish|当前性能硬件最优。|☆☆☆☆☆|
|PRelu|当前性能硬件最优。|☆☆☆☆☆|
|BNInference|当前性能硬件最优。<br><br>Conv(depthwise)+Bn组合使用时，会进行图融合优化抵消。|☆☆☆☆☆|
|Convolution|当Cin和Cout都是16的倍数时性能最优。|☆☆☆☆☆|
|QuantizedConvolution|当Cin和Cout都是32的倍数时性能最优。|☆☆☆☆☆|
|ConvTranspose|- 当Cin和Cout都是16的倍数时性能最优。<br><br>- 当前针对kernel 1*1，2*2，3*3，8*8优化性能最优。|☆☆☆☆☆|
|BiasAdd|当前性能硬件最优。<br><br>Conv(depthwise)+BiasAdd组合使用时，会进行图融合优化抵消。|☆☆☆☆☆|
|Eltwise|当前性能硬件最优。|☆☆☆☆☆|
|LRN|当前性能硬件较优。<br><br>- 计算过程中计算均值方差，计算量较大，性能差于batchNorm。<br>- 主要用于图像增强，对精度计算较敏感，NPU使用FP16计算存在精度风险。|☆☆☆|
|ConvolutionDepthwise|当前性能硬件最优。|☆☆☆☆☆|
|QuantizedConvolutionDepthwise|当前性能硬件最优。|☆☆☆☆☆|
|FullyConnection|性能受DDR带宽限制，非算力受限算子，算法设计时合理配置权重大小。|☆☆☆☆☆|
|QuantizedFullyConnection|性能受DDR带宽限制，非算力受限算子，算法设计时合理配置权重大小。|☆☆☆☆☆|
|PoolingD|当前性能硬件最优。|☆☆☆☆☆|
|Scale|当前性能硬件最优。<br><br>Conv(depthwise)+Scale组合使用时，会进行图融合优化抵消。|☆☆☆☆☆|
|ShuffleChannel|kirin 9000芯片的手机性能较优，其余芯片的手机无性能优化，仅支持功能。|☆|
|ShuffleChannelV2|为了适配支持ANN场景算子，性能较差，仅支持功能。|☆|
|Softmax|当前性能硬件最优。<br><br>4维输入，axis=1，基于C通道做softmax时性能最优。|☆☆☆☆☆|
|TopK|为了适配支持ANN场景算子，性能较差，仅支持功能。|☆|
|LogSoftmax|当前性能硬件最优。|☆☆☆☆☆|
|Rank|shape推导类算子，模型构建时即可抵消。|☆☆☆☆☆|
|ScatterNd|非规则数据搬移，性能较差，不建议模型过多使用。|☆☆☆|
|LogicalXor|当前性能硬件最优。|☆☆☆☆☆|
|Threshold|当前性能硬件最优。|☆☆☆☆☆|
|AxisAlignedBboxTransform|当前性能硬件最优。|☆☆☆☆☆|
|Normalize|当前性能硬件最优。|☆☆☆☆☆|
|SVDF|当前性能硬件最优。|☆☆☆☆☆|
|ReduceMean|当前性能硬件最优。|☆☆☆☆☆|
|LayerNorm|当前性能硬件最优。<br><br>- 计算过程中计算均值方差，计算量较大，性能差于batchNorm。<br>- 主要用于图像增强，对精度计算较敏感，NPU使用FP16计算存在精度风险。|☆☆☆|
|InstanceNorm|当前性能硬件较优。<br><br>- 计算过程中计算均值方差，计算量较大，性能差于batchNorm。<br>- 主要用于图像增强，对精度计算较敏感，NPU使用FP16计算存在精度风险。|☆☆☆|
|PriorBox|当前性能硬件最优。|☆☆☆☆☆|
|LSTM|当前性能硬件较优，功能支持较窄。|☆☆☆☆|

### Math算子

|IR算子|性能使用指导|推荐使用指数|
|:--|:--|:--|
|Add|当前性能硬件最优。|☆☆☆☆☆|
|Mul|当前性能硬件最优。|☆☆☆☆☆|
|Expm1|当前性能硬件最优。|☆☆☆☆☆|
|Ceil|当前性能硬件最优。|☆☆☆☆☆|
|Sin|性能较差。|☆|
|Cos|性能较差。|☆|
|Floor|当前性能硬件最优。|☆☆☆☆☆|
|Log1p|当前性能硬件最优。|☆☆☆☆☆|
|LogicalAnd|当前性能硬件最优。|☆☆☆☆☆|
|LogicalNot|当前性能硬件最优。|☆☆☆☆☆|
|Maximum|kirin 9000芯片的手机性能较优，其余芯片的手机无性能优化，仅支持功能。|☆|
|Minimum|kirin 9000芯片的手机性能较优，其余芯片的手机无性能优化，仅支持功能。|☆|
|Equal|当前性能硬件最优。|☆☆☆☆☆|
|Reciprocal|当前性能硬件最优。|☆☆☆☆☆|
|Sqrt|当前性能硬件最优。|☆☆☆☆☆|
|Square|当前性能硬件最优。|☆☆☆☆☆|
|CastT|kirin 9000芯片的手机性能较优，其余芯片的手机无性能优化，仅支持功能。|☆|
|Sign|当前性能硬件最优。|☆☆☆☆☆|
|Exp|当前性能硬件最优。|☆☆☆☆☆|
|FloorMod|当前性能硬件最优。|☆☆☆☆☆|
|GreaterEqual|当前性能硬件最优。|☆☆☆☆☆|
|Greater|当前性能硬件最优。|☆☆☆☆☆|
|Less|当前性能硬件最优。|☆☆☆☆☆|
|MatMul|当前性能硬件最优。|☆☆☆☆☆|
|RealDiv|性能较差，建议等效成mul或者Reciprocal+mul。|☆|
|Rint|kirin 9000芯片的手机性能较优，其余芯片的手机无性能优化，仅支持功能。|☆|
|Round|kirin 9000芯片的手机性能较优，其余芯片的手机无性能优化，仅支持功能。|☆|
|Rsqrt|kirin 9000芯片的手机性能较优，其余芯片的手机无性能优化，仅支持功能。|☆|
|Sub|当前性能硬件最优。|☆☆☆☆☆|
|Range|模型构建时最优。|☆☆☆☆☆|
|Acos|当前性能硬件最优。|☆☆☆☆☆|
|Asin|当前性能硬件最优。|☆☆☆☆☆|
|Log|当前性能硬件最优。|☆☆☆☆☆|
|LogicalOr|当前性能硬件最优。|☆☆☆☆☆|
|Neg|当前性能硬件最优。|☆☆☆☆☆|
|ReduceProdD|kirin 9000芯片的手机性能较优，其余芯片的手机无性能优化，仅支持功能。|☆|
|ReduceSum|当前性能硬件最优。|☆☆☆☆☆|
|Tan|性能较差。|☆|
|Power|当前性能硬件最优。|☆☆☆☆☆|
|Pow|性能较差。|☆|
|ArgMaxExt2|当前性能硬件最优。|☆☆☆☆|
|FloorDiv|性能较差，不建议使用。|☆|
|NotEqual|当前性能硬件最优。|☆☆☆☆☆|
|LessEqual|当前性能硬件最优。|☆☆☆☆☆|
|SquaredDifference|当前性能硬件最优。|☆☆☆☆☆|
|Atan|当前性能硬件最优。|☆☆☆☆☆|
|BatchMatMul|当前性能硬件最优。|☆☆☆☆☆|
|ClipByValue|当前性能硬件最优。|☆☆☆☆☆|
|L2Normalize|当前性能硬件最优。|☆☆☆☆☆|
|ReduceMax|kirin 9000芯片的手机性能较优，其余芯片的手机无性能优化，仅支持功能。|☆|
|ReduceMin|kirin 9000芯片的手机性能较优，其余芯片的手机无性能优化，仅支持功能。|☆|

### Array算子

|IR算子|性能使用指导|推荐使用指数|
|:--|:--|:--|
|ConcatD|当前性能硬件最优。<br><br>当Cin是16的倍数且Cout是16的倍数时，做图融合抵消，性能最优。|☆☆☆☆☆|
|FakeQuantWithMinMaxVars|当前性能硬件最优。|☆☆☆☆☆|
|Reshape|当前性能硬件最优。<br><br>有些场景算子会被融合抵消掉。|☆☆☆☆☆|
|SplitD|当前性能硬件最优。<br><br>当Cin是16的倍数且Cout是16的倍数时，做图融合抵消，性能最优。|☆☆☆☆☆|
|SplitV|由于是乱序的数据重排，性能较差。|☆|
|Unpack|由于是乱序的数据重排，性能较差。|☆|
|Flatten|由于是乱序的数据重排，性能较差。|☆|
|Slice|由于是乱序的数据重排，性能较差。|☆|
|ExpandDims|shape推导类算子，模型构建时即可抵消。|☆☆☆☆☆|
|GatherV2D|由于是乱序的数据重排，性能较差。|☆|
|GatherNd|由于是乱序的数据重排，性能较差。|☆|
|Pack|由于是乱序的数据重排，性能较差。|☆|
|SpaceToDepth|由于是乱序的数据重排，性能较差。|☆|
|DepthToSpace|由于是乱序的数据重排，大部分场景性能较差。<br><br>针对4宫格场景（Cin=4，block=1）有特殊优化，性能较优。|☆☆|
|StridedSlice|由于是乱序的数据重排，性能较差。|☆|
|SpaceToBatchND|由于是乱序的数据重排，性能较差。|☆|
|BatchToSpaceND|由于是乱序的数据重排，性能较差。|☆|
|Tile|由于是乱序的数据重排，性能较差。|☆|
|Size|shape推导类算子，模型构建时即可抵消。|☆☆☆☆☆|
|Fill|由于是乱序的数据重排，性能较差。|☆|
|Select|仅支持功能。|☆☆|
|PadV2|针对HW方向补0的场景性能较优。<br><br>其他场景由于乱序的数据重排，性能较差。|☆☆☆|
|Squeeze|shape推导类算子，模型构建时即可抵消。|☆☆☆☆☆|
|Pad|针对HW方向补0的场景性能较优。<br><br>其他场景由于乱序的数据重排，性能较差。|☆☆☆|
|MirrorPad|其他场景由于乱序的数据重排，性能较差。|☆|
|OneHot|其他场景由于乱序的数据重排，性能较差。|☆|
|Shape|shape推导类算子，模型构建时即可抵消。|☆☆☆☆☆|
|Dequantize|当前性能硬件最优。|☆☆☆☆☆|
|Quantize|当前性能硬件最优。|☆☆☆☆☆|

### Detection算子

|IR算子|性能使用指导|推荐使用指数|
|:--|:--|:--|
|Permute|由于乱序的数据重排，虽然做了相关优化，但是硬件不适合过多此类操作。|☆☆☆|
|SSDDetectionOutput|当前性能最优。|☆☆☆☆☆|

### Image算子

|IR算子|性能使用指导|推荐使用指数|
|:--|:--|:--|
|ImageData<br><br>DynamicImageData<br><br>ImageCrop<br><br>ImageChannelSwap<br><br>ImageColorSpaceConvertion<br><br>ImageResize<br><br>ImageDataTypeConversion<br><br>ImagePadding|AIPP相关图形处理算子，性能硬件最优。|☆☆☆☆☆|
|CropAndResize|仅功能支持，性能较差。|☆|
|ResizeBilinear<br><br>ResizeBilinearV2<br><br>Interp|大部分场景性能硬件最优，个别场景待优化。|☆☆☆☆☆|
|ResizeNearestNeighbor<br><br>Upsample|大部分场景性能硬件最优，个别场景待优化。|☆☆☆☆☆|
|Crop|仅功能支持，性能较差。|☆|
|NonMaxSuppressionV3D|仅功能支持，性能较差。|☆|

## 性能友好计算结构

|应用场景|网络类型|推荐指数|推荐说明|
|:--|:--|:--|:--|
|分类网络|AlexNet|☆☆☆☆|全连接层权重较大，推理过程带宽受限，可从[Model Zoo](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-model-zoo#section175551381682)中下载。|
|VGG16|☆☆☆☆|全连接层权重较大，推理过程带宽受限，可从[Model Zoo](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-model-zoo#section175551381682)中下载。|
|VGG19|☆☆☆|全连接层权重较大，推理过程带宽受限，可从[Model Zoo](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-model-zoo#section175551381682)中下载。|
|ResNet18/34/50/101/152|☆☆☆☆☆|模型权重大小适中，硬件算力利用率接近100%，ResNet50可从[Model Zoo](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-model-zoo#section175551381682)下载。|
|GoogleNet|☆☆☆☆|硬件算力利用率接近75%，可从[Model Zoo](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-model-zoo#section175551381682)中下载。|
|InceptionV3|☆☆☆☆|硬件算力利用率接近85%，可从[Model Zoo](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-model-zoo#section175551381682)中下载。|
|InceptionV4|☆☆☆☆|硬件算力利用率接近85%，可从[Model Zoo](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-model-zoo#section175551381682)中下载。|
|Inception_Resnet_v2|☆☆☆☆|硬件算力利用率接近90%，可从[Model Zoo](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-model-zoo#section175551381682)中下载。|
|Xception|☆☆☆☆|硬件算力利用率接近85%，可从[Model Zoo](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-model-zoo#section175551381682)中下载。|
|MobileNet_v1|☆☆☆☆☆|模型权重大小适中，硬件算力利用率接近95%，可从[Model Zoo](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-model-zoo#section175551381682)中下载。|
|MobileNet_v2|☆☆☆☆☆|模型权重大小适中，硬件算力利用率接近95%，可从[Model Zoo](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-model-zoo#section175551381682)中下载。|
|MobileNet_v3|☆☆☆☆☆|模型权重大小适中，硬件算力利用率接近95%，可从[Model Zoo](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-model-zoo#section175551381682)中下载。|
|SqueezeNet|☆☆☆☆☆|模型权重大小适中，硬件算力利用率接近95%，可从[Model Zoo](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-model-zoo#section175551381682)中下载。|
|DenseNet|☆☆☆☆☆|模型权重大小适中，硬件算力利用率接近95%。|
|ShuffleNet_v1<br><br>ShuffleNet_v2|☆|存在大量shuffleChannel操作，本身是内存搬移操作，非计算受限。<br><br>此网络为带宽受限网络，shuffleChannel仅支持功能，性能不保证较优。|
|Resnext|☆☆☆☆|硬件算力利用率接近85%。|
|EfficientNet|☆☆☆☆☆|模型权重大小适中，硬件算力利用率接近95%。|
|SENet|☆☆☆☆|硬件算力利用率接近75%。|
|目标检测|Faster_RCNN|☆☆☆☆☆|硬件算力利用率接近85%。|
|SSD|☆☆☆☆|硬件算力利用率接近85%，当前仅支持通过omg流程生成。|
|FPN|☆☆☆☆☆|硬件算力利用率接近90%，后处理不在模型中，由算法单独完成。|
|语义分割|FCN|☆☆☆☆☆|硬件算力利用率接近85%，由于模型计算量较大，实际部署时要做参数裁剪，可从[Model Zoo](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-model-zoo#section175551381682)中下载 。|
|DeepLabV3|☆☆☆|硬件算力利用率接近60%，可从[Model Zoo](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-model-zoo#section175551381682)中下载。|
|Unet|☆☆☆|硬件算力利用率接近60%。|
|MaskRcnn|☆☆|硬件算力利用率接近80%（仅限tf->om版本，IR对接方式不支持）。|
|PSPNet|☆☆☆|不支持pyramid pooling算子，可以通过多个pool等效，性能一般。|
|超分|VDSR|☆☆☆☆☆|硬件算力利用率接近85%，可以达到实时超分要求，可从[Model Zoo](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-model-zoo#section175551381682)中下载。|
|FSRCNN|☆☆☆☆|硬件算力利用率接近70%，可以达到部分实时超分要求，可从[Model Zoo](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-model-zoo#section175551381682)中下载。|
|SRCNN|☆☆☆☆|硬件算力利用率接近70%，可以达到部分实时超分要求。|
|DnCNN|☆☆☆☆|硬件算力利用率接近65%，计算量较大，可以达到部分实时超分要求。|
|DRCN|☆☆☆☆|硬件算力利用率接近65%，计算量较大，可以达到部分实时超分要求。|
|DRRN|☆☆☆|硬件算力利用率接近60%，计算量较大，可以达到部分实时超分要求。|
|EnhanceNet|☆☆☆|硬件算力利用率接近60%，计算量较大，可以达到部分实时超分要求。|
|语音语义|RNN|☆☆|功能支持较为单一。|
|LSTM|☆☆|功能支持较为单一。|
|Transformer|☆☆☆☆|硬件算力利用率接近70%。|
|Bert|☆☆☆☆|硬件算力利用率接近70%。|

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-model-optimization "模型优化")
# 概述

更新时间: 2025-12-16 16:28

## 简介

轻量化工具是一款集模型压缩算法和网络结构搜索算法于一体的自动模型轻量化工具，针对NPU架构对深度神经网络模型进行深度的模型优化，可以帮助开发者自动地完成模型轻量化以及网络结构的生成任务。目前支持无训练模式、插件式量化模式、大语言模型低位量化和网络结构搜索训练。

- 无训练量化：开发者可以直接输入模型，无需重训练，快速的完成模型轻量化。适用于快捷方便量化的开发者使用。

- 插件式量化：为开发者提供模型量化API，在开发者训练工程中对浮点模型进行量化模型校准或量化模型重训练，易用性高，插件式重训练量化适用于较高精度要求的开发者。
- 大语言模型低位量化：提供大语言模型的4bit低位量化支持。通过权重量化、激活量化和参数提取三段式执行流程，实现大模型压缩。
- 网络结构搜索训练：支持分类网络、检测网络、分割网络三种网络类型。开发者配置相应的搜索参数和接口函数后，使用网络结构搜索工具进行搜索，在设定的算力约束下，得到优秀的网络模型。适用于需要自动生成网络结构的开发者。

|模式|支持的框架|支持的策略|支持的设备|
|:--|:--|:--|:--|
|无训练量化|TensorFlow、PyTorch、ONNX|Quant_INT8-8|同时支持CPU和GPU模式，GPU支持单机单卡。|
|插件式量化|TensorFlow、PyTorch|Quant_INT8-8|支持GPU，支持单机单卡。|
|网络结构搜索训练|TensorFlow、PyTorch|NASEA|支持GPU，支持单机单卡和单机多卡。|
|大语言模型低位量化|PyTorch|Quant_INT16-4|支持GPU，量化蒸馏支持单机多卡。|

说明

Quant_INT8-8：数据8bit量化，权重8bit量化。

Quant_INT16-4：数据16bit量化，权重4bit量化。

通过模型轻量化以及网络结构搜索获得模型在NPU上的收益可以参见[模型收益](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-model-benefits)。

经过轻量化工具小型化后的模型，可以使用OMG转换工具转为OM离线模型，使用方式可参见[量化模型转换](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-model-conversion-example#section29012331976)。

该轻量化工具位于“tools_dopt”目录下。

|目录文件|描述说明|
|:--|:--|
|tools_dopt/dopt_tf_py3|TensorFlow框架无训练，插件式量化，网络结构搜索的工具入口以及demo。|
|tools_dopt/dopt_pytorch_py3|PyTorch框架无训练，插件式，大语言模型量化，网络结构搜索的工具入口以及demo。|
|tools_dopt/dopt_onnx_py3|ONNX框架无训练工具入口。|

## 支持范围

- 插件式支持GPU训练，单机单卡训练。
- 无训练支持CPU和GPU量化。
- 大语言模型低位量化支持GPU量化。
- 网络结构搜索工具支持单机单卡和单机多卡，进行分类、检测、分割场景的骨架搜索，依赖运行环境参见[环境准备](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-network-structure-search-training#section193737375169)。

## 系统要求

- TensorFlow开发者使用本工具需同时满足下列环境要求：
    - Python 3.10
    - Ubuntu 22.04
    - Tensorflow 2.8.0
    - GPU需要使用支持CUDA的显卡（无训练量化可不配置）
- PyTorch开发者使用本工具需同时满足下列环境要求：
    - Python 3.10
    - Ubuntu 22.04
    - PyTorch 1.11
    - opencv-python
    - GPU需要使用支持CUDA的显卡（无训练量化可不配置）

- ONNX开发者使用本工具需同时满足下列环境要求：
    - Python 3.10
    - Ubuntu 22.04
    - ONNX Runtime 1.15
    - ONNX 1.14

## 开发者指引

下面列举了不同开发者场景对应的步骤和工具链功能。开发者可以根据下表中列举的不同场景选择适宜的优化方式。

### TensorFlow开发者

|**开发者场景**|**使用依赖**|**工具链提供功能**|**建议使用工具**|优势|
|:--|:--|:--|:--|:--|
|- 缺少足量数据集和训练资源<br>- 追求高易用性|- 可运行TensorFlow环境<br>- 模型pb文件（需要开发者自行转换）<br>- 校准集|Quant_INT8-8|[TensorFlow无训练量化](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-no-training-and-quantization#section293645783311)|无需TensorFlow编写代码，新手开发者友好|
|- 对精度要求较高<br>- 有足够数据集和训练资源<br>- 有一定编程能力<br>- 持有模型训练工程|- 可运行TensorFlow环境<br>- 模型的ckpt文件<br>- 训练集<br>- 测试集<br>- 开发者需要在训练工程中调用轻量化工具API量化模型并进行重训练|Quant_INT8-8|[TensorFlow插件式量化](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-plugin-based-quantization#section16110815547)|模型精度可保障|
|- 需要自动生成符合需求的网络结构|- [环境准备](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-network-structure-search-training#section193737375169)<br>- 训练集<br>- 测试集<br>- 开发者需要根据说明书编写模型接口代码|搜索生成网络结构|[网络结构搜索训练](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-network-structure-search-training)|可根据开发者提供的配置信息自动搜索到在特定场景上表现优秀的网络结构|

### PyTorch开发者

|**开发者场景**|**使用依赖**|**工具链提供功能**|**建议使用工具**|**优势**|
|:--|:--|:--|:--|:--|
|- 缺少足量数据集和训练资源<br>- 追求高易用性|- 可运行PyTorch环境<br>- 模型参数文件pth<br>- python模型定义<br>- 校准集|Quant_INT8-8|[PyTorch无训练量化](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-no-training-and-quantization#section18483131873820)|无需PyTorch编写代码，新手开发者友好|
|- 对精度要求较高<br>- 有足够数据集和训练资源<br>- 有一定编程能力|- 可运行PyTorch环境<br>- 模型参数文件pth<br>- 训练集<br>- 测试集<br>- 开发者需要调用轻量化工具API量化模型并进行重训练|Quant_INT8-8|[PyTorch插件式量化](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-plugin-based-quantization#section162431930104618)|模型精度可保障|
|- 需要自动生成符合需求的网络结构|- [环境准备](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-network-structure-search-training#section193737375169)<br>- 训练集<br>- 测试集<br>- 开发者需要根据说明书编写模型接口代码|搜索生成网络结构|[网络结构搜索训练](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-network-structure-search-training)|可根据开发者提供的配置信息自动搜索到在特定场景上表现优秀的网络结构|
|- 需要对大语言模型进行4bit权重量化|- 训练集<br>- 开发者根据说明书生成配置文件和执行脚本<br>- 脚本执行量化|Quant_INT16-4|[大语言模型低位量化](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-large-language-model)|超大规模模型，权重压缩至4bit|

### ONNX开发者

|**开发者场景**|**开发者需要准备**|**工具链提供功能**|**建议使用工具**|优势|
|:--|:--|:--|:--|:--|
|- 缺少足量数据集和训练资源<br>- 追求高易用性|- 可运行ONNX Runtime环境<br>- ONNX model<br>- 校准集|Quant_INT8-8|[ONNX模型无训练量化](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-no-training-and-quantization#section1262217244312)|无需编写代码，新手开发者友好|

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-lightweight-tool-instructions "模型轻量化")
# 无训练量化

更新时间: 2025-12-16 16:28

## 输入准备

### 准备模型

- TensorFlow开发者
    
    开发者需提供需要量化的pb模型。
    
- PyTorch开发者
    
    开发者需提供需要量化的模型定义py文件以及模型参数pth文件。
    
- ONNX开发者
    
    开发者需提供需要量化的ONNX模型。
    

### 准备校准集

开发者需提供bin格式或图片格式的校准集。bin格式的输入数据需按照以下方式存储，如[任意维度二进制校准集说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-no-training-and-quantization#table1397054115616)。图片格式的数据为存放测试图片的文件夹，图片格式的输入默认以BGR的三通道彩图读取，读出的数据格式为NCHW，其中N为提供图片的数量。

说明

轻量化工具支持的图片格式包括 ".bmp"，".dib"，".jpeg"，".jpg"，".jpe"，".png"，".webp"，".pbm"，".pgm"，".ppm"，".tiff"，".tif"，".BMP"，".DIB"，".JPEG"，".JPG"，".JPE"，".PNG"，".WEBP"，".PBM"，".PGM"，".PPM"，".TIFF"，".TIF"。

bin格式的输入数据支持两种定义方式，分别适用于任意维度的输入数据和4维的输入数据（推荐开发者使用任意维度的定义方式）。

对于任意维度的输入数据，bin文件需按照以下方式定义，以维度（50, 100, 300）的3维数据为例，读出的数据形状为（50, 100, 300）。

**表1** 任意维度二进制校准集说明
|**文件头/数据**|**地址偏移**|**Type**|**Value**|**Description**|
|:--|:--|:--|:--|:--|
|文件头（共20字节）|0000|32bit int|610|Magic number<br><br>当magic number = 610，用来校验文件的合法性。|
|0004|32bit int|3|Input data rank|
|0008|32bit int|50|Input dimension 1|
|0012|32bit int|100|Input dimension 2|
|0016|32bit int|300|Input dimension 3|
|数据|…|Float32|...|数据数量等于50*100*300|

对于4维的输入数据，bin文件可以按照[任意维度二进制校准集说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-no-training-and-quantization#table1397054115616)定义，也可以按照[4维二进制校准集说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-no-training-and-quantization#table1960771718465)， 以维度（50, 3, 28, 28）的4维数据为例，读出的数据形状为（50, 3, 28, 28）。

**表2** 4维二进制校准集说明
|**文件头****/数据**|**地址偏移**|**Type**|**Value**|**Description**|
|:--|:--|:--|:--|:--|
|文件头（共20字节）|0000|32bit int|510|Magic number<br><br>当magic number = 510，用来校验文件的合法性|
|0004|32bit int|50|Input num|
|0008|32bit int|3|Input channels|
|0012|32bit int|28|Input height|
|0016|32bit int|28|Input width|
|数据|…|Float32|...|数据数量等于50*3*28*28|

说明

轻量化工具已提供脚本支撑bin格式文件的转换，详见[Tools下载](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-preparations#section152959341125)的tools_dopt/dopt_tf_py3/demo/quant8-8/notrain/bin_data_preprocessing.py。

### 填写config.prototxt文件

config.prototxt参数说明如下表所示。其中BINARY模式不进行预处理，IMAGE模式根据开发者给出的均值方差进行预处理。

|参数名称|参数描述|是否必填|
|:--|:--|:--|
|strategy|优化策略，当前对所有框架都只支持Quant_INT8-8。|否，默认策略为Quant_INT8-8|
|device|使用GPU还是CPU进行量化。<br><br>- USE_GPU：GPU模式<br>- USE_CPU：CPU模式|否，默认CPU模式|
|exclude_op|支持两种方式。<br><br>- 使用一个exclude_op，exclude_op包含多个op_name，用分号隔开。<br>- 使用多个exclude_op，每个exclude_op包含一个op_name 。<br><br>两种方式可混合使用，当所给op_name不在模型内时，会报错。<br><br>说明<br><br>ONNX的exclude_op应该为weight name。|否|
|preprocess_parameter|校准数据配置文件路径。|是|

preprocess_parameter包含的子参数说明如下表所示，对于模型有多输入的情况，每一个输入都需要配置一份preprocess_parameter。

|参数名称|参数描述|是否必填|
|:--|:--|:--|
|input_type|使用二进制文件输入还是图片格式输入。<br><br>- BINARY：使用二进制输入<br>- IMAGE：使用图片格式输入|否，默认IMAGE格式|
|image_format|图片格式，仅在“IMAGE”模式下生效。<br><br>- BGR：使用BGR图片格式输入<br>- RGB：使用RGB图片格式输入|否，默认采用BGR|
|mean_value|图片预处理的均值参数，仅“IMAGE”模式下生效。<br><br>类型为float的数值，范围为0.0-255.0。<br><br>mean_value个数必须和输入的C维度相等。|否，默认输入C维度为0.0|
|standard_deviation|图片预处理使用的标准差，仅“IMAGE”模式下生效。<br><br>类型为float的数值，需要>=0.0。|否，默认为0.0|
|input_file_path|输入校准集的绝对路径，bin文件路径或存有图片的文件夹。<br><br>例如：“/path/to/user/data”。|是|

说明

- 当使用“IMAGE”模式输入时，工具链会对图片做如下处理：image = (image - mean_value) / standard_deviation。
- 当使用“BINARY”模式时，工具链不会对输入数据做任何处理，即image_format、mean_value、standard_deviation三个参数无效。

配置文件的配置示例如下所示。

- BINARY模式输入
    
    1. strategy: "Quant_INT8-8"
    2. device: USE_GPU
    3. // 多输入场景提供不同的bin文件
    4. preprocess_parameter:
    5. {  
    6.     input_type: BINARY
    7.     input_file_path: "path/to/user/bin/caffe_inception_calibrationset1.bin"
    8. }
    9. preprocess_parameter:
    10. {  
    11.     input_type: BINARY
    12.     input_file_path: "path/to/user/bin/caffe_inception_calibrationset2.bin"
    13. }
    14. // ...
    15. exclude_op:  "conv1"
    16. exclude_op:  "conv2;conv3"
    

- IMAGE模式输入
    
    1. strategy: "Quant_INT8-8"
    2. device: USE_GPU
    3. // 多输入场景提供不同的图片路径
    4. preprocess_parameter:
    5. {
    6.     input_type: IMAGE
    7.     image_format: BGR
    8.     mean_value: 104.0
    9.     mean_value: 113.0
    10.     mean_value: 123.0
    11.     standard_deviation: 0.5
    12.     input_file_path: "path/to/user/images1/"
    13. }
    14. preprocess_parameter:
    15. {
    16.     input_type: IMAGE
    17.     image_format: BGR
    18.     mean_value: 104.0
    19.     mean_value: 113.0
    20.     mean_value: 123.0
    21.     standard_deviation: 0.5
    22.     input_file_path: "path/to/user/images2/"
    23. }
    24. // ...
    25. exclude_op:  "conv1"
    26. exclude_op:  "conv2;conv3"
    

## TensorFlow模型无训练量化

### 环境准备

该功能支持TensorFlow 2.8 CPU或GPU版本。如没有该版本环境，需要自行安装；如已有，则不需要配置环境。

TensorFlow2.8安装方法如下:

1. pip3 install tensorflow-gpu==2.8

### 模型量化

运行“python3 tools_dopt/dopt_tf_py3/dopt_so.py”。请在python3环境下运行该命令。

运行该脚本对TensorFlow模型进行无训练量化的参数如下所示。

说明

- 路径：支持大小写字母、数字、下划线。
- 文件名：支持大小写字母、数字、下划线和点(.)。

|**参数名称**|**是否必填**|**参数描述**|
|:--|:--|:--|
|-m, --mode|是|运行模式。<br><br>- 0：无训练模式。（当前只支持0）|
|--framework|是|深度学习框架类型。<br><br>- 3：TensorFlow<br>- 5：PyTorch或ONNX|
|--model|是|原始模型文件路径，支持pb模型。|
|--cal_conf|是|校准方式量化配置文件路径。<br><br>量化配置文件说明请参见[填写config.prototxt文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-no-training-and-quantization#section2065711363111)。|
|--output|是|存放量化完成后的模型文件绝对路径，例如“/path/to/out/resnet18.pb”。|
|--input_format|是|输入格式数据， NHWC或NCHW。<br><br>当开发者选择IMAGE格式或文件头为510的bin文件作为输入数据，并选择输入格式数据为NHWC时，工具会自动调整通道顺序；当选择文件头为610的bin文件作为输入数据时不会调整通道顺序。|
|--input_shape|是|输入数据的shape。<br><br>例如：“input_name1: n1, c1，h1, w1; input_name2: n2, c2, h2,w2”。input_name必须是转换前的网络模型中的节点名称。多输入input_shape之间由';'进行分割。input_shape中指定各维度输入数据值需与网络模型中指定的输入节点所需形状保持一致。例如：假设转换前网络模型指定输入节点为input_shape_network: none, 224, 224, 3; input_shape第2、3、4维度输入数值必须为224,224,3，否则尺寸不匹配。假设转换前网络模型指定输入节点为input_shape_network: 1, 224, 224, 3；则input_shape各维度输入数据均不可变。|
|--out_nodes|是|指定输出节点。<br><br>例如：“node_name1; node_name2; node_name3”。node_name必须是模型转换前的网络模型中的节点名称。|
|--compress_conf|是|模型文件转为二进制格式文件的路径。<br><br>例如：“param_file”。该文件为轻量化配置，在使用OMG离线模型转换时将被作为参数compress_conf的输入。|
|--device_idx|否|GPU或CPU的设备号，默认为0。|

运行量化脚本后，会输出开发者--output传入同名的pb，以及--compress_conf传入同名的量化配置文件。例如：开发者--output输入quantmodel.pb，--compress_conf输入param，最终会输出quantmodel.pb和param。

## PyTorch模型无训练量化

### 环境准备

该功能现仅支持PyTorch1.11版本。使用如下命令安装依赖：

1. pip3 install torch==1.11

### 模型量化

运行“python3 tools_dopt/dopt_pytorch_py3/dopt_so.py”。运行该脚本对PyTorch模型进行无训练量化的参数如下所示。

说明

路径：支持大小写字母、数字、下划线。

文件名：支持大小写字母、数字、下划线和点(.)。

|参数名称|是否必填|参数描述|
|:--|:--|:--|
|-m, --mode|是|运行模式。<br><br>- 0：无训练模式。（当前只支持0）|
|--framework|是|深度学习框架类型。<br><br>- 3：TensorFlow<br>- 5：PyTorch或ONNX|
|--model|是|PyTorch模型定义文件路径。|
|--weight|是|PyTorch模型参数pth文件路径。|
|--cal_conf|是|校准方式量化配置文件路径。<br><br>量化配置文件说明请参见[填写config.prototxt文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-no-training-and-quantization#section2065711363111)。|
|--output|是|存放量化完成后的模型文件绝对路径，例如“/path_to_out/resnet.pt”。|
|--input_shape|是|输入数据的shape。例如：“input_name1: n1, c1, h1, w1; input_name2: n2, c2, h2, w2”。input_name是模型定义中，forward()函数的入参名称。input_shape中指定的各输入数据的维度信息，用于转换PyTorch模型，需与实际模型的输入节点形状保持一致。|
|--compress_conf|是|模型文件转为二进制格式文件的路径。<br><br>例如：“param_file”。该文件为轻量化配置，在使用OMG离线模型转换时将被作为参数compress_conf的输入。|
|--device_idx|否|GPU或CPU的设备号，默认为0。|
|--input_format|PyTorch框架无需配置该参数|输入格式数据，NHWC或NCHW。<br><br>当开发者选择IMAGE格式或文件头为510的bin文件作为输入数据，并选择输入格式数据为NHWC时，工具会自动调整通道顺序；当选择文件头为610的bin文件作为输入数据时不会调整通道顺序。|
|--out_nodes|PyTorch框架无需配置该参数|指定输出节点。<br><br>例如：“node_name1; node_name2; node_name3”。node_name必须是模型转换前的网络模型中的节点名称。|

运行量化脚本后，会输出开发者--output传入同名的pt，以及--compress_conf传入同名的量化配置文件。例如：开发者--output输入quantmodel.pt，--compress_conf输入param，最终会输出quantmodel.pt和param。

## ONNX模型无训练量化

### 环境准备

该功能支持ONNX Runtime 1.15 CPU版本和ONNX环境。如没有该版本环境，需要自行安装；如已有，则不需要配置环境。

ONNX安装方法如下:

1. pip3 install onnx==1.14

其他依赖：

1. pip3 install protobuf==3.20.0

ONNX Runtime CPU版本安装方法如下:

1. pip3 install onnxruntime==1.15

### 模型量化

运行“python3 tools_dopt/dopt_onnx_py3/dopt_so.py”。请在python3环境下运行该命令。

运行该脚本对ONNX模型进行无训练量化的参数如下所示。

说明

- 路径：支持大小写字母、数字、下划线。
- 文件名：支持大小写字母、数字、下划线和点(.)。

|**参数名称**|**是否必填**|**参数描述**|
|:--|:--|:--|
|-m, --mode|是|运行模式。<br><br>- 0：无训练模式。（当前只支持0）|
|--framework|是|深度学习框架类型。<br><br>- 3：TensorFlow<br>- 5：PyTorch或ONNX|
|--weight|ONNX框架无需配置该参数|权值文件路径。|
|--model|是|原始模型文件路径，支持ONNX模型。|
|--cal_conf|是|校准方式量化配置文件路径。<br><br>量化配置文件说明请参见[填写config.prototxt文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-no-training-and-quantization#section2065711363111)。|
|--output|是|存放量化完成后的模型文件绝对路径，例如“/path_to_out/resnet.onnx”。|
|--input_format|是|输入格式数据， NHWC或NCHW。<br><br>当开发者选择IMAGE格式或文件头为510的bin文件作为输入数据，并选择输入格式数据为NHWC时，工具会自动调整通道顺序；当选择文件头为610的bin文件作为输入数据时不会调整通道顺序。|
|--input_shape|是|输入数据的shape。<br><br>例如：“input_name1: n1, c1，h1, w1; input_name2: n2, c2, h2,w2”。input_name必须是转换前的网络模型中的节点名称。多输入input_shape之间由';'进行分割。input_shape中指定各维度输入数据值需与网络模型中指定的输入节点所需形状保持一致。例如：假设转换前网络模型指定输入节点为input_shape_network: none, 224, 224, 3; input_shape第2、3、4维度输入数值必须为224,224,3，否则尺寸不匹配。假设转换前网络模型指定输入节点为input_shape_network: 1, 224, 224, 3；则input_shape各维度输入数据均不可变。|
|--out_nodes|是|指定输出节点。<br><br>例如：“node_name1; node_name2; node_name3”。node_name必须是模型转换前的网络模型中的节点名称。|
|--compress_conf|是|模型文件转为二进制格式文件的路径。<br><br>例如：“param_file”。该文件为轻量化配置，在使用OMG离线模型转换时将被作为参数compress_conf的输入。|
|--device_idx|ONNX框架无需配置该参数|GPU或CPU的设备号，默认为0。|

运行量化脚本后，会输出开发者--output传入同名的ONNX，以及--compress_conf传入同名的量化配置文件。例如：开发者--output输入quantmodel.onnx，--compress_conf输入param，最终会输出quantmodel.onnx和param。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-lightweight-tool-overview "概述")
# 插件式量化

更新时间: 2025-12-16 16:28

## 依赖环境准备

插件式量化运行环境依赖开发者本身的训练工程环境，目前轻量化工具支持TensorFlow和PyTorch两种框架的插件式量化。

说明

插件式量化环境配置完成后，可同时支持无训练和重训练量化。

## TensorFlow插件式量化

TensorFlow模型优化训练如下步骤：

前提条件：准备模型训练数据集、全精度的基线ckpt文件。

1. 准备TensorFlow环境（[准备TensorFlow环境](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-plugin-based-quantization#section103814481178)）。
2. 调用API生成模型优化策略模板（[获取量化配置模板](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-plugin-based-quantization#section7308624487)）。
3. 优化策略文件配置（[优化策略配置](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-plugin-based-quantization#section1035414781018)）。
4. 训练模型（[训练或校准模型](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-plugin-based-quantization#section184938114114)）。（重训练模式对量化模型训练，无训练模式对量化模型进行校准）
5. 提取模型及量化参数（[转换模型](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-plugin-based-quantization#section11929116113114)）。

### 准备TensorFlow环境

准备Linux环境，使用轻量化工具插件式量化功能，开发者需要准备如下依赖。

- python 3.10版本
- 依赖python库说明：
    
    1. pip3 install ruamel_yaml
    2. pip3 install pathlib
    3. pip3 install protobuf==3.20.0
    4. pip3 install opencv-python
    
- 轻量化工具当前支持tensorflow-gpu 2.8.0版本，使用如下的命令安装：
    
    1. pip3 install tensorflow-gpu==2.8.0
    

### 获取量化配置模板

将解压出的DDK中的dopt_tf_py3添加到python环境变量中：

1. import sys
2. sys.path.append(".../dopt_tf_py3") ## 其中路径为绝对路径

对需要进行量化的PyTorch模型，调用API生成量化配置json文件。

1. from dopt.dopt_tf.opt_main import generate_config_file
2. generate_config_file(sess, dst_path="./config_gen.json")

|**参数名称**|**是否必填**|**参数描述**|
|:--|:--|:--|
|sess|是|sess中加载原始的TensorFlow浮点模型。|
|dst_path|是|dst_path为生成配置json文件路径。|

生成的配置样式如下。

1. {
2.     "quant_strategy_for op 'Conv2D'": [
3.         "Quant_INT8-8"
4.     ],
5.     "quant_strategy_for op 'MatMul'": [
6.         "Quant_INT8-8"
7.     ],
8.     "layer_strategy": {
9.         "model/resnet_model/conv2d/Conv2D": {
10.             "op_type": "Conv2D",
11.             "quant_strategy": "float"
12.         },
13.         "model/resnet_model/conv2d_1/Conv2D": {
14.             "op_type": "Conv2D",
15.             "quant_strategy": "float"
16.         },
17.         // ...
18.     }
19. }

### 优化策略配置

基于上述生成的配置文件，确定要量化的层，并将对应的quant_strategy由float调整为对应的量化策略，例如Quant_INT8-8。

1. {
2.     "quant_strategy_for op 'Conv2D'": [
3.         "Quant_INT8-8"
4.     ],
5.     "quant_strategy_for op 'MatMul'": [
6.         "Quant_INT8-8"
7.     ],
8.     "layer_strategy": {
9.         "model/resnet_model/conv2d/Conv2D": {
10.             "op_type": "Conv2D",
11.             "quant_strategy": "Quant_INT8-8"
12.         },
13.         "model/resnet_model/conv2d_1/Conv2D": {
14.             "op_type": "Conv2D",
15.             "quant_strategy": "Quant_INT8-8"
16.         },
17.         // ...
18.     }
19. }

说明

- _layer_strategy_中包含的为当前版本所支持的所有可量化层，开发者不应额外添加层。
- 开发者需要根据_op_type_选择支持的量化策略，若配置_op_type_为不支持的量化策略，那么在后续量化环节会报错。

### 训练模型

开发者需要进行插件式量化时，将解压出的DDK中的dopt_tf_py3文件路径添加到python环境变量中：

1. import sys
2. sys.path.append(".../dopt_tf_py3") ## 其中路径为绝对路径

3. from dopt.dopt_tf.opt_main import optimize_model

optimize_model接口在_session_中构造模型，并根据配置的量化策略json文件将模型进行量化。

- 配置标志位_is_train_flag_，表示模型当前的量化参数是否随训练更新。
- 配置标志位_quant_flag_，表示模型是否走量化通路。
    
    1. with tf.Session(config=config) as sess:
    2.     ## 待量化的tf模型graph，仅构建拓扑图，不可加载权重
    3.     build_tf_model()
    4.     quant_flag = tf.placeholder(tf.int32)
    5.     is_train_flag = tf.placeholder(tf.bool, name='is_train')
    6.     ## 模型量化，自动在 tf.get_default_graph()上进行改图操作
    7.     optimize_model( 
    8.         sess,
    9.         config_file,
    10.         is_train_flag,
    11.         quant_flag
    12.     )
    
    13.     ## 调用完optimize_model之后，加载模型权重
    14.     saver = tf.Saver()
    15.     saver.restore(ckpt)
    16.     tf.global_variables_initializer().run()
    

- build_tf_model：由开发者定义，在session中创建要量化的模型图。
- quant_flag：tf.int32类型，其中为0表示走浮点通路（不做量化），为1（或其他正值）表示走量化通路，与is_train_flag共同作用。
- is_train_flag：在quant_flag > 0时，表示量化参数是否随训练更新。
    
    |**参数名称**|**是否必填**|**参数描述**|
    |:--|:--|:--|
    |sess|是|_sess_中加载原始的TensorFlow浮点模型。|
    |config_file|是|开发者手动配置完成量化层的json文件路径。|
    |is_train_flag|是|模型当前的量化参数是否随训练更新。|
    |quant_flag|是|模型是否走量化通路。|
    

正常训练模型，检查损失函数loss，效果达标后，可停止训练，需保存对应的ckpt数据。

1. ## ckpt save 
2. saver = tf.train.Saver() 
3. saver.save(sess, train_ckpt_path)

开发者需要进行无训练量化时，可以使用set_calibrate_state API设置为无训练模式。

1. from dopt.dopt_tf.opt_main import set_calibrate_state 

2. calibration_mode = True
3. set_calibrate_state(sess, calibration_mode ) 

|**参数名称**|**是否必填**|**参数描述**|
|:--|:--|:--|
|sess|是|量化后的TensorFlow Session。|
|calibration_mode|是|bool变量，开发者是否开启无训练（校准）模式。<br><br>- True：开启无训练（校准）模式<br>- False：关闭无训练（校准）模式|

完成无训练模式的设置之后，使用量化后的“sess”对校准集进行前向推理就可进行无训练量化。

### 转换模型

完成模型量化以及重训练或者校准集前向推理后即可对量化参数进行收集，将session中的量化参数提取至量化文件中并生成对应的PB文件。

将解压出的DDK中的dopt_tf_py3文件路径添加到python环境变量中：

1. import sys
2. sys.path.append(".../dopt_tf_py3") ## 其中路径为绝对路径

3. from dopt.dopt_tf.opt_main import generate_final_model

初始化原始浮点模型，加载量化训练的ckpt，利用提供的接口提取参数。

1. with tf.Session(config=config) as sess:
2.     build_tf_model()
3.         generate_final_model(
4.         sess,
5.         config_file         = FLAGS.config_file,
6.         output_name_list    = output_name_list,
7.         ckpt_file           = train_ckpt_path,
8.         output_dir          = output_dir
9.     )

build_tf_model：由开发者定义，在session中创建要量化的模型图。

|**参数名称**|**是否必填**|**参数描述**|
|:--|:--|:--|
|sess|是|_sess_中加载原始的TensorFlow浮点模型。|
|config_file|是|开发者手动配置完成量化层的json文件路径与optimize_model处理时的配置保持一致。|
|output_name_list|是|pb模型的最后一层输出节点名，数据类型为list。|
|ckpt_file|是|量化重训练或校准保存的ckpt数据。|
|output_dir|否|提取的pb和量化参数保存路径，需确保该路径存在，如果不填写模型在当前路径下保存。|

## PyTorch插件式量化

PyTorch模型优化训练如下步骤：

前提条件：准备模型训练数据集、全精度的基线参数pth文件。

1. 准备PyTorch环境（[准备PyTorch环境](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-plugin-based-quantization#section461318612307)）。
2. 调用API生成量化配置json文件（[生成量化配置json文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-plugin-based-quantization#section1374313714435)）。
3. 修改策略文件配置（[优化策略配置](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-plugin-based-quantization#section16522384430)）。
4. 调用API训练量化模型（[训练或校准模型](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-plugin-based-quantization#section767733515413)）。
5. 调用API生成量化ONNX模型及量化参数文件（[生成量化模型](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-plugin-based-quantization#section1567210444438)）。

### 准备PyTorch环境

使用轻量化工具插件式量化功能，开发者需要准备如下依赖。

- python 3.10版本
- 依赖python库说明：
    
    1. pip3 install ruamel_yaml
    2. pip3 install pathlib
    3. pip3 install protobuf>=3.20.0
    4. pip3 install onnx==1.14.0
    
- 轻量化工具当前仅支持PyTorch 1.11版本。使用如下的命令安装：
    
    1. pip3 install torch==1.11.0
    

说明

- 路径：支持大小写字母、数字、下划线。
- 文件名：支持大小写字母、数字、下划线和点(.)。

### 生成量化配置json文件

将解压出的DDK中的dopt_pytorch_py3文件路径添加到python环境变量中：

1. import sys
2. sys.path.append(".../dopt_pytorch_py3") ## 其中路径为绝对路径

3. from dopt.dopt_torch.opt_main import generate_config_file

对需要进行量化的PyTorch模型，调用API生成量化配置json文件。

1. generate_config_file(model, input_shape, dst_path="./config_gen.json") # model：torch.nn.Module， input_shape : "input1:input1.shape;input2:input2.shape"

|**参数名称**|**是否必填**|**参数描述**|
|:--|:--|:--|
|model|是|torch.nn.Module，未经过torch.nn.parallel.DistributedDataParallel等分布式API封装的模型。|
|input_shape|是|最终部署模型的shape，而非训练阶段的训练数据shape。|
|dst_path|是|生成配置json文件路径。|

### 优化策略配置

生成的配置文件如下：

1. {
2.     "quant_strategy_for op '<class 'torch.nn.modules.conv.Conv2d'>'": [
3.         "Quant_INT8-8"
4.     ],
5.     "quant_strategy_for op '<class 'torch.nn.modules.linear.Linear'>'": [
6.         "Quant_INT8-8"
7.     ],
8.     "input_shape": "x:1,3,224,224",
9.     "layer_strategy": {
10.         "conv1/Conv2D": {
11.             "op_type": "<class 'torch.nn.modules.conv.Conv2d'>",
12.             "quant_strategy": "float"
13.         },
14.         "conv2/Conv2D": {
15.             "op_type": "<class 'torch.nn.modules.conv.Conv2d'>",
16.             "quant_strategy": "float"
17.         },
18.         // ...
19.     }
20. }

开发者可根据需要的量化修改配置。

- 支持逐层配置量化策略，默认为"float"。
- 支持的量化策略Quant_INT8-8为8a8w。

以上述json为例，开发者可修改成：

1. {
2.     "quant_strategy_for op '<class 'torch.nn.modules.conv.Conv2d'>'": [
3.         "Quant_INT8-8"
4.     ],
5.     "quant_strategy_for op '<class 'torch.nn.modules.linear.Linear'>'": [
6.         "Quant_INT8-8"
7.     ],
8.     "input_shape": "x:1,3,224,224",
9.     "layer_strategy": {
10.         "conv1/Conv2D": {
11.             "op_type": "<class 'torch.nn.modules.conv.Conv2d'>",
12.             "quant_strategy": "Quant_INT8-8"，
13.         },
14.         "conv2/Conv2D": {
15.             "op_type": "<class 'torch.nn.modules.conv.Conv2d'>",
16.             "//": "可以逐层配置量化，不量化的层保持浮点",
17.             "quant_strategy": "float"
18.         },
19.         // ...
20.     }
21. }

- layer_strategy中包含的为当前版本所支持的所有可量化层，开发者不应额外添加层。
- 开发者需要根据_op_type_选择支持的量化策略，若配置_op_type_为不支持的量化策略，那么在后续量化环节会报错。
- json文件中，除了input_shape和layer_strategy两个key之外，其余内容为提示作用，不会进行解析。

### 训练模型

将解压出的DDK中的dopt_pytorch_py3文件路径添加到python环境变量中：

1. import sys
2. sys.path.append(".../dopt_pytorch_py3") ## 其中路径为绝对路径
3. from dopt.dopt_torch.opt_main import optimize_model

开发者需在PyTorch模型定义阶段调用API进行模型的量化操作。

1. quant_model = optimize_model(model, config_path) ## config_path为上一步中修改后的json文件绝对路径

|**参数名称**|**是否必填**|**参数描述**|
|:--|:--|:--|
|model|是|torch.nn.Module，未经过torch.nn.parallel.DistributedDataParallel等分布式API封装的模型。|
|config_path|是|最终部署模型的shape，而非训练阶段的训练数据shape。|

开发者可根据需要调用API，获取量化相关的损失函数，加入到优化训练中（可选项，简单任务不推荐使用）。

1. from dopt.dopt_torch.opt_main import get_quant_loss
2. quant_loss = get_quant_loss(quant_model)
3. total_loss = loss + quant_weight * quant_loss ## quant_weight为量化损失的超参数

|**参数名称**|**是否必填**|**参数描述**|
|:--|:--|:--|
|quant_model|是|经过optimize_model API处理后量化模型。|

对量化训练完成的模型需要保存其对应的checkpoint。

1. torch.save(quant_model.state_dict(),"quant.pth")

如果开发者无需进行重训练量化可以只进行无训练量化，开启无训练只需调用set_calibrate_state API

1. from dopt.dopt_torch.opt_main import set_calibrate_state 
2. calibrate_mode = True
3. set_calibrate_state(quant_model, calibrate_mode)

|**参数名称**|**是否必填**|**参数描述**|
|:--|:--|:--|
|quant_model|是|量化后的PyTorch模型。|
|calibration_mode|是|bool变量，开发者是否开启无训练（校准）模式。<br><br>- True：开启无训练（校准）模式<br>- False：关闭无训练（校准）模式|

完成无训练模式的设置之后，使用量化后的quant_model对校准集进行前向推理就可进行无训练量化。

说明

- 调用optimize_model函数的入参model需要是未经过torch.nn.parallel.DistributedDataParallel等分布式API封装的模型，且优化器optimizer需要针对quant_model而非原始浮点模型。
- 量化损失非必须添加，quant_loss需要根据实际量化损失的大小和原始损失的大小进行超参数的调节，一般量化损失函数与原始损失函数比例为1:20，如对优化方向产生较大影响，建议减少量化损失的占比。

### 生成量化模型

将解压出的DDK中的dopt_pytorch_py3文件路径添加到python环境变量中：

1. import sys
2. sys.path.append(".../dopt_pytorch_py3") ## 其中路径为绝对路径

3. from dopt.dopt_torch.opt_main import generate_final_model

训练完成后，使用对应API生成最终模型：

1. generate_final_model(
2.     model,              ## 浮点模型
3.     config_file,         ## 量化配置json文件
4.     pth_file = "quant.pth",    ## 量化后 pth 文件
5.     output_dir = "./"   ## 量化para与PyTorch的生成文件夹
6. )

|**参数名称**|**是否必填**|**参数描述**|
|:--|:--|:--|
|model|是|浮点模型。|
|config_file|是|量化配置json文件路径，与optimize_model api的处理的config_path保持一致。|
|pth_file|是|量化训练的权重文件。|
|output_dir|是|PyTorch和量化参数保存路径。请确保该路径存在，如果不填写，模型将默认保存到当前路径下。|

说明

- 调用generate_final_model函数的入参model须为重新构建的浮点模型。
- 生成的PyTorch模型中不带有量化参数，但是会做部分图融合以及伪量化处理。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-no-training-and-quantization "无训练量化")
# 大语言模型低位量化

更新时间: 2025-12-16 16:28

## 简介

本工具提供大语言模型（Large Language Model，以下简称LLM）的4bit低位量化能力，采用标准的三段式量化流程：权重量化、激活量化和量化参数提取。三段式量化流程说明如下表所示。

**表1** 大语言模型4bit低位量化三阶段流程
|阶段|输入|输出|
|:--|:--|:--|
|阶段一（权重量化）|- 开发者提供<br><br>- JSON数据集（text字段作prompt）<br><br>- HuggingFace模型路径（开发者浮点模型）<br><br>- 量化配置及执行文件<br><br>- config.yaml<br><br>- demo.py<br><br>- run.sh|- dopt_config.json：开发者需完成该文件的量化策略配置后，重新执行此阶段<br><br>- trained_quant_weight.pth：权重量化参数<br><br>说明<br><br>开发者需根据阶段一生成的dopt_config.json文件手动进行量化策略配置后，再次执行该阶段。|
|阶段二（激活量化）|trained.pth：用于阶段三加载或量化仿真验证|
|阶段三（量化参数提取）|- fake_quant_weight.pth：用于ONNX模型导出<br>- quant_params_file：权重及激活量化参数|

## 量化前准备工作

- HuggingFace浮点模型
- JSON格式数据集，使用“text”字段作为prompt关键字
- 量化配置文件[config.yaml](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-large-language-model#section19562154641017)
- [demo.py](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-large-language-model#section158091338101113)及[run.sh](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-large-language-model#section11700841124819)执行脚本

说明

- LLM在量化过程中使用AutoModelForCausalLM以及AutoTokenizer加载，所以开发者的HuggingFace浮点模型需要满足该加载方式约束。
- run.sh执行脚本环境须与开发者推理或者训练环境保持一致，否则模型加载失败。

### config.yaml示例

config.yaml用于模型量化配置，开发者可根据实际需要进行配置。以下示例可供参考，主要参数说明请参见[config.yaml配置参数说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-large-language-model#section760161441112)。

1. kd:
2.   enable: True
3.   loss: mse
4.   micro_batch_size: 2
5.   gradient_accumulation_steps: 4
6.   weight_decay: 0.0
7.   warmup_steps: 10
8.   num_epochs: 3
9.   learning_rate: !!float 1e-4
10.   eval_step: 1
11.   logging_step: 50
12.   lr_scheduler_type: cosine
13.   trainable_keys:
14.     - quant_alpha
15.     - norm
16.   no_split_module_classes:
17.     - Qwen2DecoderLayer
18.     - GlmDecoderLayer
19.     - LlamaDecoderLayer
20.     - HunYuanDecoderLayer
21. dataset:
22.   train_files: dataset.json
23.   train_samples: 1024
24.   ptq_samples: 1024
25. extra_training_config:
26.   fp16: True
27. cutoff_len: 128
28. num_samples: 256
29. lut_mode: False
30. embedding_in_omc: False

### config.yaml配置参数说明

以下为config.yaml文件的关键配置参数，具体说明如下表所示。

|参数|   |默认取值|说明|
|:--|:--|:--|:--|
|kd：量化蒸馏相关|enable|True|- True：使用蒸馏量化策略<br>- false：使用无训练量化策略|
|loss|mse|量化蒸馏损失函数，仅支持mse|
|micro_batch_size|2|单卡batch|
|gradient_accumulation_steps|4|梯度累计步数|
|weight_decay|0.0|权重衰减系数|
|warmup_steps|10|预热步数|
|num_epochs|3|训练迭代次数|
|learning_rate|1e-4|学习率|
|logging_step|50|log打印步数|
|lr_scheduler_type|cosine|学习率调整策略。|
|trainable_keys|-|配置可训练参数。<br><br>- quant_alpha：量化层的训练参数<br>- norm：layer_norm层的可训练参数|
|no_split_module_classes|-|多卡切分时，选择切分粒度。<br><br>- Qwen2DecoderLayer<br>- GlmDecoderLayer<br>- LlamaDecoderLayer<br>- HunYuanDecoderLayer|
|dataset|train_files|-|JSON格式训练数据文件，dataset.json|
|train_samples|1024|训练集样本数，缺省默认全量数据集|
|ptq_samples|1024|PTQ优化样本数，缺省默认全量数据集|
|extra_training_config|fp16|训练数据类型，仅支持fp16|
|cutoff_len|128|样本序列长度|
|num_samples|256|激活量化校准样本数|
|lut_mode|False|- True：导出参数使用lut表<br>- False：导出参数不使用lut表|
|embedding_in_omc|False|- True：导出embedding的量化参数到量化文件<br>- False：单独保存为bin文件|

### demo.py示例

1. #!/usr/bin/env python
2. # -*- coding: utf-8 -*-
3. # Copyright Huawei Technologies Co., Ltd. 2010-2024. All rights reserved
4. import os
5. import sys
6. import argparse
7. from dopt.log import Logger
8. from dopt.dopt_llm.opt_main import parse_args, generate_quant_config, llm_quant_pipline
9. if __name__ == '__main__':
10.     args = parse_args()
11.     ### step1 generate dopt_quant_config
12.     if not os.path.exists(args.dopt_config):
13.         generate_quant_config(args.model_path, args.dopt_config)
14.         Logger.info(f'generate plugin quang config please set quant strategy firstly')
15.         exit()
16.     optimize_info = {
17.         "model_path" :  args.model_path,
18.         "config_yaml":  args.optimize_config,
19.         "dopt_config":  args.dopt_config,
20.         "output_dir" :  args.output_dir,
21.         "hf_type_save": args.hf_type_save,
22.         "quant_stage" : args.quant_stage,
23.         "group_size" :  args.group_size,
24.         "act_bits":     args.act_bits,
25.         "w_bits":       args.w_bits,
26.     }
27.     ### step2 run llm model Quantification optimization process
28.     llm_quant_pipline(**optimize_info)

## 执行三段式量化

按以下步骤执行run.sh文件，stagex为传入参数，具体可参考[run.sh示例](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-large-language-model#section11317363241)。

1. 权重量化。
    
    1. 选配量化策略。
        
        生成插件式量化配置文件[dopt_config.json](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-large-language-model#section15113659191318)。
        
        1. /*bash run.sh stage1*/ 
        
        量化策略可选配置为：
        
        2. /*
        3. Quant_act_weight_eco   decode层策略
        4. Quant_lm_head          lm_head层策略
        5. Quant_Embed_MinMax     embedding层策略
        6. */
        
    2. 进行权重量化。
        
        1.  /*bash run.sh stage1*/
        
    
2. 激活量化。
    
    1. /*bash run.sh stage2*/
    
3. 提取量化参数。
    
    1. /*bash run.sh stage3*/
    

### run.sh示例

1. #!/bin/bash
2. set -e
3. export WANDB_DISABLED=true
4. export HF_DATASETS_OFFLINE=0
5. export PYTHONPATH=../../dopt_tool_chain:$PYTHONPATH
6. # 设置为cuda或npu模式
7. # cuda模式
8. export DEVICE=cuda
9. export CUDA_VISIBLE_DEVICES=1
10. # npu模式
11. # export DEVICE=npu
12. # export ASCEND_RT_VISIBLE_DEVICES=2,3
13. ROOT=''
14. testcase='demo_case'
15. RUN_FILE=${ROOT}/demo.py
16. output_dir=${ROOT}/${testcase}/train_output
17. mkdir -p ${output_dir}
18. model_path=model_path_or_name
19. dopt_config=./${testcase}/dopt_config.json
20. quant_stage=$1
21. group_size=128
22. act_bits=16
23. w_bits=4
24. python -u \
25.     ${RUN_FILE} --model-path $model_path \
26.     --dopt-config $dopt_config \
27.     --optimize-config ${ROOT}/config.yaml \
28.     --quant-stage $quant_stage \
29.     --group-size $group_size \
30.     --act-bits $act_bits \
31.     --w-bits $w_bits \
32.     --output-dir ${output_dir} 2>&1 | tee ${output_dir}/logs.log

### dopt_config.json量化配置文件说明

工具支持开发者插件式自定义LLM量化规格：

- 逐层权重量化位宽(bit)和分组大小(group_size)。
- 逐层激活量化位宽(bit)。
- 量化策略：decoder层使用"Quant_act_weight_eco"，lm_head层使用"Quant_lm_head"，embedding层使用"Quant_Embed_MinMax"。

1. {
2.      "layer_strategy": {
3.          "model.layers.0.self_attn.q_proj": {
4.              "type": "<class 'torch.nn.modules.linear.Linear'>",
5.              "quant_strategy": "Quant_act_weight_eco",
6.              "weight":{
7.                  "bit": 4,
8.                  "group_size": 64
9.              }
10.              "input":{
11.                  "bit": 16
12.              }
13.          }
14.          // ...
15.  }

## 量化工具输出件

1. trained.pth            ### 量化仿真可使用该文件
2. fake_quant_weight.pth  ### 导出onnx文件使用该权重
3. trained_quant_weight.pth ### 阶段一的输出，阶段二的输入

## 量化仿真

量化完成后，开发者可进行量化仿真推理，通过对比量化模型与原始浮点模型的输出结果，来评估量化模型精度是否满足要求。量化仿真推理工程可参考[qwen2模型量化仿真推理demo](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-large-language-model#section20831155341215)。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162810.44905416301102213697237228547266:50001231000000:2800:1DFAE030F14170FC6176630CC6F0F68EC659D390165F052E5BA854D54208A928.jpg "点击放大")

### 插件方法

浮点模型完成加载和初始化后，使用以下接口将浮点模型转换为量化模型，模型推理逻辑不变，可参考[qwen2模型量化仿真推理demo](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-large-language-model#section20831155341215)。

1. import sys
2. sys.path.append("path/to/dopt")
3. def get_quanted_model(base_model, dopt_config, quanted_ckpt):
4.      from dopt.dopt_llm.do_opt import(
5.          optimize_model,
6.          set_quant_state,
7.          set_calibrate_state,
8.          set_run_mode,
9.      )
10.      model = optimize_model(base_model, dopt_config)
11.      model.load_state_dict(torch.load(quanted_ckpt, map_location=torch.device('cpu')), strict=True)
12.      set_quant_state(model, weight_state=True, input_state=True)
13.      set_calibrate_state(model, False)    
14.      model.eval()
15.      return model

- base_model：开发者浮点模型（使用transformers库AutoModelForCausalLM类进行加载）。
- dopt_config：量化配置文件。
- quanted_ckpt：量化后pth文件。

### qwen2模型量化仿真推理demo

1. import os
2. import sys
3. import torch
4. from transformers import AutoModelForCausalLM, AutoTokenizer
5. sys.path.append('path/to/dopt')
6. os.environ["CUDA_VISIBLE_DEVICES"] = "0"
7. def get_quanted_model(base_model, dopt_config, quanted_ckpt):
8.     """
9.     加载量化模型核心函数
10.     :param base_model: 原始HF模型对象
11.     :param dopt_config: 量化配置文件路径（dopt_config.json）
12.     :param quanted_ckpt: 量化权重路径（trained.pth）
13.     :return: 量化后的模型
14.     """
15.     from dopt.dopt_llm.do_opt import(
16.         optimize_model,
17.         set_quant_state,
18.         set_calibrate_state,
19.         set_run_mode,
20.     )
21.     # 模型量化优化（根据配置文件应用4bit量化策略）
22.     model = optimize_model(base_model, dopt_config)
23.     # 加载量化权重（强制CPU加载避免显存冲突）
24.     model.load_state_dict(torch.load(quanted_ckpt, map_location=torch.device('cpu')), strict=True)
25.     # 设置量化状态
26.     set_quant_state(model, weight_state=True, input_state=True)  # 启用权重和激活量化
27.     set_calibrate_state(model, False)  # 关闭校准模式
28.     set_run_mode(model, "hardware")   # 设置为硬件推理模式
29.     model.eval()
30.     return model
31. def generate(prompt = "Give me a short introduction to large language model."):
32.     """
33.     量化模型推理函数
34.     :param prompt: 输入文本（默认示例prompt）
35.     :return: 模型生成的响应
36.     """
37.     # 构建Qwen2专用对话模板
38.     messages = [
39.         {"role": "system", "content": "You are Qwen, created by Alibaba Cloud..."},
40.         {"role": "user", "content": prompt}
41.     ]
42.     # 应用模板并tokenize
43.     text = tokenizer.apply_chat_template(
44.         messages,
45.         tokenize=False,
46.         add_generation_prompt=True
47.     )
48.     model_inputs = tokenizer([text], return_tensors="pt").to(model.device)
49.     # 执行生成
50.     generated_ids = model.generate(
51.         **model_inputs,
52.         max_new_tokens=512,  # 控制最大生成长度
53.     )
54.     # 后处理：去除输入部分
55.     generated_ids = [
56.         output_ids[len(input_ids):]
57.         for input_ids, output_ids in zip(model_inputs.input_ids, generated_ids)
58.     ]
59.     return tokenizer.batch_decode(generated_ids, skip_special_tokens=True)[0]
60. if __name__ == '__main__':
61.     # === 1. 加载原始模型 ===
62.     model_name = "path/to/model"  # 需替换为实际模型路径
63.     model = AutoModelForCausalLM.from_pretrained(
64.         model_name,
65.         torch_dtype=torch.float16,  # 半精度加载
66.         device_map="auto"           # 自动分配GPU
67.     )
68.     tokenizer = AutoTokenizer.from_pretrained(model_name)
69.     # === 2. 加载量化模型 ===
70.     quant_res_root = 'dsr1_qwen7b_ptq'  # 量化结果目录
71.     dopt_config = f"./{quant_res_root}/dopt_config.json"    # 阶段一生成的配置文件
72.     quanted_ckpt = f"./{quant_res_root}/train_output/trained.pth"  # 阶段二生成的权重
73.     model = get_quanted_model(
74.         model,
75.         dopt_config,  # 需确保已正确配置量化参数
76.         quanted_ckpt   # 需与当前模型架构匹配
77.     )
78.     # === 3. 执行推理测试 ===
79.     prompt = "who are you?"
80.     response = generate(prompt)
81.     print("量化模型推理结果：", response)
82.     """
83.     预期输出示例：
84.     "Hi, I am Qwen, ..."
85.     """

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-plugin-based-quantization "插件式量化")
# 网络结构搜索训练

更新时间: 2025-12-16 16:28

网络结构搜索训练请按照如下步骤进行：

1. 准备环境（[环境准备](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-network-structure-search-training#section193737375169)）。
2. 准备数据集（[数据集准备](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-network-structure-search-training#section1766391819183)）。
3. 配置搜索参数（[搜索参数配置](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-network-structure-search-training#section9753193220185)）。
4. 配置开发者接口（[TensorFlow开发者自定义接口](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-network-structure-search-training#section183452511917)、[PyTorch开发者自定义接口](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-network-structure-search-training#section56271946125514)）。
5. 搜索和训练网络结构（[搜索训练](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-network-structure-search-training#section05357228205)）。

## 环境准备

### Linux环境

1. NASEA策略运行环境的依赖在如下的requirements中：
    
    1. tensorflow-gpu==2.8
    2. ruamel.yaml==0.17.28
    3. PyYAML==5.4.1
    4. Cython==0.29.35
    5. pymoo==0.3.2
    6. pathlib
    7. mpi4py==3.1.4
    8. sklearn
    9. opencv-python
    10. matplotlib
    11. numpy==1.23.5
    12. tqdm==4.43.0
    13. protobuf==3.20.3
    14. requests==2.31.0
    15. Pillow==7.1.2
    
    请使用pip或者conda安装上述依赖。
    
    说明
    
    如果仅需要在单机单卡运行工具，可跳过后续步骤。如需要单机多卡环境运行，请继续完成如下步骤。
    
2. 安装并配置[Horovod](https://github.com/horovod/horovod#instal)和Open MPI。
3. 安装mpi4py。
    
    1. pip3 install mpi4py
    
4. 验证安装。
    
    下载[Horovod](https://github.com/horovod/horovod/blob/master/examples/tensorflow/tensorflow_mnist.py)官方对应的[Demo](https://github.com/horovod/horovod/blob/master/examples/tensorflow/tensorflow_mnist.py)到当前目录。在一台服务器上利用4张加速卡运行如下命令：
    
    1. horovodrun -np 4 -H localhost:4 python3 tensorflow_mnist.py
    
    若正常训练，则Horovod环境部署成功。
    

## 数据集准备

开发者根据需要准备数据集或代理数据集：

1. 在user_module.py中定义数据集函数，并在该函数中接收scen.yaml传入的数据集路径。
    
    说明
    
    TensorFlow版本中函数名为build_dataset_search，PyTorch版本中函数名为dataset_define。
    
2. 解析数据集，读取图片和标签。根据is_training判断是训练还是评估模式。
    
    - 如果是训练模式，则dataset_dir传入scen.yaml中配置的train_dir目录。
    - 如果是评估模式，则dataset_dir传入scen.yaml中配置的val_dir目录。
    
3. 解析对应的数据并返回处理后的数据（具体接口定义参见[TensorFlow开发者自定义接口](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-network-structure-search-training#section183452511917)、[PyTorch开发者自定义接口](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-network-structure-search-training#section56271946125514)）。

## 搜索参数配置

开发者可配置合适的搜索参数，以达到较优的搜索结果。开发者需自行完成配置文件（可参考“tools_dopt/dopt_tf_py3/demo/nas_ea/ea_cls_imagenet/scen.yaml”），如下示例：

1. _## Network architecture search scenario_
2. scenario:
3.   strategy:
4.     name:                NASEA
5.     framework:           Tensorflow
6.     batch_size:          128
7.     epochs:              60
8.     constraint:
9.       application_type:  "image_classification"
10.       constraint_type:   "size"
11.       constraint_value:  11000000
12.     supernet:
13.       input_shape:       (224, 224, 3) 
14.       data_format:       "channels_last" 
15.       filters:           [64, 64, 128, 128, 256, 256] 
16.       strides:           [1, 1, 2, 1, 2, 1] 
17.       feature_choose:    [4, 5]
18.     optimizer:
19.       weights_optimizer:
20.         type:            "Adam"
21.         betas:           [0.9, 0.999]
22.         learning_rate:   0.0001
23.     dataset:
24.       pre_train_dir：   "/tmp/tfrecords"
25.       train_dir:        "/tmp/ImageNet_tf/"
26.       val_dir:          "/tmp/ImageNet_tf/"
27.     searcher:
28.       generation_num:    100
29.       pop_size:          40
30.     resource:
31.       name:              Tensorflow_standalone
32.       gpu_id:            0,1,2,3,4,5,6,7

参数说明如下表所示。

|参数名称|类型|取值范围|是否必选|参数描述|
|:--|:--|:--|:--|:--|
|**scenario.strategy**|   |   |   |   |
|name|string|NASEA|是|策略名。|
|framework|string|TensorFlow、PyTorch|是|训练框架|
|batch_size|int|-|是|数据集的batch_size。|
|epochs|int|-|是|数据集轮询次数。|
|**scenario.strategy.supernet**|   |   |   |   |
|input_shape|tuple|-|否|模型输入shape的CHW或HWC的维度，默认值：(224, 224, 3)。|
|data_format|string|channels_first/channels_last|否|数据格式，input_shape和data_format取值需要对应，例："channels_last"。在PyTorch版本中，该参数只支持channels_first选项。|
|filters|list|-|否|搜索骨架每层的cout，与strides对应的列表，格式为[cout, ..., cout]，例：[64, 64, 128, 128, 256, 256]。|
|strides|list|-|否|搜索骨架每层使用的stride，例：[1, 1, 2, 1, 2, 1]。|
|feature_choose|list|-|否|需要融合的待搜索层，以逗号分隔，从0开始计数。例：融合第4、6层：[3, 5]。<br><br>该参数当前仅适用于TensorFlow版本的检测场景和PyTorch版本的分割场景。|
|**scenario.strategy.constraint**|   |   |   |   |
|application_type|string|image_classification/object_detection/ semantic_segmentation|是|应用类型，支持分类、检测和分割场景。|
|constraint_type|string|size/flops/latency|是|模型约束类型。目前“latency”约束仅支持TensorFlow版本的分类场景。|
|constraint_value|int, float|-|是|模型约束取值，整个网络的大小。|
|processor_version|string|npu_v1|否|该参数目前仅支持模型约束类型为"latency"的场景。|
|**scenario.strategy.optimizer**|   |   |   |   |
|**scenario.strategy.optimizer.weights_optimizer**|   |   |   |   |
|type|string|SGD/Momentum/Adam|否|优化器[1]，分类检测默认值："Adam"，分割默认值："Momentum"。在PyTorch版本中，目前仅支持"SGD"和"Adam"两种优化器，分类场景和分割场景的默认优化器为"Adam"。|
|betas|list|(0, 1)|否|衰减因子，Adam优化器参数，默认值：[0.9, 0.999]。|
|learning_rate|float|(0, 1)|否|学习率，多GPU时工具会自动翻倍，分类检测默认值：0.0001，分割默认值：0.00001。|
|momentum|float|(0, 1)|否|动量，Momentum优化器参数，默认值：0.9。该参数目前仅支持TensorFlow版本。|
|**scenario.strategy.dataset**|   |   |   |   |
|pre_train_dir|string|-|是|检测和分割场景为**必选项**，分类场景无需此字段，预训练数据集路径或预训练生成的ckpt路径（参见注释[2]）。|
|train_dir|string|-|是|训练数据集路径。|
|val_dir|string|-|是|验证数据集路径。|
|**scenario.strategy.searcher**|   |   |   |   |
|generation_num|int|-|否|进化算法的代数，例：100。|
|pop_size|int|-|否|进化算法的种群数量，默认值：40。|
|**scenario.resource**|   |   |   |   |
|name|string|Tensorflow_standalone/ pytorch_standalone|是|资源对象名称。|
|gpu_id|string|-|是|指定使用的gpuID。<br><br>- 填写一个gpu id，如0，则使用单机单卡模式进行训练。<br>- 填写多个gpu id，如0, 1, 2, 3，则使用单机多卡模型进行训练。|

说明

[1] 优化器类型支持SGD，Momentum和Adam三种优化器类型。

- SGD优化器，支持learning_rate参数。
- Momentum优化器，支持momentum、learning_rate参数。PyTorch版本目前不支持该优化器。
- Adam优化器，支持betas、learning_rate参数，betas的形式为list，list中索引为0的元素为beta1，索引为1的元素为beta2。

[2] 当没有预训练的ckpt文件时，其取值为预训练数据集的目录路径；当有预训练的ckpt文件时，其取值为ckpt所在的目录路径。

## TensorFlow开发者自定义接口

网络结构搜索基于TensorFlow框架进行训练，开发者需要按照如下的接口定义配置模型训练文件。

说明

仅支持tf.keras实现。

### UserModule类

|   |   |
|---|---|
|**类描述**|class **UserModule** - 定义开发者侧接口。|
|**函数描述**|构造函数。|
|**接口定义**|def **__init__**(self, epoch, batch_size)|

此类用于定义搜索过程中的以下几个函数：

- 数据集读取。
    
    |   |   |
    |---|---|
    |**函数描述**|数据集读取函数。|
    |**接口定义**|分类场景：<br><br>def **build_dataset_search**(self, dataset_dir, is_training)<br><br>检测、分割场景：<br><br>def **build_dataset_search**(self, dataset_dir, is_training, is_shuffle)|
    |**参数描述**|dataset_dir：数据集路径。当前is_training为True时传入scen.yaml中配置的train_dir路径，否则传入scen.yaml中配置的val_dir路径。<br><br>is_training：训练时为True； 推理时为False。<br><br>is_shuffle：数据集是否需要shuffle。提示：在evaluation阶段更新bn时，数据集不需要做shuffle。|
    |**返回值**|- 训练流程<br>    <br>    分类、分割场景：<br>    <br>    dataset: TensorFlow数据集。<br>    <br>    data_num: 数据集图片数量。<br>    <br>    检测场景：<br>    <br>    train_generator：训练集生成器。<br>    <br>    train_dataset_size：训练集数量。<br>    <br><br>- 推理流程<br>    <br>    分类、分割场景：<br>    <br>    dataset: TensorFlow数据集。<br>    <br>    data_num: 数据集图片数量。<br>    <br>    检测场景：<br>    <br>    val_generator：验证集生成器。<br>    <br>    val_dataset：解析json文件后的数据集。<br>    <br>    val_dataset_size：验证集数量。|
    
- 学习率更新策略。
    
    |   |   |
    |---|---|
    |**函数描述**|学习率更新策略函数。|
    |**接口定义**|def **lr_scheduler**(self, lr_init, global_step)|
    |**参数****描述**|lr_init：学习率的初始值。<br><br>global_step：TensorFlow的global step。|
    |**返回值**|已更新的学习率。|
    
    说明
    
    推荐将学习率的初始值设为常数。
    
- 评估函数。
    
    |   |   |
    |---|---|
    |**函数描述**|评估函数。|
    |**接口定义**|def **metrics_op**(self, inputs, outputs)|
    |**参数描述**|- 分类、分割场景<br>    <br>    inputs：真值标签(ground truth labels)。<br>    <br>    outputs：前向推理的结果。<br>    <br><br>- 检测场景<br>    <br>    inputs: [valid_dir, model]<br>    <br>    valid_dir：验证集路径。<br>    <br>    model：网络模型。<br>    <br>    outputs： [data_generator, proxy_val_image_ids, data_size]<br>    <br>    data_generator：数据集生成器。<br>    <br>    proxy_val_image_ids：代理验证集图片索引，用于从验证集中挑选出一个子集，以加快评估效率。<br>    <br>    data_size：数据集大小。|
    |**返回值**|评估结果。|
    
- loss计算函数。
    
    |   |   |
    |---|---|
    |**函数描述**|loss计算函数。|
    |**接口定义**|def **loss_op**(self, labels, logits)|
    |**参数描述**|labels：真值标签(ground truth labels)。<br><br>logits：前向推理的结果。|
    |**返回值**|loss值，tensor。|
    

### PreNet类

模型中输入层不需要搜索，因此通过固定网络结构的形式定义。

|   |   |
|---|---|
|**类描述**|Class **PreNet** - 模型输入层。|
|**函数描述**|PreNet构造函数。|
|**接口定义**|def **__init__**(self)|
|**参数****描述**|NA。|
|**返回值**|NA。|
|**函数描述**|构建模型的输入结构。|
|**接口定义**|def **call**(self, inputs, training=True)|
|**参数****描述**|inputs：输入数据。<br><br>training：训练时为True； 推理时为False。|
|**返回值**|搜索骨架的输入，tensor。|

### PostNet类

模型中输出层不需要搜索，因此通过固定网络结构的形式定义。

|   |   |
|---|---|
|**类描述**|Class **PostNet** - 模型输出层。|
|**函数描述**|PostNet构造函数。|
|**接口定义**|def **__init__**(self)|
|**参数描述**|NA。|
|**返回值**|NA。|
|**函数描述**|构建模型的输出结构。|
|**接口定义**|def **call**(self, inputs, training=True)|
|**参数描述**|inputs：搜索骨架的输出。<br><br>training：训练时为True； 推理时为False。|
|**返回值**|模型输出，tensor。|

## PyTorch开发者自定义接口

网络结构搜索基于PyTorch框架进行训练，开发者需要按照如下的接口定义配置模型训练文件。

### UserModule类

|   |   |
|---|---|
**表1** UserModule类
|**类描述**|class **UserModule** - 定义开发者侧接口|
|**函数描述**|构造函数|
|**接口定义**|def **__init__**(self, epoch, batch_size)|

此类用于定义搜索过程中的以下几个函数：

|   |   |
|---|---|
**表2** 数据集读取
|**函数描述**|数据集读取函数|
|**接口定义**|def **dataset_define**(self, dataset_dir, is_training)|
|**参数描述**|dataset_dir：数据集路径，当前is_training为True时传入scen.yaml中配置的train_dir路径，否则传入scen.yaml中配置的val_dir路径。<br><br>is_training：训练时为True； 推理时为False。|
|**返回值**|PyTorch的torch.utils.data.Dataset对象实例。|

|   |   |
|---|---|
**表3** 学习率更新策略
|**函数描述**|学习率更新策略函数|
|**接口定义**|def **scheduler_define**(self, optimizer, steps_per_epoch)|
|**参数****描述**|optimizer：优化器对象实例。<br><br>steps_per_epoch：训练过程中每个epoch的步数。|
|**返回值**|PyTorch的lr_scheduler对象实例。|

|   |   |
|---|---|
**表4** 评估函数
|**函数描述**|评估函数|
|**接口定义**|def **metrics_func**(self, eval_dataloader, eval_function)|
|**参数描述**|- eval_dataloader：PyTorch的Dataloader对象，用于加载验证数据集。<br>- eval_function：前向推理函数，eval_dataloader中加载的数据输入到该函数中可以得到对应的推理结果。|
|**返回值**|评估结果。|

|   |   |
|---|---|
**表5** loss计算函数
|**函数描述**|loss计算函数|
|**接口定义**|def **loss_func**(self, labels, logits)|
|**参数描述**|labels：数据的真实标签。<br><br>logits：前向推理的结果。|
|**返回值**|loss值。|

### PreNet类

模型中输入层不需要搜索，因此通过固定网络结构的形式定义。

|   |   |
|---|---|
|**类描述**|Class **PreNet** - 模型输入层|
|**函数描述**|PreNet构造函数|
|**接口定义**|def **__init__**(self)|
|**参数****描述**|NA|
|**返回值**|NA|
|**函数描述**|构建模型的输入结构。|
|**接口定义**|def **forward**(self, inputs)|
|**参数****描述**|inputs：输入数据。|
|**返回值**|搜索骨架的输入，tensor。|

### PostNet类

模型中输出层不需要搜索，因此通过固定网络结构的形式定义。

|   |   |
|---|---|
|**类描述**|Class **PostNet** - 模型输出层|
|**函数描述**|PostNet构造函数|
|**接口定义**|def **__init__**(self)|
|**参数描述**|NA|
|**返回值**|NA|
|**函数描述**|构建模型的输出结构|
|**接口定义**|def **forward**(self, inputs)|
|**参数描述**|inputs：搜索骨架的输出，如果开发者在scen.yaml中没有配置feature_choose，那么inputs是一个tensor；如果开发者配置了scen.yaml中的feature_choose参数，那么inputs是一个列表，其内容依次为feature_choose中配置的对应层的输出以及搜索骨架最后一层的输出。|
|**返回值**|模型输出，tensor。|

## 搜索训练

主要从以下三个方面介绍工具的训练入口，维测方式以及搜索结果展示。

### 训练入口

TensorFlow开发者执行“python3 tools_dopt/dopt_tf_py3/dopt_so.py -c scen.yaml”，即开启搜索训练；PyTorch开发者执行“python3 tools_dopt/dopt_pytorch_py3/dopt_so.py -c scen.yaml”。针对每种场景都有对应的demo目录入口，详见[TensorFlow NASEA网络结构搜索Demo](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-examples#section1897718597348)。

注意

在执行上述命令时，工具将在当前目录下查找user_module.py文件。

### 维测方式

搜索训练过程可以利用[TensorBoard](https://www.tensorflow.org/tensorboard?hl=zh-cn)进行观测中间信息，生成的信息文件保存在log_*目录。

- loss-模型精度损失loss曲线
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162811.94630943931934492664707609341753:50001231000000:2800:B2E88B961873BC4B77D037C43DA548FA946D20EC2CDD3ADA4DDD174A1DC60115.png "点击放大")
    
- lr-学习率变化曲线
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162811.61946637633951468300569725698964:50001231000000:2800:1C80F4548BC276E57947EBCB463A7C43AF4184601DC7C0B624CA841CE5CBBE33.png "点击放大")
    
- pareto-帕累托前沿图
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162811.65272481078525003288322649815946:50001231000000:2800:4DEEB2AB7F0D25DE3D0147A6421A1B2485F9859B62F357BAABF7ABB0D33F71C1.png "点击放大")
    

帕累托图横坐标为模型大小或计算量即约束项，纵坐标为结构搜索后的精度。图中的精度为搜索过程的评估结果，如果要获得更好的精度，建议对搜索结构进行充分训练。

搜索模型结构具有不同的精度、参数量/计算量/时延，开发者可根据实际需求选择合适的模型。

### 搜索结果展示

搜索结束后，工具会自动将pareto图中模型结构保存在results目录，生成多个model_arch_result_$NUM.py文件。其中$NUM文件编号与pareto图上的编号一致，头部有model_param_size和accuracy，开发者可根据TensorBoard中的pareto图或者这两个参数选择合适的网络结构，例如TensorFlow版本的搜索结果（PyTorch版本的搜索结果只是实现框架不同，不再赘述）如下图所示：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162811.59304818130528037190885269742656:50001231000000:2800:59BED32F2A428AC2B25A3BA7639AC0B87695168D81E6F5F78003D8F22545FA27.png "点击放大")

开发者选定合适的模型结构文件，可以拷贝到results的上一级目录，并执行模型结构文件。

1. python3 model_arch_result_$NUM.py

执行结束后，当前目录下会生成模型的pb文件和TensorBoard日志文件，开发者可通过TensorBoard查看模型的图结构。如下：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162811.22019760458007636158078263153579:50001231000000:2800:50377F29F8256D0E8B74569DF02217F61FE9A22D3B7EC9696B53270B945B91D3.png "点击放大")

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-large-language-model "大语言模型低位量化")
# 模型轻量化示例

更新时间: 2025-12-16 16:28

## TensorFlow Quant_INT8-8无训练量化Demo

### 环境准备

请参见[环境准备](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-no-training-and-quantization#section025882820347)，安装TensorFlow及依赖。

### 模型配置

- 准备量化模型
    
    将基线模型的pb文件放入“dopt_tf_py3/demo/quant8-8/notrain/tensorflow_mnist/basemodel/”。该路径下已经放入了mnist基线模型mnist.pb。
    

- 准备量化输入数据
    
    参见[模型量化](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-no-training-and-quantization#section977955263419)，将图片或二进制形式的校准集放入“dopt_tf_py3/demo/quant8-8/notrain/tensorflow_mnist/mnist_test/”中。该路径下已经放入了图片校准集。
    

### 模型量化

执行“dopt_tf_py3/demo/quant8-8/notrain/tensorflow_mnist/”下run_release.sh即可。

“dopt_tf_py3/demo/quant8-8/notrain/tensorflow_mnist”中存有量化后的pb模型和量化配置文件，运行demo后生成的文件如下图所示：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162811.41229513946903544335366102200806:50001231000000:2800:8666910E2B3F1BA5870841BC2B537B349060B4E2587BCD30898901E7B10554F2.png)

## PyTorch Quant_INT8-8无训练量化Demo

### 环境准备

请参见[环境准备](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-no-training-and-quantization#section8715155563919)，安装PyTorch及依赖。

### 模型配置

- 准备量化模型
    
    将基线模型的模型定义文件(.py)以及模型参数文件放入“dopt_pytorch_py3/demo/quant8-8/notrain/pytorch_mnist/”中。
    
    该路径下已经放入了mnist基线模型定义文件mnist.py以及模型参数文件mnist.pth。
    

- 准备量化输入数据
    
    参见[模型量化](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-no-training-and-quantization#section793161024016)，将图片或二进制形式的校准集放入“dopt_pytorch_py3/demo/quant8-8/notrain/pytorch_mnist/”中。
    

### 模型量化

执行“dopt_pytorch_py3/demo/quant8-8/notrain/pytorch_mnist/”下run_release.sh即可。

“dopt_pytorch_py3/demo/quant8-8/notrain/pytorch_mnist/”中存有PyTorch无训练量化示例文件，如下图所示：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162811.75072199019622276928458137676879:50001231000000:2800:7601804B7FEB5E97C98574D0B12245CE666C8CBFDB14DDB3EDE5C2FB4AE21118.png)

## ONNX Quant_INT8-8无训练量化Demo

### 环境准备

环境准备请参见[环境准备](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-no-training-and-quantization#section2399333123120)，安装ONNX及依赖。

### 示例代码

将dopt_onnx_py3 目录添加到系统环境中，在终端环境执行

1. python3 ./dopt_so.py \
2.     --framework 5 \
3.     --mode   0 \
4.     --model "./resnet18_matmul.onnx" \          ## 待量化的ONNX模型
5.     --cal_conf "./config.prototxt" \            ## 校准集配置文件
6.     --output  "./resnet18_matmul_quant.onnx" \  ## 量化后的ONNX文件
7.     --input_shape   input:1,3,128,128 \         ## 浮点模型输入shape  
8.     --compress_conf  ./mnist_param              ## dopt 工具生成的量化文件

其中，./config.prototxt配置内容为（[配置文件使用方法](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-no-training-and-quantization#section1262217244312)）：

1. strategy: 'Quant_INT8-8'
2. device: USE_CPU
3. preprocess_parameter:
4. {
5.     input_type: BINARY
6.     input_file_path: './input1.bin'
7. }

## TensorFlow Quant_INT8-8插件式量化Demo

### 环境准备

请参见[准备TensorFlow环境](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-plugin-based-quantization#section103814481178)。安装TensorFlow-gpu 2.8.0版本以及其必要的依赖。

### 示例代码

1. import sys
2. sys.path.append(".../dopt_tf_py3") ## 其中路径为绝对路径

3. def generate_config():
4.     with tf.Session(config=config) as sess:
5.         build_tf_model() ## 自定义tf模型graph，仅构建拓扑图，不可加载权重
6.         from dopt.dopt_tf.opt_main import generate_config_file
7.         generate_config_file(sess, dst_path="./config_gen.json")

8. def train_model():
9.     with tf.Session(config=config) as sess:
10.         build_tf_model() ## 自定义tf模型graph，仅构建拓扑图，不可加载权重
11.         from dopt.dopt_tf.opt_main import optimize_model
12.         quant_flag = tf.placeholder(tf.int32)
13.         is_train_flag = tf.placeholder(tf.bool, name='is_train')
14.         ## 模型量化，自动在 tf.get_default_graph()上进行改图操作
15.         optimize_model( 
16.             sess,
17.             "./config_gen.json",
18.             is_train_flag,
19.             quant_flag
20.         )
21.         ## 调用完optimize_model之后，加载模型权重
22.         saver = tf.Saver()
23.         saver.restore(ckpt)
24.         tf.global_variables_initializer().run()
25.         ## train model
26.         for i in range(...):
27.             optimizer = ...
28.             feed_dict[is_train_flag] = True
29.             feed_dict[quant_flag] = 1
30.             sess.run(train_op, feed_dict)
31.         ## eval model
32.         feed_dict[is_train_flag] = False
33.         feed_dict[quant_flag] = 1
34.         sess.run(output, feed_dict)
35.         evaluate_output(output)

36. def calibrate_model():
37.     with tf.Session(config=config) as sess:
38.         build_tf_model() ## 自定义tf模型graph，仅构建拓扑图，不可加载权重
39.         from dopt.dopt_tf.opt_main import optimize_model, set_calibrate_state 
40.         quant_flag = tf.placeholder(tf.int32)
41.         is_train_flag = tf.placeholder(tf.bool, name='is_train')
42.         ## 模型量化，自动在 tf.get_default_graph()上进行改图操作
43.         optimize_model( 
44.             sess,
45.             "./config_gen.json",
46.             is_train_flag,
47.             quant_flag
48.         )
49.         ## 调用完optimize_model之后，加载模型权重
50.         saver = tf.Saver()
51.         saver.restore(ckpt)

52.         calibration_mode = True
53.         set_calibrate_state(sess, calibration_mode ) 
54.         ## eval model
55.         feed_dict[is_train_flag] = False
56.         feed_dict[quant_flag] = 1
57.         sess.run(output, feed_dict)
58.         evaluate_output(output)

59. def generate_params():
60.     with tf.Session(config=config) as sess:
61.         build_tf_model()
62.         from dopt.dopt_tf.opt_main import generate_final_model
63.         generate_final_model(
64.             sess,
65.             config_file         = "./config_gen.json",
66.             output_name_list    = ["output"],
67.             ckpt_file           = "train_ckpt_path",
68.             output_dir          = "./output_dir"
69.         )
70. if __name__ == "__main__":
71.     ## step 1
72.     ## 开发者接入，配置修改
73.     generate_config()

74.     ## step 2
75.     ## 训练模型，直至达标
76.     train_model() ## 重训练量化模型
77.     ## calibrate_model()  ## 校准量化模型

78.     ## step 3
79.     ## 提取参数，用于后续模型部署
80.     generate_params()

## PyTorch Quant_INT8-8插件式量化Demo

### 环境准备

请参见[准备PyTorch环境](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-plugin-based-quantization#section461318612307)。安装PyTorch-gpu 1.11版本以及其必要的依赖。

### 示例代码

1. import sys
2. sys.path.append(".../dopt_tf_py3") ## 其中路径为绝对路径

3. def generate_config():
4.     model = build_torch_model()  ## 开发者待量化的浮点模型
5.     generate_config_file(model, input_shape, dst_path="./config_gen.json") # model：torch.nn.Module， input_shape : "input1:input1.shape;input2:input2.shape"
6.     return model

7. def train_model():
8.     model = build_torch_model() ## 开发者待量化的浮点模型
9.     from dopt.dopt_torch.opt_main import optimize_model
10.     model.load_state_dict(state)  ## load 浮点模型参数

11.     ## 调用optimize model 量化模型
12.     quanted_model = optimize_model(model, config_path)

13.     ## train model
14.     quant_loss = get_quant_loss(quant_model)
15.     optimizer = torch.optim.SGD(quanted_model.parameters(), lr=0.001, momentum=0.9) ## 假设使用SGD优化器

16.     for input_data, label in range(...):
17.         optimizer.zero_grad()
18.         outputs = model(input_data)
19.         loss = loss_fn(outputs, label) ## loss_fn 为原始浮点网络训练loss

20.         total_loss = loss + quant_weight * quant_loss ## quant_weight是指量化损失所占比例
21.         loss.backward()

22.         optimizer.step()

23. def calibrate_model():
24.     model = build_torch_model() ## 开发者待量化的浮点模型
25.     from dopt.dopt_torch.opt_main import optimize_model, set_calibrate_state
26.     model.load_state_dict(state)  ## load 浮点模型参数

27.     ## 调用optimize model 量化模型
28.     quanted_model = optimize_model(model, config_path)

29.     calibrate_mode = True
30.     set_calibrate_state(model, calibrate_mode)

31.     for input_data, label in range(...):
32.         outputs = model(input_data)

33. def generate_params():
34.     model = build_torch_model()
35.     from dopt.dopt_torch.opt_main import generate_final_model
36.     generate_final_model(model, 
37.                         config_file,
38.                         pth_file="quant.pth",
39.                         output_dir="./results_dir")

40. if __name__ == "__main__":
41.     ## step 1
42.     ## 开发者接入，配置修改
43.     generate_config()

44.     ## step 2
45.     ## 训练模型，直至达标
46.     train_model()
47.     ## 无训练模式
48.     ## calibrate_model() 

49.     ## step 3
50.     ## 提取参数，用于后续模型部署
51.     generate_params()

## TensorFlow NASEA网络结构搜索Demo

### NASEA分类网络

分类网络Demo位于“tools_dopt/dopt_tf_py3/demo/nas_ea/ea_cls_imagenet”，包含5个文件，如下图所示：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162811.63853178372802748016153692375077:50001231000000:2800:060C6AA0D4569C9FB40DBF86BB3B558D13134C8EEDA8D544B9149AEB9D8F77E8.png)

- blocks.so：搜索空间文件
- readme.md：搜索训练指导文件
- run_release.sh：开始搜索的执行脚本
- scen.yaml：配置项
- user_module.py：工具的自定义接口

执行步骤：

1. 准备ImageNet数据集（tfrecord格式），并修改scen.yaml文件中的数据集路径。
2. 环境准备请参见[环境准备](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-network-structure-search-training#section193737375169)。
3. 加载依赖的开源代码：
    
    1. 进入分类网络demo目录：
        
        1. cd tools_dopt/dopt_tf_py3/demo/nas_ea/ea_cls_imagenet
        
    
    2. 下载开源代码：
        
        1. git clone https://github.com/Tensorflow/models.git
        
    
    3. 进入开源代码目录：
        
        1. cd models
        
    
    4. 切换到指定版本：
        
        - 如果TensorFlow版本为1.12.0，执行如下命令：
            
            1. git checkout v1.12.0
            
        
        - 如果TensorFlow版本为2.1.0，执行如下命令：
            
            1. git checkout v2.1.0
            
    5. 返回分类网络demo目录：
        
        1. cd ..
        
    6. 设置PYTHONPATH默认路径：
        
        1. export PYTHONPATH=$PYTHONPATH:`pwd`/models/
        
    
    注意
    
    每次打开终端需要重新执行一次上述命令，或添加到“~/.bashrc”文件，并执行“source ~/.bashrc”。
    
4. 配置demo下的scen.yaml文件，请参见[搜索参数配置](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-network-structure-search-training#section9753193220185)。scen.yaml中提供了建议参数，开发者可根据实际需求修改。
5. 修改demo下的user_module.py文件，模型接口定义请参见[TensorFlow用户自定义接口](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-network-structure-search-training#section183452511917)。user_module.py中提供了建议配置，开发者可根据实际需求进行修改。
6. 执行脚本run_release.sh，在results下，生成多个model_arch_result_*.py文件。开发者可根据log_classification中提供的信息选择合适的网络结构进行训练。后续训练可参考readme.md中的指导。

### NASEA检测网络

检测网络Demo位于“tools_dopt/dopt_tf_py3/demo/nas_ea/ea_det_coco”，包含6个文件，如下图所示：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162811.83001575479426226546673379548552:50001231000000:2800:10D13A756D52BCC4A07E708A3414A0D8A7C101E4C7D4C4787E7BF80115988691.png)

- blocks.so：搜索空间文件。
- pre_train.yaml：预训练的配置项。
- readme.md：搜索训练指导文件。
- run_release.sh：开始搜索的执行脚本。
- scen.yaml：配置项。
- user_module.py：工具的自定义接口。

执行步骤：

1. 准备数据集，包括用于预训的ImageNet数据集（tfrecord格式）和用于训练的COCO数据集（原始格式）。若有完成预训练的ckpt文件，则不需再准备ImageNet数据集。请参见[搜索参数配置](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-network-structure-search-training#section9753193220185)，修改scen.yaml文件中的数据集路径。
2. 环境准备请参见[环境准备](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-network-structure-search-training#section193737375169)。
3. 加载依赖的开源代码。
    
    1. 进入检测网络demo目录。
        
        1. cd tools_dopt/dopt_tf_py3/demo/nas_ea/ea_det_coco
        
    2. 下载开源代码。
        
        1. git clone https://github.com/pierluigiferrari/ssd_keras.git
        2. git clone https://github.com/Tensorflow/models.git
        
    3. 进入开源代码目录。
        
        1. cd ssd_keras
        
    4. 切换到指定版本。
        
        1. git checkout -b v0.9.0
        
    5. 返回检测网络demo目录。
        
        1. cd ..
        
    6. 进入models开源代码目录。
        
        1. cd models
        
    7. 切换models到指定版本。
        
        如果TensorFlow版本为1.12.0，执行如下命令：
        
        1. git checkout v1.12.0
        
        如果TensorFlow版本为2.1.0，则执行如下命令：
        
        2. git checkout v2.1.0
        
    8. 进入models开源代码目录
        
        1. cd models
        
    9. 设置PYTHONPATH默认路径
        
        1. export PYTHONPATH=$PYTHONPATH:`pwd`/models/
        
    10. 按照readme.md中的step1~step4步骤，修改相关开源文件。
    
4. 配置demo的scen.yaml文件和pre_train.yaml，请参见[搜索参数配置](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-network-structure-search-training#section9753193220185)。scen.yaml中提供了建议参数，开发者可根据实际需求修改。
5. 修改demo的user_module.py文件，模型接口定义请参见[TensorFlow用户自定义接口](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-network-structure-search-training#section183452511917)。user_module.py中提供了建议配置，开发者可根据实际需求进行修改。
6. 执行脚本run_release.sh，在results下，生成多个model_arch_result_*.py文件。开发者可根据log_detection中提供的信息选择合适的网络结构进行训练。后续训练可参考readme.md中的指导。

### NASEA分割网络

分割网络Demo位于“tools_dopt/dopt_tf_py3/demo/nas_ea/ea_seg_voc”，包含 6个文件，如下图所示：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162811.21931815362470661763805651775084:50001231000000:2800:C64AE6058616E44F472CEF2A0070EB1BDE1E71ED53245920EBAC28D2CCB45C39.png)

- blocks.so：搜索空间文件。
- pre_train.yaml：预训练的配置项
- readme.md：搜索训练指导文件。
- run_release.sh：开始搜索的执行脚本。
- scen.yaml：配置项。
- user_module.py：工具的自定义接口。

执行步骤：

1. 准备数据集，包括用于预训练的ImageNet数据集（tfrecord格式）和用于训练的VOC数据集（tfrecord格式）。若有完成预训练的ckpt文件，则不需再准备ImageNet数据集。请参见[搜索参数配置](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-network-structure-search-training#section9753193220185)，修改scen.yaml文件中的数据集路径。
2. 环境准备请参见[环境准备](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-network-structure-search-training#section193737375169)。
3. 加载依赖的开源代码。
    
    1. 进入分割网络demo目录。
        
        1. cd tools_dopt/dopt_tf_py3/demo/nas_ea/ea_seg_voc
        
    2. 下载开源代码：
        
        1. git clone https://github.com/Tensorflow/models.git
        
    3. 进入开源代码目录。
        
        1. cd models
        
    4. 切换到指定版本。
        
        1. git checkout v1.13.0
        
    5. 返回分割网络demo目录。
        
        1. cd ..
        
    6. 设置PYTHONPATH默认路径：
        
        1. export PYTHONPATH=$PYTHONPATH:`pwd`/models/research:`pwd`/models/research/slim
        
    7. 如果TensorFlow版本为2.1.0，需要执行如下命令：
        1. 创建models_tf2.1，并进入文件夹
            
            1. mkdir models_tf2.1
            2. cd models_tf2.1
            
        2. 下载开源实现
            
            1. git clone https://github.com/Tensorflow/models.git
            
        3. 进入开源代码路径
            
            1. cd models
            
        4. 切换到指定版本
            
            1. git checkout v2.1.0
            
        5. 返回models_tf2.1目录
            
            1. cd ..
            
        6. 设置PYTHONPATH默认路径
            
            1. export PYTHONPATH=$PYTHONPATH:`pwd`/models/
            
            注意
            
            每次打开终端需要重新执行一次上述命令，或添加到“~/.bashrc”文件，并执行“source ~/.bashrc”。
            
    8. 修改开源实现，按照readme.md中修改开源实现的步骤，修改相关开源文件。
    
4. 配置demo的scen.yaml文件和pre_train.yaml，请参见[搜索参数配置](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-network-structure-search-training#section9753193220185)。scen.yaml中提供了建议参数，开发者可根据实际需求修改。
5. 修改demo的user_module.py文件，模型接口定义请参见[TensorFlow用户自定义接口](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-network-structure-search-training#section183452511917)。user_module.py中提供了建议配置，开发者可根据实际需求进行修改。
6. 执行脚本run_release.sh，在results下，生成多个model_arch_result_*.py文件。开发者可根据log_segmentation中提供的信息选择合适的网络结构进行训练。后续训练可参考readme.md中的指导。

## PyTorch NASEA网络结构搜索Demo

### NASEA分类网络

分类网络Demo位于tools_dopt/dopt_pytorch_py3/demo/nas_ea/ea_cls_imagenet_pytorch，包含5个文件，如下：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162812.40150877675653986206093244436152:50001231000000:2800:25FDCAF129E567D2F7749077DA0F2D42B261398064EE881E4BD1B0AE119AB76B.png)

- blocks.so：搜索空间文件
- readme.md：搜索训练指导文件
- run_release.sh：开始搜索的执行脚本
- scen.yaml：配置项
- user_module.py：工具的自定义接口

执行步骤：

1. 准备ImageNet数据集（原始格式），并修改scen.yaml文件中的数据集路径。
2. 环境准备请参见[环境准备](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-network-structure-search-training#section193737375169)。
3. 配置demo下的scen.yaml文件，请参见[搜索参数配置](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-network-structure-search-training#section9753193220185)。scen.yaml中提供了建议参数，开发者可根据实际需求修改。
4. 修改demo下的user_module.py文件，模型接口定义请参见[PyTorch开发者自定义接口](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-network-structure-search-training#section56271946125514)。user_module.py中提供了建议配置，开发者可根据实际需求进行修改。
5. 执行脚本run_release.sh，在results下，生成多个model_arch_result_*.py文件。开发者可根据log_classification中提供的信息选择合适的网络结构进行训练。后续训练可参考readme.md中的指导。

### NASEA分割网络

分割网络Demo位于tools_dopt/dopt_pytorch_py3/demo/nas_ea/ea_seg_voc_pytorch，包含 6个文件，如下：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162812.98481281650686190567040360957309:50001231000000:2800:91674586CA139067C11BAFAF405CE5E039FE0DF205D016F9B890C99AE365FEE5.png)

- blocks.so：搜索空间文件
- pre_train.yaml：预训练的配置项
- readme.md：搜索训练指导文件
- run_release.sh：开始搜索的执行脚本
- scen.yaml：配置项
- user_module.py：工具的自定义接口

执行步骤：

1. 准备数据集，包括用于预训练的ImageNet数据集（原始格式）和用于训练VOC数据集（原始格式）。若有完成预训练的ckpt文件，则不需再准备ImageNet数据集。请参见[搜索参数配置](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-network-structure-search-training#section9753193220185)，修改scen.yaml文件中的数据集路径。
2. 环境准备请参见[环境准备](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-network-structure-search-training#section193737375169)。
3. 加载依赖的开源代码：参考tools_dopt/dopt_pytorch_py3/demo/nas_ea/ea_seg_voc_pytorch/readme.md
4. 配置demo下的scen.yaml文件和pre_train.yaml文件，请参见[搜索参数配置](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-network-structure-search-training#section9753193220185)。scen.yaml中提供了建议参数，开发者可根据实际需求修改。
5. 修改demo下的user_module.py文件，模型接口定义请参见[PyTorch开发者自定义接口](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-network-structure-search-training#section56271946125514)。user_module.py中提供了建议配置，开发者可根据实际需求进行修改。
6. 执行脚本run_release.sh，在results下，生成多个model_arch_result_*.py文件。开发者可根据log_segmentation中提供的信息选择合适的网络结构进行训练。后续训练可参考readme.md中的指导。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-network-structure-search-training "网络结构搜索训练")
# 模型收益

更新时间: 2025-12-16 16:28

## Quant_INT8-8量化收益

以resnet-18为例，使用轻量化工具后（Quant_INT8-8量化）的收益如下。

|框架|数据集|模型|原始精度|重训练后精度|非量化OM离线<br><br>模型体积(MB)|Quant_INT8-8量化OM<br><br>离线模型体积(MB)|
|:--|:--|:--|:--|:--|:--|:--|
|TensorFlow|ImageNet|resnet-18(v2)|70.0%|70.0%|22.457|11.9|

## 网络结构搜索工具分类场景收益对比

以resnet-18为例，使用轻量化工具后（网络结构搜索）的收益如下。

|框架|数据集|模型|参数量（M）|精度|
|:--|:--|:--|:--|:--|
|TensorFlow|ImageNet|ResNet-18|11.69|70.32%|
|NASEA|10.93|72.13%[1]|
|PyTorch|ImageNet|ResNet-18|11.69|69.6%|
|NASEA|11.4|72.88%|

### 检测场景收益对比

|框架|数据集|模型|计算量（G）|mAP@[.5, .95][2]|
|:--|:--|:--|:--|:--|
|SSD(backbone：ResNet-18)|COCO|ResNet-18|11.6|17.8[3]|
|NASEA|9.25|18.4[3]|

### 分割场景收益对比

|框架|数据集|模型|计算量（G）|mIOU[4]|
|:--|:--|:--|:--|:--|
|TensorFlow|VOC|ResNet-18 + Deeplab v3|40.9|54.1[5]|
|NASEA|28.3|56.1[5]|
|PyTorch|VOC|ResNet-18 + Deeplab v3|43.7|64.2|
|NASEA|30.7|65.1|

说明

[1] 此精度是使用tensorpack重训练模型得出。

[2] 此指标的计算方法为：IoU(Intersection over Union)从0.5~0.95区间上，以0.05为间隔计算AP的值，再计算所有AP的均值。

[3] 此精度是在COCO val2017数据集上测试得出。

[4] 此指标为平均交并比，计算方法为先求每个类别的交并比，再平均。

[5] 此精度是在VOC val2012数据集上测试得出。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-model-size-reduction-faqs "常见问题")
# 模型收益

更新时间: 2025-12-16 16:28

## Quant_INT8-8量化收益

以resnet-18为例，使用轻量化工具后（Quant_INT8-8量化）的收益如下。

|框架|数据集|模型|原始精度|重训练后精度|非量化OM离线<br><br>模型体积(MB)|Quant_INT8-8量化OM<br><br>离线模型体积(MB)|
|:--|:--|:--|:--|:--|:--|:--|
|TensorFlow|ImageNet|resnet-18(v2)|70.0%|70.0%|22.457|11.9|

## 网络结构搜索工具分类场景收益对比

以resnet-18为例，使用轻量化工具后（网络结构搜索）的收益如下。

|框架|数据集|模型|参数量（M）|精度|
|:--|:--|:--|:--|:--|
|TensorFlow|ImageNet|ResNet-18|11.69|70.32%|
|NASEA|10.93|72.13%[1]|
|PyTorch|ImageNet|ResNet-18|11.69|69.6%|
|NASEA|11.4|72.88%|

### 检测场景收益对比

|框架|数据集|模型|计算量（G）|mAP@[.5, .95][2]|
|:--|:--|:--|:--|:--|
|SSD(backbone：ResNet-18)|COCO|ResNet-18|11.6|17.8[3]|
|NASEA|9.25|18.4[3]|

### 分割场景收益对比

|框架|数据集|模型|计算量（G）|mIOU[4]|
|:--|:--|:--|:--|:--|
|TensorFlow|VOC|ResNet-18 + Deeplab v3|40.9|54.1[5]|
|NASEA|28.3|56.1[5]|
|PyTorch|VOC|ResNet-18 + Deeplab v3|43.7|64.2|
|NASEA|30.7|65.1|

说明

[1] 此精度是使用tensorpack重训练模型得出。

[2] 此指标的计算方法为：IoU(Intersection over Union)从0.5~0.95区间上，以0.05为间隔计算AP的值，再计算所有AP的均值。

[3] 此精度是在COCO val2017数据集上测试得出。

[4] 此指标为平均交并比，计算方法为先求每个类别的交并比，再平均。

[5] 此精度是在VOC val2012数据集上测试得出。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-model-size-reduction-faqs "常见问题")
# 模型转换示例

更新时间: 2025-12-16 16:28

使用CANN Kit SDK时，可以预先使用OMG工具将Caffe、TensorFlow、ONNX、MindSpore模型转换为OM离线模型，移动端AI程序直接读取离线模型进行推理。OMG工具位于[Tools下载](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-preparations#section152959341125)的tools/tools_omg下，可运行在64位Linux平台上。

## Caffe模型转换

当前支持[Caffe](https://gitee.com/mirrors/caffe) 1.0版本。

命令行中的参数说明请参见[OMG参数](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-overall-parameter)，转换命令：

1. ./omg --model xxx.prototxt --weight yyy.caffemodel --framework 0 --output ./modelname

转换示例：

1. ./omg --model deploy.prototxt --weight squeezenet_v1.1.caffemodel --framework 0 --output ./squeezenet

当看到OMG generate offline model success时，则说明转换成功，会在当前目录下生成squeezenet.om。

## TensorFlow模型转换

当前支持[TensorFlow](https://www.tensorflow.org/?hl=zh-cn) 2.x版本。

命令行中的参数说明请参见[OMG参数](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-overall-parameter)，转换命令：

1. ./omg --model xxx.pb --framework 3 --output ./modelname --input_shape "xxx:n,h,w,c" --out_nodes "node_name1:0"

转换示例：

1. ./omg --model mobilenet_v2_1.0_224_frozen.pb --framework 3 --output ./mobilenet_v2 --input_shape "input:1,224,224,3" --out_nodes "MobilenetV2/Predictions/Reshape_1:0"

当看到OMG generate offline model success时，则说明转换成功，会在当前目录下生成mobilenet_v2.om。

## ONNX模型转换

当前支持[ONNX](https://github.com/onnx/onnx) opset版本7~18（最高支持到V1.13.1）。

命令行中的参数说明请参见[OMG参数](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-overall-parameter)，转换命令：

1. ./omg --model xxx.onnx --framework 5 --output ./modelname 

转换示例:

1. ./omg --model resnet18.onnx --framework 5 --output ./resnet18

当看到如下log时，则说明转换成功，会在当前目录下生成resnet18.om。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162807.60312651902845236342404960008731:50001231000000:2800:619163F25AA62E0C7D71D022FEEE490112552CBCE003DE8CF563CD90391993B0.png "点击放大")

## 量化模型转换（以Caffe模型为例）

目前大部分模型在NPU上都是使用16bit float类型进行计算的，使用量化既可以减少模型的体积，也可以加快模型推理速度。

量化模型转换依赖轻量化工具，利用轻量化工具生成模型及轻量化配置，通过“compress_conf”参数传递给OMG并生成量化模型，更多说明请参见[模型轻量化](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-lightweight-tool-overview)。

命令行中的参数说明请参见[OMG参数](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-overall-parameter)，转换命令：

1. ./omg --model xxx.prototxt --weight xxx.caffemodel --framework 0 --output ./modelname  --compress_conf=param

转换示例：

1. ./omg --model deploy.prototxt --weight squeezenet_v1.1.caffemodel --framework 0 --output ./squeezenet --compress_conf=param

当看到OMG generate offline model success时，说明模型量化成功，会在当前目录下生成量化模型squeezenet.om。

## 推理前可变Shape模型转换（以ONNX模型为例）

如果一个模型需要支持一次加载，然后不同次的推理会遇到不同的batch，或者不同的分辨率，那么可以使用推理前可变Shape的模型转换。

在模型转换时，将推理过程可能遇到的所有Shape种类预先通过dynamic_dims和input_shape指定出来，生成一个标准IR模型，其携带多种shape输入。

命令行中的参数说明请参见[OMG参数](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-overall-parameter)。

转换示例：

1. ./omg --model=./1batch.onnx --input_shape="inputName:-1,3,128,128" --dynamic_dims="1;2;5" --framework=5 --output=./FlexibleShapeModelName

说明

不同shape输入对应的不同输出shape，可在模型转换日志中，通过 "Graph:" 关键字查找对应的shape信息，方便在模型推理时指定对应的输出描述。

## MindSpore模型转换

MindSpore支持的算子数量有限，建议通过[TensorFlow模型转换](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-model-conversion-example#section165091091578)或者[ONNX模型转换](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-model-conversion-example#section59657541256)。

## AIPP模型转换（以Caffe模型为例）

如果模型推理需要对图像或其他输入数据进行变换（如图像尺寸变换、色域转换、减均值/乘系数等），可使用AIPP模型转换功能。转换后的模型增加算子替换此类操作，可提升效率。

命令行中的参数说明请参见[OMG参数](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-overall-parameter)，转换命令：

1. ./omg --model xxx.prototxt --weight xxx.caffemodel --framework 0 --insert_op_conf aipp_conf_static.cfg --output ./modelname

转换示例：

1. ./omg --model deploy.prototxt --weight squeezenet_v1.1.caffemodel --framework 0 --insert_op_conf aipp_conf_static.cfg --output ./squeezenet

当出现OMG generate offline model success时，说明AIPP模型转换成功，会在当前目录下生成AIPP squeezenet.om模型。

说明

aipp_conf_static.cfg是AIPP的配置文件，位置存放在“tools/tools_omg/sample”文件夹中，具体说明参见[AIPP配置文件说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-aipp-configuration-file#section1435315264269)。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-preparing-for-model-conversion "模型转换前准备")
# 模型转换示例

更新时间: 2025-12-16 16:28

使用CANN Kit SDK时，可以预先使用OMG工具将Caffe、TensorFlow、ONNX、MindSpore模型转换为OM离线模型，移动端AI程序直接读取离线模型进行推理。OMG工具位于[Tools下载](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-preparations#section152959341125)的tools/tools_omg下，可运行在64位Linux平台上。

## Caffe模型转换

当前支持[Caffe](https://gitee.com/mirrors/caffe) 1.0版本。

命令行中的参数说明请参见[OMG参数](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-overall-parameter)，转换命令：

1. ./omg --model xxx.prototxt --weight yyy.caffemodel --framework 0 --output ./modelname

转换示例：

1. ./omg --model deploy.prototxt --weight squeezenet_v1.1.caffemodel --framework 0 --output ./squeezenet

当看到OMG generate offline model success时，则说明转换成功，会在当前目录下生成squeezenet.om。

## TensorFlow模型转换

当前支持[TensorFlow](https://www.tensorflow.org/?hl=zh-cn) 2.x版本。

命令行中的参数说明请参见[OMG参数](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-overall-parameter)，转换命令：

1. ./omg --model xxx.pb --framework 3 --output ./modelname --input_shape "xxx:n,h,w,c" --out_nodes "node_name1:0"

转换示例：

1. ./omg --model mobilenet_v2_1.0_224_frozen.pb --framework 3 --output ./mobilenet_v2 --input_shape "input:1,224,224,3" --out_nodes "MobilenetV2/Predictions/Reshape_1:0"

当看到OMG generate offline model success时，则说明转换成功，会在当前目录下生成mobilenet_v2.om。

## ONNX模型转换

当前支持[ONNX](https://github.com/onnx/onnx) opset版本7~18（最高支持到V1.13.1）。

命令行中的参数说明请参见[OMG参数](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-overall-parameter)，转换命令：

1. ./omg --model xxx.onnx --framework 5 --output ./modelname 

转换示例:

1. ./omg --model resnet18.onnx --framework 5 --output ./resnet18

当看到如下log时，则说明转换成功，会在当前目录下生成resnet18.om。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162807.60312651902845236342404960008731:50001231000000:2800:619163F25AA62E0C7D71D022FEEE490112552CBCE003DE8CF563CD90391993B0.png "点击放大")

## 量化模型转换（以Caffe模型为例）

目前大部分模型在NPU上都是使用16bit float类型进行计算的，使用量化既可以减少模型的体积，也可以加快模型推理速度。

量化模型转换依赖轻量化工具，利用轻量化工具生成模型及轻量化配置，通过“compress_conf”参数传递给OMG并生成量化模型，更多说明请参见[模型轻量化](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-lightweight-tool-overview)。

命令行中的参数说明请参见[OMG参数](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-overall-parameter)，转换命令：

1. ./omg --model xxx.prototxt --weight xxx.caffemodel --framework 0 --output ./modelname  --compress_conf=param

转换示例：

1. ./omg --model deploy.prototxt --weight squeezenet_v1.1.caffemodel --framework 0 --output ./squeezenet --compress_conf=param

当看到OMG generate offline model success时，说明模型量化成功，会在当前目录下生成量化模型squeezenet.om。

## 推理前可变Shape模型转换（以ONNX模型为例）

如果一个模型需要支持一次加载，然后不同次的推理会遇到不同的batch，或者不同的分辨率，那么可以使用推理前可变Shape的模型转换。

在模型转换时，将推理过程可能遇到的所有Shape种类预先通过dynamic_dims和input_shape指定出来，生成一个标准IR模型，其携带多种shape输入。

命令行中的参数说明请参见[OMG参数](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-overall-parameter)。

转换示例：

1. ./omg --model=./1batch.onnx --input_shape="inputName:-1,3,128,128" --dynamic_dims="1;2;5" --framework=5 --output=./FlexibleShapeModelName

说明

不同shape输入对应的不同输出shape，可在模型转换日志中，通过 "Graph:" 关键字查找对应的shape信息，方便在模型推理时指定对应的输出描述。

## MindSpore模型转换

MindSpore支持的算子数量有限，建议通过[TensorFlow模型转换](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-model-conversion-example#section165091091578)或者[ONNX模型转换](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-model-conversion-example#section59657541256)。

## AIPP模型转换（以Caffe模型为例）

如果模型推理需要对图像或其他输入数据进行变换（如图像尺寸变换、色域转换、减均值/乘系数等），可使用AIPP模型转换功能。转换后的模型增加算子替换此类操作，可提升效率。

命令行中的参数说明请参见[OMG参数](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-overall-parameter)，转换命令：

1. ./omg --model xxx.prototxt --weight xxx.caffemodel --framework 0 --insert_op_conf aipp_conf_static.cfg --output ./modelname

转换示例：

1. ./omg --model deploy.prototxt --weight squeezenet_v1.1.caffemodel --framework 0 --insert_op_conf aipp_conf_static.cfg --output ./squeezenet

当出现OMG generate offline model success时，说明AIPP模型转换成功，会在当前目录下生成AIPP squeezenet.om模型。

说明

aipp_conf_static.cfg是AIPP的配置文件，位置存放在“tools/tools_omg/sample”文件夹中，具体说明参见[AIPP配置文件说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-aipp-configuration-file#section1435315264269)。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-preparing-for-model-conversion "模型转换前准备")
# OMG参数

更新时间: 2025-12-16 16:28

说明

- 路径：支持大小写字母、数字、下划线。
- 文件名：支持大小写字母、数字、下划线和点(.)。

|参数名称|参数描述|是否必选|默认值|
|:--|:--|:--|:--|
|--h/help|显示帮助信息。|否|不涉及|
|--mode|运行模式。<br><br>- 0：生成DaVinci模型。<br>- 1：模型转json。json可查看模型结构的文本格式。<br><br>- 3：仅做预检，检查模型文件的内容是否合法。|否|0|
|--model|原始框架模型文件路径。|是|不涉及|
|--framework|原始框架类型。<br><br>- 0：Caffe。<br>- 3：TensorFlow。<br>- 5：ONNX。<br>- 6：MindSpore。<br><br>说明<br><br>- 当mode为1时，该参数可选，可以指定Caffe、TensorFlow、ONNX、MindSpore，不指定时默认为离线模型转json。<br>- 当mode为0或3时，该参数必选，可以指定Caffe或TensorFlow或ONNX或MindSpore。<br>- 当原始模型格式为TensorFlow的CheckPoint、SavedModel、TFLite时，推荐使用[tf2onnx](https://github.com/onnx/tensorflow-onnx)工具转换成ONNX模型后使用。|是|不涉及|
|--weight|权值文件路径。当原始模型是Caffe时需要指定。当原始模型是其他框架时不需要指定。|否|不涉及|
|--output|存放转换后的离线模型文件的路径（包含文件名），例如“out/caffe_resnet18”。转换后的模型文件，会自动以.om的后缀结尾。|是|不涉及|
|--hiai_version|指定使用OMG的版本，当前支持：v300\|v310\|IR。|否|IR|
|--om|模型文件路径。当mode为1时必填。|否|不涉及|
|--json|模型文件转换为json格式文件的路径。|否|不涉及|
|--input_shape|输入数据的shape。当input_shape参数为-1时，必须和--dynamic_dims参数联合使用。<br><br>例如：“input_name1: n1, c1, h1, w1; input_name2: n2, c2, h2, w2”。input_name必须是转换前的网络模型中的节点名称。<br><br>当原始模型是ONNX时，input_name必须是模型转换前的网络模型中input算子的name。<br><br>说明<br><br>- 当原始模型是ONNX，并且ONNX模型输入维度为动态时，此参数必须指定。<br>- 当原始模型是TensorFlow，并且TensorFlow模型输入维度为动态时，此参数必须指定。|否|不涉及|
|--input_format|输入数据格式：NCHW和NHWC。<br><br>说明<br><br>- 当原始框架是Caffe时或ONNX或MindSpore时，此参数不生效。<br>- 当原始框架是TensorFlow时，绝大多数场景不需要指定，如果转换时提示需要指定，根据实际情况指定。|否|不涉及|
|--input_type|支持设定模型输入格式，支持指定为FP32、FP16、 INT32、UINT8等，包括多输入和单输入。具体是否能成功生成离线模型，取决于原始模型是否支持指定为该格式的输入。模型输入支持场景详见[非AIPP场景设定输入类型支持情况](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-overall-parameter#li13442526155)和[AIPP场景设定输入类型支持情况](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-overall-parameter#li478393817151)。<br><br>例如："input_name1:FP16;input_name2:UINT8"。<br><br>input_name必须是转换前的网络模型中的节点名称。<br><br>当原始模型是ONNX时，input_name必须是模型转换前的网络模型中input算子的name。|否|FP32|
|--input_fp16_nodes|不支持与--input_type同时设置。<br><br>指定数据类型为“fp16nchw”的输入节点名称。<br><br>例如：“node_name1;node_name2”。<br><br>说明<br><br>当原始框架是ONNX或MindSpore时，此参数不生效。|否|不涉及|
|--out_nodes|指定输出节点。<br><br>- 如果原始模型是TensorFlow或者Caffe，按照以下格式指定：“node_name1:0;node_name1:1;node_name2:0”。<br>    <br>    node_name必须是模型转换前的网络模型中的节点名称。同一个节点的输出从0开始，如果该节点有多个输出，依次往后累加。<br>    <br><br>- 如果原始模型是ONNX，按照以下格式指定：“tensor_name1;tensor_name2”。<br>    <br>    tensor_name必须是模型转换前的网络模型中的节点输出Tensor名称。|否|不涉及|
|--output_type|支持设定模型的输出数据类型，支持指定为FP32、FP16、INT32、UINT8等，包括多输出和单输出。具体是否能成功生成离线模型，取决于原始模型是否支持指定为该类型的输出。模型输出支持场景详见[非AIPP场景设定输入类型支持情况](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-overall-parameter#li13442526155)。<br><br>例如："output_name1:FP16;output_name2:UINT8"。<br><br>output_name必须是转换前的网络模型中的节点名称。<br><br>当原始框架是ONNX时，output_name可以是模型转换前的网络模型中output算子的name或者是开发者指定out_nodes中所用到的tensor_name。|否|FP32|
|--is_output_fp16|不支持与--output_type同时设置。<br><br>标注输出的数据类型是否为“fp16 nchw”。<br><br>例如：false, true, false, true。<br><br>说明<br><br>当原始框架是ONNX或MindSpore时，此参数不生效。|否|false|
|--stream_num|模型使用的stream数量，当前仅支持1。|否|1|
|--check_report|预检结果保存文件路径。若不指定该路径，在模型转换失败或mode为3（仅做预检）时，将预检结果保存在当前路径下。|否|不涉及|
|--net_format|指定网络算子优先选用的数据格式。<br><br>说明<br><br>注：该参数现已不推荐使用，可通过网络推导得出。|否|不涉及|
|--insert_op_conf|AIPP配置文件路径。详情参见[模型转换AIPP配置文件说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-aipp-configuration-file)。|否|不涉及|
|--op_name_map|算子映射配置文件路径。包含DetectionOutput网络时需要指定。<br><br>例如：不同的网络中DetectionOutput算子的功能不同，指定DetectionOutput到FSRDetectionOutput或者SSDDetectionOutput的映射。<br><br>说明<br><br>算子映射配置文件的内容示例如下：<br><br>DetectionOutput:SSDDetectionOutput。|否|不涉及|
|--compress_conf|轻量化配置文件路径。该参数需与轻量化工具搭配使用，由轻量化工具自动生成。具体参见[模型轻量化](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-lightweight-tool-overview)。|否|不涉及|
|--weight_data_type|支持设定模型权值数据类型，支持指定为FP32或FP16。<br><br>该参数仅针对模型中权值数据类型为FP32时生效，根据设定将权值数据类型由FP32转为FP16存储或维持FP32不变。该参数默认值为FP16。<br><br>例如："weight_data_type:FP16"。<br><br>说明<br><br>由于CPUCL不支持FP16的权重进行计算，如果模型需要兼容CPU计算库，需要指定该参数为FP32。|否|FP16|
|--weight_merge|离线模型权值归并开关，支持指定在离线模型生成时权值是否进行归并存储操作；该参数为true时，模型权值归并存储。该参数为false时，权值维持非归并存储方式，对性能无影响。该参数默认为true。|否|true|
|--use_origin_format|支持设定模型的输入输出和原始模型保持一致的format。<br><br>说明<br><br>本参数仅支持基于yolo、inception的业务网络转换设置为true，其它网络转换使用默认值false。|否|false|
|--dynamic_dims|支持同一个原始模型生成能支持不同shape输入档位的Davinci模型，该参数指定可以变化的dim值。和**--input_shape**参数配合使用，在input_shape参数中可以变化的dim使用-1代替。<br><br>该参数中每一种可以变化的dims值使用分号分隔（也称为一档），如果一档中有多个维度，每个维度之间使用逗号分隔。举例：<br><br>- 动态batch<br>    <br>    --input_shape = "input_name1:-1,c,h,w" --dynamic_dims = "n1;n2;n3"<br>    <br><br>- 动态分辨率<br>    <br>    --input_shape = "input_name1:n,-1,-1,c" --dynamic_dims = "h1,w1;h2,w2"<br>    <br><br>说明<br><br>使用约束：支持可以变化的shape种类最多16种。|否|不涉及|
|--platform|芯片平台，当--target设置为omc时必须设置。|否|不涉及|
|--target|目标模型类型。<br><br>- om<br>    <br>    硬件无关Davinci模型。<br>    <br>- omc<br>    <br>    硬件强相关Davinci模型，仅可在--platform指定的平台部署|否|om|

说明

当前只支持下表列出的情况。

- 非AIPP场景设定输入类型支持情况
    
    |**原始模型实际输入**|**离线模型期望输入（开发者设定）**|**针对OMG参数**|
    |:--|:--|:--|
    |FP32|FP16|--input_type|
    |FP32|FP32|--input_type|
    |FP16|FP16|--input_type|
    |UINT8|UINT8|--input_type|
    |INT32|INT32|--input_type|
    |INT8|INT8|--input_type|
    

- AIPP场景设定输入类型支持情况
    
    |**原始模型实际输入**|**离线模型期望输入**|**是否有AIPP**|**针对OMG参数**|
    |:--|:--|:--|:--|
    |FP32|UINT8|有|--input_type|
    |FP16|UINT8|有|--input_type|
    |UINT8|UINT8|有|--input_type|
    
- 设定输出类型支持情况
    
    |**原始模型**|**离线模型输出**|**针对OMG参数**|
    |:--|:--|:--|
    |FP32|UINT8|--output_type|
    |FP16|UINT8|--output_type|
    |UINT8|UINT8|--output_type|
    |FP16|FP16|--output_type|
    |FP32|FP32|--output_type|
    |FP32|FP16|--output_type|
    |FP16|FP32|--output_type|
    |INT8|INT8|--output_type|
    |INT32|INT32|--output_type|
    |INT64|INT64|--output_type|
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-model-conversion-example "模型转换示例")
# 模型转换AIPP配置文件说明

更新时间: 2025-12-16 16:28

## 模型转换AIPP配置文件说明

一份功能完整的AIPP配置文件示例如下：

1. # AIPP的配置以aipp_op开始，标识这是一个AIPP算子的配置，aipp_op支持配置多个
2. aipp_op {
3.     # input_name参数为可选，标识对模型的哪个输入做AIPP处理
4.     # 类型：string
5.     input_name: "data"

6.     # related_input_rank参数为可选，与input_name对应，推荐使用input_name，当模型输入名称未知时，可使用related_input_rank标识对模型的第几个输入做AIPP处理
7.     # 类型：uint32
8.     related_input_rank: 0

9.     # node_after_aipp参数为可选，用于当一个输入之后有多个分支，需要对分支进行不同的AIPP处理的场景，且需满足均配置或者均不配置，不能只配置一部分分支
10.     # 类型：string
11.     node_after_aipp: "op_name"

12.     # input_edge_idx参数为可选，与node_after_aipp对应，当输入Data算子之后的若干算子名称重复时，可以使用input_edge_idx标识对第几个分支进行AIPP处理
13.     # 类型：uint32
14.     input_edge_idx: 0

15.     input_para {
16.         # 输入图片的类型
17.         # 类型: enum
18.         # 取值范围：[YUV420SP_U8, XRGB8888_U8, ARGB8888_U8, YUYV_U8, YUV422SP_U8, AYUV444_U8, YUV400_U8, RGB888_U8]
19.         format: AYUV444_U8

20.         shape {
21.             # 输入图片的宽度、高度
22.             # 类型：uint32
23.             # 取值范围 & 约束：[0,4096]、对于除了YUV400之外的YUV类型的图片，要求取值是偶数
24.             src_image_size_w: 800
25.             src_image_size_h: 600
26.         }

27.         # max_src_image_size用于动态AIPP的场景，当图片的长宽或者输入类型不确定时，设置输入图片最大的size
28.         # 类型: uint32
29.         max_src_image_size: 102400
30.     }

31.     # == Crop参数设置 == #
32.     crop_func {
33.         switch: true
34.         dynamic: true
35.         load_start_pos_w: 50
36.         load_start_pos_h: 50
37.         crop_size_w: 400
38.         crop_size_h: 400
39.     }

40.     # == Channel Swap参数设置 == #
41.     swap_func {
42.         dynamic: true
43.         rbuv_swap_switch: true
44.         ax_swap_switch: true
45.     }

46.     # == Resize参数设置 == #
47.     resize_func {
48.         switch: true
49.         dynamic: true
50.         resize_output_w: 200
51.         resize_output_h: 200
52.     }

53.     # == Color Space Conversion参数设置 == #
54.     csc_func {
55.         switch: true
56.         dynamic: true
57.         matrix_r0c0: 256
58.         matrix_r0c1: 0
59.         matrix_r0c2: 259
60.         matrix_r1c0: 256
61.         matrix_r1c1: -88
62.         matrix_r1c2: -183
63.         matrix_r2c0: 256
64.         matrix_r2c1: 454
65.         matrix_r2c2: 0
66.         output_bias_0: 0
67.         output_bias_1: 0
68.         output_bias_2: 0
69.         input_bias_0: 16
70.         input_bias_1: 128
71.         input_bias_2: 128
72.     }

73.     # == Data Type Conversion参数设置 == #
74.     dtc_func {
75.         switch: true
76.         dynamic: true
77.         mean_chn_0: 0
78.         mean_chn_1: 0
79.         mean_chn_2: 0
80.         mean_chn_3: 0
81.         min_chn_0: 0
82.         min_chn_1: 0
83.         min_chn_2: 0
84.         min_chn_3: 0
85.         var_reci_chn_0: 1.0
86.         var_reci_chn_1: 1.0
87.         var_reci_chn_2: 1.0
88.         var_reci_chn_3: 1.0
89.     }

90.     # == Rotation参数设置 == #
91.     rotation_func {
92.         switch: true
93.         dynamic: true
94.         rotation_angle: 0.0
95.     }

96.     # == Padding参数设置 == #
97.     padding_func {
98.         switch: true
99.         dynamic: true
100.         left_padding_size: 12
101.         right_padding_size: 12
102.         top_padding_size: 12
103.         bottom_padding_size: 12
104.         padding_value_chn_0: 20.0
105.         padding_value_chn_1: 20.0
106.         padding_value_chn_2: 20.0
107.         padding_value_chn_3: 20.0
108.     }
109. }

### AIPP配置多输入支持

AIPP支持对一个多输入模型的多个输入分别配置AIPP，也支持在一个输入Data算子有多个输出分支的情况下，对不同的输出分支分别配置AIPP。

AIPP配置的多输入支持由2组共4个配置参数控制：input_name和related_input_rank用于指定对哪一个输入进行AIPP处理，node_after_aipp和input_edge_idx用于指定对Data算子的多个输出中的哪一个输出进行AIPP处理。

input_name和related_input_rank两个参数推荐使用input_name，related_input_rank参数用于模型输入名称不确定的场景，如果同时配置这两个参数，则两个参数互为校验；如果两个参数都没有被配置，默认对模型的第一个输入进行AIPP处理。

node_after_aipp和input_edge_idx两个参数推荐使用node_after_aipp，input_edge_idx用于Data算子的多个输出分支衔接的算子名称重复或不确定的场景，如果同时配置这两个参数，则两个参数互为校验；如果两个参数都没有被配置，则该Data算子的所有输出分支使用同一个AIPP处理。

### AIPP配置区分动态AIPP与静态AIPP

只要有一个AIPP子功能的dynamic开关配置为true，或者没有打开任何一个子功能的开关，则生成的DaVinci模型为动态AIPP模型，需要在模型推理阶段传入AIPP配置参数；相反没有任何子功能的dynamic开关配置为true，并且至少有一个子功能的开关是打开的，则生成的DaVinci模型为静态AIPP模型，模型推理阶段使用配置文件中定义的AIPP配置参数。

对于动态AIPP的场景，AIPP可以允许输入图片的长宽，以及图片类型不确定，对应即src_image_size_w、src_image_size_h和input_format三个参数不配置，此时开发者需要指定动态AIPP处理时的最大图片尺寸，配置max_src_image_size。

## 图片裁剪(Crop)

图片裁剪功能是指在原始图片中从指定的起点裁剪出指定大小的子图。

dynamic不写或者写成“false”表示静态配置，写成“true”表示动态配置。

- 静态配置时，crop_size_w和crop_size_h以设定的值作为输出shape。
- 动态配置时，crop_size_w和crop_size_h为预分配的最大输出shape，实际运行时设置的参数值不超过预分配的最大值。

### 静态配置

1. crop_func {
2.     switch: true
3.     load_start_pos_w: 50
4.     load_start_pos_h: 50
5.     crop_size_w: 150
6.     crop_size_h: 150
7. }

### 动态配置

1. crop_func {
2.     switch: true
3.     dynamic: true
4.     load_start_pos_w: 0
5.     load_start_pos_h: 0
6.     crop_size_w: 150
7.     crop_size_h: 150
8. }

## 通道交换功能(axSwap/uvSwap/rbSwap)

交换图片的通道支持AX通道交换、UV通道交换、RB通道交换。

- AX通道交换：仅支持ARGB8888、XRGB8888、AYUV444格式，其他格式不支持。
- UV通道交换：仅支持YUV420SP、YUV422SP_U8、YUYV、AYUV444格式，其他格式不支持。
- RB通道交换：仅支持ARGB8888、XRGB8888、RGB888_U8格式，其他格式不支持。

dynamic不写或者写成“false”表示静态配置，写成“true”表示动态配置。

### 静态配置

1. swap_func {
2.     ax_swap_switch: true
3.     rbuv_swap_switch: false
4. }

### 动态配置

可以不写具体的参数，在动态创建input tensor时指定。

1. swap_func {
2.     dynamic: true
3.     ax_swap_switch: true
4.     rbuv_swap_switch: false
5. }

## 色域转换功能(CSC)

dynamic不写或者写成“false”表示静态配置，写成“true”表示动态配置。

支持的转换格式如下：

- 支持从YUV420SP、YUYV、YUV422SP、AYUV444转到RGB888、BGR888。
- 支持从XRGB8888、ARGB8888、RGB888转到YVU444SP、YUV444SP、YUV400。

### 静态配置

静态AIPP配置色域转化矩阵示例如下。

1. csc_func {
2.     switch: true
3.     matrix_r0c0: 256
4.     matrix_r0c1: 454
5.     matrix_r0c2: 0
6.     matrix_r1c0: 256
7.     matrix_r1c1: -88
8.     matrix_r1c2: -183
9.     matrix_r2c0: 256
10.     matrix_r2c1: 0
11.     matrix_r2c2: 359
12.     output_bias_0: 0
13.     output_bias_1: 0
14.     output_bias_2: 0
15.     input_bias_0: 0
16.     input_bias_1: 128
17.     input_bias_2: 128
18. }

### 动态配置

指定输出的色域格式，动态场景下，inputFormat可以改变，但是output_format不可变，否则会报错，因为输出的格式一般是固定的。

1. csc_func {
2.     switch: true
3.     dynamic: true
4.     output_format: RGB888_U8
5.     color_space: JPEG
6. }

## 图片缩放(Resize)

图片缩放功能支持图片放大缩小，采用双线性插值方式进行缩放。缩放输出图片最小为16x16，缩放输出最大为448x448。

dynamic不写或者写成“false”表示静态配置，写成“true”表示动态配置。

### 静态配置

1. resize_func {
2.     switch: true
3.     resize_output_w: 182
4.     resize_output_h: 182
5. }

### 动态配置

resize_output_w、resize_output_h为预分配最大size。

1. resize_func {
2.     switch: true
3.     dynamic: true
4.     resize_output_w: 250
5.     resize_output_h: 200
6. }

## 数据类型转换(DTC)

数据类型转化功能是指将输入的图片数据类型通过转化公式转换为FP16类型送给后续模块计算，实际为依次执行减均值、减最小值和乘方差操作。

dynamic不写或者写成“false”表示静态配置，写成“true”表示动态配置。

### 静态配置

1. dtc_func {
2.     switch: true
3.     mean_chn_0: 4
4.     mean_chn_1: 4
5.     mean_chn_2: 4
6.     min_chn_0: 2.0
7.     min_chn_1: 2.0
8.     min_chn_2: 2.0
9.     var_reci_chn_0: 2.0
10.     var_reci_chn_1: 2.0
11.     var_reci_chn_2: 2.0
12. }

### 动态配置

可以不写具体的参数，在动态创建input tensor时指定。

1. dtc_func {
2.     switch: true
3.     dynamic: true
4. }

## 图片旋转(Rotation)

旋转功能支持图片旋转90°、180°和270°，以适配手机在不同方向时的图像数据。当前旋转功能只支持静态单算子场景，动态场景以及卷积融合场景不支持。静态配置如下。

1. rotate_para {
2.     switch: true
3.     dynamic: true    
4.     rotation_angle: 0.0
5. }

## 图片补边

图片补边功能支持在图片上下左右padding指定大小的数据。 padding的数据可以按通道来设置不同的值，最多补四个通道，如果有的通道没有设置的话，就默认补0，上下左右Padding的大小最大为32，即最多上下各补32行，左右各补32列。

- 当crop或resize作为最后一个AIPP算子时，它的输出shape固定，即输出shape不可动态调整。后面如果接卷积，卷积的输入shape就是crop或resize的输出shape。
- 当crop或者resize后接padding算子时
    - 如果padding算子是静态的，那么padding算子前面的crop或resize也相当于是静态的，输出shape固定不变，crop或resize的输出shape加上padding的值就是后面卷积的shape。
    - 如果padding算子是动态的，那么padding算子的四个padding值就写0。此时，padding算子前的crop或resize的输出就是后面卷积的shape。动态时可以调整参数值，但是要保证最终的输出等于卷积的输入。

dynamic不写或者写成“false”表示静态配置，写成“true”表示动态配置。

### 静态配置

1. padding_func {
2.     switch: true
3.     left_padding_size: 21
4.     right_padding_size: 21
5.     top_padding_size: 21
6.     bottom_padding_size: 21
7.     padding_value_chn_0: 20.0
8.     padding_value_chn_1: 20.0
9.     padding_value_chn_2: 20.0
10.     padding_value_chn_3: 20.0
11. }

### 动态配置

padding算子是动态的，padding算子的四个padding值就写0，padding value的值在动态创建input tensor时指定。

1. padding_func {
2.     switch: true
3.     dynamic: true
4.     left_padding_size: 0
5.     right_padding_size: 0
6.     top_padding_size: 0
7.     bottom_padding_size: 0
8. }

## 完整AIPP动态配置示例

1. aipp_op {
2.     input_para {
3.         shape {
4.             src_image_size_w: 480
5.             src_image_size_h: 384
6.         }
7.     }
8.     crop_func {
9.         switch: true
10.         dynamic: true
11.         load_start_pos_w: 50
12.         load_start_pos_h: 50
13.         crop_size_w: 150
14.         crop_size_h: 150
15.     }
16.     resize_func {
17.         switch: true
18.         dynamic: true
19.         resize_output_w: 250
20.         resize_output_h: 200
21.     }
22.     padding_func {
23.         switch: true
24.         dynamic: true
25.         left_padding_size: 0
26.         right_padding_size: 0
27.         top_padding_size: 0
28.         bottom_padding_size: 0
29.     }
30.     swap_func {
31.         dynamic: true
32.         ax_swap_switch: true
33.     }
34.     csc_func {
35.         switch: true
36.         dynamic: true
37.         output_format: RGB888_U8
38.         color_space: JPEG
39.     }
40.     dtc_func {
41.         switch: true
42.         dynamic: true
43.     }  
44. }

## 完整AIPP静态配置

1. aipp_op {
2.     input_para {
3.         shape {
4.             src_image_size_w: 480
5.             src_image_size_h: 384
6.         }
7.         format: AYUV444_U8
8.     }
9.     crop_func {
10.         switch: true
11.         load_start_pos_w: 50
12.         load_start_pos_h: 50
13.         crop_size_w: 150
14.         crop_size_h: 150
15.     }
16.     resize_func {
17.         switch: true
18.         resize_output_w: 182
19.         resize_output_h: 182
20.     }
21.     padding_func {
22.         switch: true
23.         left_padding_size: 21
24.         right_padding_size: 21
25.         top_padding_size: 21
26.         bottom_padding_size: 21
27.     }
28.     swap_func {
29.         ax_swap_switch: true
30.     }
31.     csc_func {
32.         switch: true
33.         matrix_r0c0: 256
34.         matrix_r0c1: 454
35.         matrix_r0c2: 0
36.         matrix_r1c0: 256
37.         matrix_r1c1: -88
38.         matrix_r1c2: -183
39.         matrix_r2c0: 256
40.         matrix_r2c1: 0
41.         matrix_r2c2: 359
42.         output_bias_0: 0
43.         output_bias_1: 0
44.         output_bias_2: 0
45.         input_bias_0: 0
46.         input_bias_1: 128
47.         input_bias_2: 128
48.     }
49.     dtc_func {
50.         switch: true
51.         mean_chn_0: 4
52.         mean_chn_1: 4
53.         mean_chn_2: 4
54.         min_chn_0: 2.0
55.         min_chn_1: 2.0
56.         min_chn_2: 2.0
57.         var_reci_chn_0: 2.0
58.         var_reci_chn_1: 2.0
59.         var_reci_chn_2: 2.0
60. }
61.     rotate_func {
62.         switch: true
63.         rotate_angle: 180.0
64.     }
65. }

## 动静态混合配置示例

动静混合场景不支持配置rotate旋转参数，因为此时模型是动态的，动态场景暂不支持rotate旋转参数的配置。

1. aipp_op {
2.     input_para {
3.         shape {
4.             src_image_size_w: 200
5.             src_image_size_h: 200
6.         }
7.         format: ARGB8888_U8
8.     }
9.     crop_func {
10.         switch: true
11.         dynamic: true
12.         crop_size_w: 100
13.         crop_size_h: 100
14.     }
15.     resize_func {
16.         switch: true
17.         resize_output_w: 200
18.         resize_output_h: 200
19.     }
20.     padding_func {
21.         switch: true
22.         right_padding_size: 24
23.         bottom_padding_size: 24
24.     }
25.     swap_func {
26.         rbuv_swap_switch: true
27.         ax_swap_switch: true
28.     }
29.     dtc_func {
30.         switch: true
31.         mean_chn_0: 4
32.         mean_chn_1: 4
33.         mean_chn_2: 4
34.         min_chn_0: 2.0
35.         min_chn_1: 2.0
36.         min_chn_2: 2.0
37.         var_reci_chn_0: 2.0
38.         var_reci_chn_1: 2.0
39.         var_reci_chn_2: 2.0
40.     }
41. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-aipp-parameters "AIPP参数")
# 模型转换AIPP配置文件说明

更新时间: 2025-12-16 16:28

## 模型转换AIPP配置文件说明

一份功能完整的AIPP配置文件示例如下：

1. # AIPP的配置以aipp_op开始，标识这是一个AIPP算子的配置，aipp_op支持配置多个
2. aipp_op {
3.     # input_name参数为可选，标识对模型的哪个输入做AIPP处理
4.     # 类型：string
5.     input_name: "data"

6.     # related_input_rank参数为可选，与input_name对应，推荐使用input_name，当模型输入名称未知时，可使用related_input_rank标识对模型的第几个输入做AIPP处理
7.     # 类型：uint32
8.     related_input_rank: 0

9.     # node_after_aipp参数为可选，用于当一个输入之后有多个分支，需要对分支进行不同的AIPP处理的场景，且需满足均配置或者均不配置，不能只配置一部分分支
10.     # 类型：string
11.     node_after_aipp: "op_name"

12.     # input_edge_idx参数为可选，与node_after_aipp对应，当输入Data算子之后的若干算子名称重复时，可以使用input_edge_idx标识对第几个分支进行AIPP处理
13.     # 类型：uint32
14.     input_edge_idx: 0

15.     input_para {
16.         # 输入图片的类型
17.         # 类型: enum
18.         # 取值范围：[YUV420SP_U8, XRGB8888_U8, ARGB8888_U8, YUYV_U8, YUV422SP_U8, AYUV444_U8, YUV400_U8, RGB888_U8]
19.         format: AYUV444_U8

20.         shape {
21.             # 输入图片的宽度、高度
22.             # 类型：uint32
23.             # 取值范围 & 约束：[0,4096]、对于除了YUV400之外的YUV类型的图片，要求取值是偶数
24.             src_image_size_w: 800
25.             src_image_size_h: 600
26.         }

27.         # max_src_image_size用于动态AIPP的场景，当图片的长宽或者输入类型不确定时，设置输入图片最大的size
28.         # 类型: uint32
29.         max_src_image_size: 102400
30.     }

31.     # == Crop参数设置 == #
32.     crop_func {
33.         switch: true
34.         dynamic: true
35.         load_start_pos_w: 50
36.         load_start_pos_h: 50
37.         crop_size_w: 400
38.         crop_size_h: 400
39.     }

40.     # == Channel Swap参数设置 == #
41.     swap_func {
42.         dynamic: true
43.         rbuv_swap_switch: true
44.         ax_swap_switch: true
45.     }

46.     # == Resize参数设置 == #
47.     resize_func {
48.         switch: true
49.         dynamic: true
50.         resize_output_w: 200
51.         resize_output_h: 200
52.     }

53.     # == Color Space Conversion参数设置 == #
54.     csc_func {
55.         switch: true
56.         dynamic: true
57.         matrix_r0c0: 256
58.         matrix_r0c1: 0
59.         matrix_r0c2: 259
60.         matrix_r1c0: 256
61.         matrix_r1c1: -88
62.         matrix_r1c2: -183
63.         matrix_r2c0: 256
64.         matrix_r2c1: 454
65.         matrix_r2c2: 0
66.         output_bias_0: 0
67.         output_bias_1: 0
68.         output_bias_2: 0
69.         input_bias_0: 16
70.         input_bias_1: 128
71.         input_bias_2: 128
72.     }

73.     # == Data Type Conversion参数设置 == #
74.     dtc_func {
75.         switch: true
76.         dynamic: true
77.         mean_chn_0: 0
78.         mean_chn_1: 0
79.         mean_chn_2: 0
80.         mean_chn_3: 0
81.         min_chn_0: 0
82.         min_chn_1: 0
83.         min_chn_2: 0
84.         min_chn_3: 0
85.         var_reci_chn_0: 1.0
86.         var_reci_chn_1: 1.0
87.         var_reci_chn_2: 1.0
88.         var_reci_chn_3: 1.0
89.     }

90.     # == Rotation参数设置 == #
91.     rotation_func {
92.         switch: true
93.         dynamic: true
94.         rotation_angle: 0.0
95.     }

96.     # == Padding参数设置 == #
97.     padding_func {
98.         switch: true
99.         dynamic: true
100.         left_padding_size: 12
101.         right_padding_size: 12
102.         top_padding_size: 12
103.         bottom_padding_size: 12
104.         padding_value_chn_0: 20.0
105.         padding_value_chn_1: 20.0
106.         padding_value_chn_2: 20.0
107.         padding_value_chn_3: 20.0
108.     }
109. }

### AIPP配置多输入支持

AIPP支持对一个多输入模型的多个输入分别配置AIPP，也支持在一个输入Data算子有多个输出分支的情况下，对不同的输出分支分别配置AIPP。

AIPP配置的多输入支持由2组共4个配置参数控制：input_name和related_input_rank用于指定对哪一个输入进行AIPP处理，node_after_aipp和input_edge_idx用于指定对Data算子的多个输出中的哪一个输出进行AIPP处理。

input_name和related_input_rank两个参数推荐使用input_name，related_input_rank参数用于模型输入名称不确定的场景，如果同时配置这两个参数，则两个参数互为校验；如果两个参数都没有被配置，默认对模型的第一个输入进行AIPP处理。

node_after_aipp和input_edge_idx两个参数推荐使用node_after_aipp，input_edge_idx用于Data算子的多个输出分支衔接的算子名称重复或不确定的场景，如果同时配置这两个参数，则两个参数互为校验；如果两个参数都没有被配置，则该Data算子的所有输出分支使用同一个AIPP处理。

### AIPP配置区分动态AIPP与静态AIPP

只要有一个AIPP子功能的dynamic开关配置为true，或者没有打开任何一个子功能的开关，则生成的DaVinci模型为动态AIPP模型，需要在模型推理阶段传入AIPP配置参数；相反没有任何子功能的dynamic开关配置为true，并且至少有一个子功能的开关是打开的，则生成的DaVinci模型为静态AIPP模型，模型推理阶段使用配置文件中定义的AIPP配置参数。

对于动态AIPP的场景，AIPP可以允许输入图片的长宽，以及图片类型不确定，对应即src_image_size_w、src_image_size_h和input_format三个参数不配置，此时开发者需要指定动态AIPP处理时的最大图片尺寸，配置max_src_image_size。

## 图片裁剪(Crop)

图片裁剪功能是指在原始图片中从指定的起点裁剪出指定大小的子图。

dynamic不写或者写成“false”表示静态配置，写成“true”表示动态配置。

- 静态配置时，crop_size_w和crop_size_h以设定的值作为输出shape。
- 动态配置时，crop_size_w和crop_size_h为预分配的最大输出shape，实际运行时设置的参数值不超过预分配的最大值。

### 静态配置

1. crop_func {
2.     switch: true
3.     load_start_pos_w: 50
4.     load_start_pos_h: 50
5.     crop_size_w: 150
6.     crop_size_h: 150
7. }

### 动态配置

1. crop_func {
2.     switch: true
3.     dynamic: true
4.     load_start_pos_w: 0
5.     load_start_pos_h: 0
6.     crop_size_w: 150
7.     crop_size_h: 150
8. }

## 通道交换功能(axSwap/uvSwap/rbSwap)

交换图片的通道支持AX通道交换、UV通道交换、RB通道交换。

- AX通道交换：仅支持ARGB8888、XRGB8888、AYUV444格式，其他格式不支持。
- UV通道交换：仅支持YUV420SP、YUV422SP_U8、YUYV、AYUV444格式，其他格式不支持。
- RB通道交换：仅支持ARGB8888、XRGB8888、RGB888_U8格式，其他格式不支持。

dynamic不写或者写成“false”表示静态配置，写成“true”表示动态配置。

### 静态配置

1. swap_func {
2.     ax_swap_switch: true
3.     rbuv_swap_switch: false
4. }

### 动态配置

可以不写具体的参数，在动态创建input tensor时指定。

1. swap_func {
2.     dynamic: true
3.     ax_swap_switch: true
4.     rbuv_swap_switch: false
5. }

## 色域转换功能(CSC)

dynamic不写或者写成“false”表示静态配置，写成“true”表示动态配置。

支持的转换格式如下：

- 支持从YUV420SP、YUYV、YUV422SP、AYUV444转到RGB888、BGR888。
- 支持从XRGB8888、ARGB8888、RGB888转到YVU444SP、YUV444SP、YUV400。

### 静态配置

静态AIPP配置色域转化矩阵示例如下。

1. csc_func {
2.     switch: true
3.     matrix_r0c0: 256
4.     matrix_r0c1: 454
5.     matrix_r0c2: 0
6.     matrix_r1c0: 256
7.     matrix_r1c1: -88
8.     matrix_r1c2: -183
9.     matrix_r2c0: 256
10.     matrix_r2c1: 0
11.     matrix_r2c2: 359
12.     output_bias_0: 0
13.     output_bias_1: 0
14.     output_bias_2: 0
15.     input_bias_0: 0
16.     input_bias_1: 128
17.     input_bias_2: 128
18. }

### 动态配置

指定输出的色域格式，动态场景下，inputFormat可以改变，但是output_format不可变，否则会报错，因为输出的格式一般是固定的。

1. csc_func {
2.     switch: true
3.     dynamic: true
4.     output_format: RGB888_U8
5.     color_space: JPEG
6. }

## 图片缩放(Resize)

图片缩放功能支持图片放大缩小，采用双线性插值方式进行缩放。缩放输出图片最小为16x16，缩放输出最大为448x448。

dynamic不写或者写成“false”表示静态配置，写成“true”表示动态配置。

### 静态配置

1. resize_func {
2.     switch: true
3.     resize_output_w: 182
4.     resize_output_h: 182
5. }

### 动态配置

resize_output_w、resize_output_h为预分配最大size。

1. resize_func {
2.     switch: true
3.     dynamic: true
4.     resize_output_w: 250
5.     resize_output_h: 200
6. }

## 数据类型转换(DTC)

数据类型转化功能是指将输入的图片数据类型通过转化公式转换为FP16类型送给后续模块计算，实际为依次执行减均值、减最小值和乘方差操作。

dynamic不写或者写成“false”表示静态配置，写成“true”表示动态配置。

### 静态配置

1. dtc_func {
2.     switch: true
3.     mean_chn_0: 4
4.     mean_chn_1: 4
5.     mean_chn_2: 4
6.     min_chn_0: 2.0
7.     min_chn_1: 2.0
8.     min_chn_2: 2.0
9.     var_reci_chn_0: 2.0
10.     var_reci_chn_1: 2.0
11.     var_reci_chn_2: 2.0
12. }

### 动态配置

可以不写具体的参数，在动态创建input tensor时指定。

1. dtc_func {
2.     switch: true
3.     dynamic: true
4. }

## 图片旋转(Rotation)

旋转功能支持图片旋转90°、180°和270°，以适配手机在不同方向时的图像数据。当前旋转功能只支持静态单算子场景，动态场景以及卷积融合场景不支持。静态配置如下。

1. rotate_para {
2.     switch: true
3.     dynamic: true    
4.     rotation_angle: 0.0
5. }

## 图片补边

图片补边功能支持在图片上下左右padding指定大小的数据。 padding的数据可以按通道来设置不同的值，最多补四个通道，如果有的通道没有设置的话，就默认补0，上下左右Padding的大小最大为32，即最多上下各补32行，左右各补32列。

- 当crop或resize作为最后一个AIPP算子时，它的输出shape固定，即输出shape不可动态调整。后面如果接卷积，卷积的输入shape就是crop或resize的输出shape。
- 当crop或者resize后接padding算子时
    - 如果padding算子是静态的，那么padding算子前面的crop或resize也相当于是静态的，输出shape固定不变，crop或resize的输出shape加上padding的值就是后面卷积的shape。
    - 如果padding算子是动态的，那么padding算子的四个padding值就写0。此时，padding算子前的crop或resize的输出就是后面卷积的shape。动态时可以调整参数值，但是要保证最终的输出等于卷积的输入。

dynamic不写或者写成“false”表示静态配置，写成“true”表示动态配置。

### 静态配置

1. padding_func {
2.     switch: true
3.     left_padding_size: 21
4.     right_padding_size: 21
5.     top_padding_size: 21
6.     bottom_padding_size: 21
7.     padding_value_chn_0: 20.0
8.     padding_value_chn_1: 20.0
9.     padding_value_chn_2: 20.0
10.     padding_value_chn_3: 20.0
11. }

### 动态配置

padding算子是动态的，padding算子的四个padding值就写0，padding value的值在动态创建input tensor时指定。

1. padding_func {
2.     switch: true
3.     dynamic: true
4.     left_padding_size: 0
5.     right_padding_size: 0
6.     top_padding_size: 0
7.     bottom_padding_size: 0
8. }

## 完整AIPP动态配置示例

1. aipp_op {
2.     input_para {
3.         shape {
4.             src_image_size_w: 480
5.             src_image_size_h: 384
6.         }
7.     }
8.     crop_func {
9.         switch: true
10.         dynamic: true
11.         load_start_pos_w: 50
12.         load_start_pos_h: 50
13.         crop_size_w: 150
14.         crop_size_h: 150
15.     }
16.     resize_func {
17.         switch: true
18.         dynamic: true
19.         resize_output_w: 250
20.         resize_output_h: 200
21.     }
22.     padding_func {
23.         switch: true
24.         dynamic: true
25.         left_padding_size: 0
26.         right_padding_size: 0
27.         top_padding_size: 0
28.         bottom_padding_size: 0
29.     }
30.     swap_func {
31.         dynamic: true
32.         ax_swap_switch: true
33.     }
34.     csc_func {
35.         switch: true
36.         dynamic: true
37.         output_format: RGB888_U8
38.         color_space: JPEG
39.     }
40.     dtc_func {
41.         switch: true
42.         dynamic: true
43.     }  
44. }

## 完整AIPP静态配置

1. aipp_op {
2.     input_para {
3.         shape {
4.             src_image_size_w: 480
5.             src_image_size_h: 384
6.         }
7.         format: AYUV444_U8
8.     }
9.     crop_func {
10.         switch: true
11.         load_start_pos_w: 50
12.         load_start_pos_h: 50
13.         crop_size_w: 150
14.         crop_size_h: 150
15.     }
16.     resize_func {
17.         switch: true
18.         resize_output_w: 182
19.         resize_output_h: 182
20.     }
21.     padding_func {
22.         switch: true
23.         left_padding_size: 21
24.         right_padding_size: 21
25.         top_padding_size: 21
26.         bottom_padding_size: 21
27.     }
28.     swap_func {
29.         ax_swap_switch: true
30.     }
31.     csc_func {
32.         switch: true
33.         matrix_r0c0: 256
34.         matrix_r0c1: 454
35.         matrix_r0c2: 0
36.         matrix_r1c0: 256
37.         matrix_r1c1: -88
38.         matrix_r1c2: -183
39.         matrix_r2c0: 256
40.         matrix_r2c1: 0
41.         matrix_r2c2: 359
42.         output_bias_0: 0
43.         output_bias_1: 0
44.         output_bias_2: 0
45.         input_bias_0: 0
46.         input_bias_1: 128
47.         input_bias_2: 128
48.     }
49.     dtc_func {
50.         switch: true
51.         mean_chn_0: 4
52.         mean_chn_1: 4
53.         mean_chn_2: 4
54.         min_chn_0: 2.0
55.         min_chn_1: 2.0
56.         min_chn_2: 2.0
57.         var_reci_chn_0: 2.0
58.         var_reci_chn_1: 2.0
59.         var_reci_chn_2: 2.0
60. }
61.     rotate_func {
62.         switch: true
63.         rotate_angle: 180.0
64.     }
65. }

## 动静态混合配置示例

动静混合场景不支持配置rotate旋转参数，因为此时模型是动态的，动态场景暂不支持rotate旋转参数的配置。

1. aipp_op {
2.     input_para {
3.         shape {
4.             src_image_size_w: 200
5.             src_image_size_h: 200
6.         }
7.         format: ARGB8888_U8
8.     }
9.     crop_func {
10.         switch: true
11.         dynamic: true
12.         crop_size_w: 100
13.         crop_size_h: 100
14.     }
15.     resize_func {
16.         switch: true
17.         resize_output_w: 200
18.         resize_output_h: 200
19.     }
20.     padding_func {
21.         switch: true
22.         right_padding_size: 24
23.         bottom_padding_size: 24
24.     }
25.     swap_func {
26.         rbuv_swap_switch: true
27.         ax_swap_switch: true
28.     }
29.     dtc_func {
30.         switch: true
31.         mean_chn_0: 4
32.         mean_chn_1: 4
33.         mean_chn_2: 4
34.         min_chn_0: 2.0
35.         min_chn_1: 2.0
36.         min_chn_2: 2.0
37.         var_reci_chn_0: 2.0
38.         var_reci_chn_1: 2.0
39.         var_reci_chn_2: 2.0
40.     }
41. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-aipp-parameters "AIPP参数")
# 可变data_type

更新时间: 2025-12-16 16:27

## 概述

可变data_type是OMG工具支持的一个功能，用于模型输入输出数据类型多样性的场景，无需修改训练好的模型，在使用OMG工具进行[模型转换](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-overall-parameter)时，通过指定输入、输出数据类型使得同一个模型适用于不同输入输出的场景。

## 使用说明

在进行模型转换时，输入输出数据类型指定分别需要通过[OMG参数](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-overall-parameter)的input_type、output_type来实现。

使用示例：

1. ./omg --model=./model.pb --framework=3 --output=./model --input_shape="inputs:1,512,512,1" --out_nodes="outputs:0" --input_type="inputs:FP16" --output_type="outputs:UINT8"

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-aipp-configuration-file "模型转换AIPP配置文件说明")
# 模型推理

更新时间: 2025-12-16 16:27

## 基本概念

该场景是基本模型的使用场景，主要包含模型的编译和推理，其他场景是基础场景的一个扩展和功能增强。

## 业务流程

模型推理的主要开发流程如下图所示：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162752.07666453952719000017985960369003:50001231000000:2800:43E05269D926E4636952E4974E82887EDA5ED28825F8321BFDB8DAD385D5C71D.png "点击放大")

## 接口说明

以下接口为主要流程接口，如要使用更丰富的编译、加载和执行时的配置，请参见[API参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cannkit)。

**表1** CANN Kit模型推理相关接口功能介绍
|接口名|描述|
|:--|:--|
|OH_NNCompilation* OH_NNCompilation_ConstructWithOfflineModelBuffer(const void *modelBuffer, size_t modelSize);|根据模型buffer创建模型编译实例。|
|OH_NN_ReturnCode OH_NNCompilation_SetDevice(OH_NNCompilation *compilation, size_t deviceID);|设置模型编译和执行的目标设备。|
|OH_NN_ReturnCode OH_NNCompilation_Build(OH_NNCompilation *compilation);|执行模型编译，生成编译后的模型保存在compilation中。|
|OH_NNExecutor* OH_NNExecutor_Construct(OH_NNCompilation *compilation);|根据编译后的模型，创建模型推理的执行器。|
|NN_Tensor* OH_NNTensor_Create(size_t deviceID, NN_TensorDesc* tensorDesc);|构造输入输出Tensor。|
|OH_NN_ReturnCode OH_NNExecutor_RunSync(OH_NNExecutor *executor, NN_Tensor *inputTensor[], size_t inputCount, NN_Tensor *outputTensor[], size_t outputCount);|执行模型的同步推理。|
|void OH_NNCompilation_Destroy(OH_NNCompilation **compilation);|销毁模型编译实例。|
|OH_NN_ReturnCode OH_NNTensor_Destroy(NN_Tensor** tensor);|销毁输入输出Tensor。|
|void OH_NNExecutor_Destroy(OH_NNExecutor **executor);|销毁模型推理的执行器。|

## 开发步骤

以下为模型推理的主要开发步骤，具体实现请参见[SampleCode](https://gitcode.com/HarmonyOS_Samples/cannkit-samplecode-clientdemo-cpp)。

1. 准备模型和开发环境。
    
    - 准备om模型，可以通过tools_omg工具生成或从[Model Zoo](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-model-zoo)获取。
    - 下载并配置[DevEco Studio](https://developer.huawei.com/consumer/cn/deveco-studio/) 环境，确保可以正常开发和调试HarmonyOS应用。
    

2. [创建DevEco Studio项目](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-creating-a-project)。

3. 创建模型编译实例。
    
    调用[OH_NNCompilation_ConstructWithOfflineModelBuffer](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-neural-network-core-h#oh_nncompilation_constructwithofflinemodelbuffer)读取模型buffer，创建模型编译实例。或者通过调用[OH_NNCompilation_ConstructWithOfflineModelFile](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-neural-network-core-h#oh_nncompilation_constructwithofflinemodelfile)直接读取模型文件，创建模型编译实例。
    
4. 选择目标device。
    
    调用[OH_NNDevice_GetAllDevicesID](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-neural-network-core-h#oh_nndevice_getalldevicesid)，获取所有的设备ID，查找name为"HIAI_F"字段的设备ID，记录并通过[OH_NNCompilation_SetDevice](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-neural-network-core-h#oh_nncompilation_setdevice)设置到[步骤3](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-model-inference#li810206624)创建的编译实例中。
    

5. 执行模型编译。
    
    调用[OH_NNCompilation_Build](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-neural-network-core-h#oh_nncompilation_build)，传入[步骤3](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-model-inference#li810206624)创建的模型编译实例，即可执行模型编译，编译后的模型数据仍然保存在模型编译实例中。
    

6. 创建模型执行器。
    
    调用[OH_NNExecutor_Construct](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-neural-network-core-h#oh_nnexecutor_construct)，创建编译后模型对应的执行器实例。执行器创建完成后即可调用[OH_NNCompilation_Destroy](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-neural-network-core-h#oh_nncompilation_destroy)销毁模型编译实例。
    

7. 构造输入输出Tensor。
    
    调用[OH_NNExecutor_GetInputCount](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-neural-network-core-h#oh_nnexecutor_getinputcount)，查询输入的个数，通过[OH_NNExecutor_CreateInputTensorDesc](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-neural-network-core-h#oh_nnexecutor_createinputtensordesc)获取到对应索引的TensorDesc，根据该TensorDesc通过[OH_NNTensor_Create](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-neural-network-core-h#oh_nntensor_create)创建Tensor，即可向Tensor中写入实际数据。输出Tensor的构造与输入Tensor的构造过程一致。
    

8. 执行模型推理。
    
    调用[OH_NNExecutor_RunSync](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-neural-network-core-h#oh_nnexecutor_runsync)，执行模型的同步推理功能，模型的输出数据保存在outputTensors中。开发者可根据需要对输出数据做相应的处理以得到期望的内容。
    

9. 销毁实例。
    
    - 调用[OH_NNExecutor_Destroy](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-neural-network-core-h#oh_nnexecutor_destroy)，销毁创建的模型执行器实例。
    - 调用[OH_NNTensor_Destroy](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-neural-network-core-h#oh_nntensor_destroy)，销毁创建的输入输出Tensor。
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-whole-deployment-process "部署全流程")
# 异构

更新时间: 2025-12-16 16:27

## 概述

异构是CANN Kit提供的异构计算能力，能够使开发者App在华为平台上充分享受到硬件平台的计算加速性能，同时提供非华为硬件平台的模型计算兼容性和计算加速，使开发者App开发过程归一化，不再需要为不同硬件平台适配不同模型或者计算框架，减少App开发及维护的难度。

异构的原理如下图所示，指定OP1、OP2、OP5~OPn在CPU上进行推理，OP3、OP4在NPU上进行推理。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162757.39448178000510972009839417784305:50001231000000:2800:8A48C873A464068DD327FE3C9BDB4C9A4437B6405928F204403A4CF42187EE02.png)

实现异构可以通过在线调优方式，以下为在线调优参数设置接口，接口使用见[在线调优开发步骤](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-optimization#section79081331124811)。如要使用更丰富的设置和查询接口，请参见[API参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cannkit)。

**表1** 在线调优接口及功能介绍
|接口名|描述|
|:--|:--|
|OH_NN_ReturnCode HMS_HiAIOptions_SetTuningMode(OH_NNCompilation* compilation, HiAI_TuningMode tuningMode);|芯片调优模式配置。|
|OH_NN_ReturnCode HMS_HiAIOptions_SetTuningCacheDir(OH_NNCompilation* compilation, const char* cacheDir);|芯片调优缓存目录配置。|

## 在线调优开发步骤

1. 设置芯片调优模式。
    
    - 调用[OH_NNCompilation_ConstructWithOfflineModelFile](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-neural-network-core-h#oh_nncompilation_constructwithofflinemodelfile)，读取模型buffer，创建模型编译实例。
    - 调用[HMS_HiAIOptions_SetTuningMode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cannkit#hms_hiaioptions_settuningmode)向模型编译实例中设置芯片调优模式调优选项。
    

2. 调用[HMS_HiAIOptions_SetTuningCacheDir](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cannkit#hms_hiaioptions_settuningcachedir)向模型编译实例中设置芯片调优缓存目录调优选项。
3. 执行模型编译。
    
    设置好所需调优选项参数后，通过调用[OH_NNCompilation_Build](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-neural-network-core-h#oh_nncompilation_build)，传入[创建模型编译实例](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-model-inference#li810206624)，即可执行模型编译，编译成功则返回编译后的模型指针。后续流程同[模型推理](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-model-inference)。
    

## 在线调优示例说明

以下示例代码设置调优参数SetTuningMode及SetTuningCacheDir，实现在线调优。

1. #include "neural_network_runtime/neural_network_core.h"
2. #include "CANNKit/hiai_options.h"
3. // 基于离线模型文件创建编译实例
4. OH_NNCompilation* compilation = OH_NNCompilation_ConstructWithOfflineModelFile("test.om");
5. if (compilation == nullptr) {
6.     return; 
7. }
8. // 选择辅助调优模式
9. OH_NN_ReturnCode ret = HMS_HiAIOptions_SetTuningMode(compilation, HIAI_TUNING_MODE_HETER);
10. if (ret != OH_NN_SUCCESS ) {
11.     return;
12. }
13. // 设置辅助调优的缓存目录
14. const char* cacheDir = "/data/local/tmp";
15. ret = HMS_HiAIOptions_SetTuningCacheDir(compilation, cacheDir);
16. if (ret != OH_NN_SUCCESS ) {
17.     return;
18. }
19. // 编译模型
20. ret = OH_NNCompilation_Build(compilation);
21. if (ret != OH_NN_SUCCESS ) {
22.     return;
23. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-aipp-deployment "AIPP部署")
# 异构

更新时间: 2025-12-16 16:27

## 概述

异构是CANN Kit提供的异构计算能力，能够使开发者App在华为平台上充分享受到硬件平台的计算加速性能，同时提供非华为硬件平台的模型计算兼容性和计算加速，使开发者App开发过程归一化，不再需要为不同硬件平台适配不同模型或者计算框架，减少App开发及维护的难度。

异构的原理如下图所示，指定OP1、OP2、OP5~OPn在CPU上进行推理，OP3、OP4在NPU上进行推理。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162757.39448178000510972009839417784305:50001231000000:2800:8A48C873A464068DD327FE3C9BDB4C9A4437B6405928F204403A4CF42187EE02.png)

实现异构可以通过在线调优方式，以下为在线调优参数设置接口，接口使用见[在线调优开发步骤](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-optimization#section79081331124811)。如要使用更丰富的设置和查询接口，请参见[API参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cannkit)。

**表1** 在线调优接口及功能介绍
|接口名|描述|
|:--|:--|
|OH_NN_ReturnCode HMS_HiAIOptions_SetTuningMode(OH_NNCompilation* compilation, HiAI_TuningMode tuningMode);|芯片调优模式配置。|
|OH_NN_ReturnCode HMS_HiAIOptions_SetTuningCacheDir(OH_NNCompilation* compilation, const char* cacheDir);|芯片调优缓存目录配置。|

## 在线调优开发步骤

1. 设置芯片调优模式。
    
    - 调用[OH_NNCompilation_ConstructWithOfflineModelFile](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-neural-network-core-h#oh_nncompilation_constructwithofflinemodelfile)，读取模型buffer，创建模型编译实例。
    - 调用[HMS_HiAIOptions_SetTuningMode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cannkit#hms_hiaioptions_settuningmode)向模型编译实例中设置芯片调优模式调优选项。
    

2. 调用[HMS_HiAIOptions_SetTuningCacheDir](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cannkit#hms_hiaioptions_settuningcachedir)向模型编译实例中设置芯片调优缓存目录调优选项。
3. 执行模型编译。
    
    设置好所需调优选项参数后，通过调用[OH_NNCompilation_Build](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-neural-network-core-h#oh_nncompilation_build)，传入[创建模型编译实例](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-model-inference#li810206624)，即可执行模型编译，编译成功则返回编译后的模型指针。后续流程同[模型推理](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-model-inference)。
    

## 在线调优示例说明

以下示例代码设置调优参数SetTuningMode及SetTuningCacheDir，实现在线调优。

1. #include "neural_network_runtime/neural_network_core.h"
2. #include "CANNKit/hiai_options.h"
3. // 基于离线模型文件创建编译实例
4. OH_NNCompilation* compilation = OH_NNCompilation_ConstructWithOfflineModelFile("test.om");
5. if (compilation == nullptr) {
6.     return; 
7. }
8. // 选择辅助调优模式
9. OH_NN_ReturnCode ret = HMS_HiAIOptions_SetTuningMode(compilation, HIAI_TUNING_MODE_HETER);
10. if (ret != OH_NN_SUCCESS ) {
11.     return;
12. }
13. // 设置辅助调优的缓存目录
14. const char* cacheDir = "/data/local/tmp";
15. ret = HMS_HiAIOptions_SetTuningCacheDir(compilation, cacheDir);
16. if (ret != OH_NN_SUCCESS ) {
17.     return;
18. }
19. // 编译模型
20. ret = OH_NNCompilation_Build(compilation);
21. if (ret != OH_NN_SUCCESS ) {
22.     return;
23. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-aipp-deployment "AIPP部署")
# 内存零拷贝

更新时间: 2025-12-16 16:28

## 概述

对于GPU的纹理数据或模型的输入数据等已经存在于ION内存中的场景，就可以使用“内存零拷贝方式”，即将存放数据的ION内存封装为输入输出张量，直接进行推理，不需要进行输入张量和输出张量的数据拷贝，以便节省内存以及推理时间。

## 使用说明

对于零拷贝使用场景，在模型加载完成后，使用[OH_NNTensor_CreateWithFd](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-neural-network-core-h#oh_nntensor_createwithfd)，将ION内存封装为输入张量“input_tensor”，输出张量"output_tensor"，执行推理。

说明

若size为模型输出大小，对于输出张量，建议开发者申请ION内存的大小为![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162803.50405012837468628586749893651533:50001231000000:2800:C53CC10E7932E747516F654FF61EAC462E560A2B65B8BB0D90CB67C8FC120365.png)。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-debugging-and-optimization "维测调优")
# 内存零拷贝

更新时间: 2025-12-16 16:28

## 概述

对于GPU的纹理数据或模型的输入数据等已经存在于ION内存中的场景，就可以使用“内存零拷贝方式”，即将存放数据的ION内存封装为输入输出张量，直接进行推理，不需要进行输入张量和输出张量的数据拷贝，以便节省内存以及推理时间。

## 使用说明

对于零拷贝使用场景，在模型加载完成后，使用[OH_NNTensor_CreateWithFd](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-neural-network-core-h#oh_nntensor_createwithfd)，将ION内存封装为输入张量“input_tensor”，输出张量"output_tensor"，执行推理。

说明

若size为模型输出大小，对于输出张量，建议开发者申请ION内存的大小为![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162803.50405012837468628586749893651533:50001231000000:2800:C53CC10E7932E747516F654FF61EAC462E560A2B65B8BB0D90CB67C8FC120365.png)。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-debugging-and-optimization "维测调优")
# 配置项目NAPI

更新时间: 2025-12-16 16:28

编译HAP时，NAPI层的so需要编译依赖NDK中的libneural_network_core.so和libhiai_foundation.so。

## 头文件引用

按需引用[NNCore](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-neuralnetworkruntime)和[CANN Kit](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cannkit-hiai-aipp-param-8h)的头文件。

1. #include "neural_network_runtime/neural_network_core.h"
2. #include "CANNKit/hiai_options.h"

## 编写CMakeLists.txt

CMakeLists.txt示例代码如下。

1. # the minimum version of CMake.
2. cmake_minimum_required(VERSION 3.4.1)
3. project(CANNDemo)

4. set(NATIVERENDER_ROOT_PATH ${CMAKE_CURRENT_SOURCE_DIR})

5. include_directories(${NATIVERENDER_ROOT_PATH}
6.                     ${NATIVERENDER_ROOT_PATH}/include)

7. include_directories(${HMOS_SDK_NATIVE}/sysroot/usr/lib)
8. FIND_LIBRARY(cann_lib hiai_foundation)

9. add_library(entry SHARED Classification.cpp HIAIModelManager.cpp)

10. target_link_libraries(entry PUBLIC libace_napi.z.so
11.     libhilog_ndk.z.so
12.     librawfile.z.so
13.     ${cann-lib}
14.     libneural_network_core.so
15.     )

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-creating-a-project "创建项目")
# 配置项目NAPI

更新时间: 2025-12-16 16:28

编译HAP时，NAPI层的so需要编译依赖NDK中的libneural_network_core.so和libhiai_foundation.so。

## 头文件引用

按需引用[NNCore](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-neuralnetworkruntime)和[CANN Kit](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cannkit-hiai-aipp-param-8h)的头文件。

1. #include "neural_network_runtime/neural_network_core.h"
2. #include "CANNKit/hiai_options.h"

## 编写CMakeLists.txt

CMakeLists.txt示例代码如下。

1. # the minimum version of CMake.
2. cmake_minimum_required(VERSION 3.4.1)
3. project(CANNDemo)

4. set(NATIVERENDER_ROOT_PATH ${CMAKE_CURRENT_SOURCE_DIR})

5. include_directories(${NATIVERENDER_ROOT_PATH}
6.                     ${NATIVERENDER_ROOT_PATH}/include)

7. include_directories(${HMOS_SDK_NATIVE}/sysroot/usr/lib)
8. FIND_LIBRARY(cann_lib hiai_foundation)

9. add_library(entry SHARED Classification.cpp HIAIModelManager.cpp)

10. target_link_libraries(entry PUBLIC libace_napi.z.so
11.     libhilog_ndk.z.so
12.     librawfile.z.so
13.     ${cann-lib}
14.     libneural_network_core.so
15.     )

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-creating-a-project "创建项目")
# 集成模型

更新时间: 2025-12-16 16:28

模型的加载、编译和推理主要是在native层实现，应用层主要作为数据传递和展示作用。

模型推理之前需要对输入数据进行预处理以匹配模型的输入，同样对于模型的输出也需要做处理获取自己期望的结果。另外SDK中提供了设置模型编译和运行时的配置接口，开发者可根据实际需求选择使用接口。

本节阐述同步模式下单模型的使用，从流程上分别阐述每个步骤在应用层和native层的实现和调用。接口请参见[API参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cannkit)，示例请参见[SampleCode](https://gitcode.com/HarmonyOS_Samples/cannkit-samplecode-clientdemo-cpp)，本示例支持加载离线模型对图片中的物体进行分类，App运行效果图如下所示。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162810.25187197715296099308933139387096:50001231000000:2800:23011C10A9A3EDD963FCDFEDE91C7D81F3C0EE012EE0B5F1F83D96B8972C83DB.png "点击放大")

## 预置模型

为了让App运行时能够读取到模型文件和处理推理结果，需要先把离线模型和模型对应的结果标签文件预置到工程的“entry/src/main/resources/rawfile”目录中。

本示例所使用的离线模型的转换和生成请参考[Caffe模型转换](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-model-conversion-example#section329315242618)。

## 加载离线模型

在App应用创建时加载模型和读取结果标签文件。

1. 调用NAPI层的LoadModel函数，读取模型的buffer。
2. （可选）根据需要调用[HMS_HiAIOptions_SetOmOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cannkit#hms_hiaioptions_setomoptions)接口，打开维测功能（如Profiling）。
3. 把模型buffer传递给HIAIModelManager类的HIAIModelManager::LoadModelFromBuffer接口，该接口调用[OH_NNCompilation_ConstructWithOfflineModelBuffer](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-neural-network-core-h#oh_nncompilation_constructwithofflinemodelbuffer)创建模型的编译实例。
4. 设置模型的deviceID。
    
    1. size_t deviceID = 0;
    2. const size_t *allDevicesID = nullptr;
    3. uint32_t deviceCount = 0;
    4. // 获取所有已连接设备的ID
    5. OH_NN_ReturnCode ret = OH_NNDevice_GetAllDevicesID(&allDevicesID, &deviceCount);
    6. if (ret != OH_NN_SUCCESS || allDevicesID == nullptr) {
    7.     OH_LOG_ERROR(LOG_APP, "OH_NNDevice_GetAllDevicesID failed");
    8.     return OH_NN_FAILED;
    9. }
    10. // 获取设备名为HIAI_F的设备ID
    11. for (uint32_t i = 0; i < deviceCount; i++) {
    12.     const char *name = nullptr;
    13.     // 获取指定设备的名称
    14.     ret = OH_NNDevice_GetName(allDevicesID[i], &name);
    15.     if (ret != OH_NN_SUCCESS || name == nullptr) {
    16.         OH_LOG_ERROR(LOG_APP, "OH_NNDevice_GetName failed");
    17.         return OH_NN_FAILED;
    18.     }
    19.     if (std::string(name) == "HIAI_F") {
    20.         deviceID = allDevicesID[i];
    21.         break;
    22.     }
    23. }
    
    24. // modelData和modelSize为模型的内存地址和大小， compilation的创建可参考[CANN Kit Codelab](https://developer.huawei.com/consumer/cn/codelabsPortal/carddetails/tutorials_CANNKit-Image-classification)
    25. OH_NNCompilation *compilation = OH_NNCompilation_ConstructWithOfflineModelBuffer(modelData, modelSize); 
    26. // 设置编译器的设备id为HIAI_F
    27. ret = OH_NNCompilation_SetDevice(compilation, deviceID); 
    28. if (ret != OH_NN_SUCCESS) {
    29.     OH_LOG_ERROR(LOG_APP, "OH_NNCompilation_SetDevice failed");
    30.     return OH_NN_FAILED;
    31. }
    
5. 调用[OH_NNCompilation_Build](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-neural-network-core-h#oh_nncompilation_build)，执行模型编译。
6. 调用[OH_NNExecutor_Construct](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-neural-network-core-h#oh_nnexecutor_construct)，创建模型执行器。
7. 调用[OH_NNCompilation_Destroy](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-neural-network-core-h#oh_nncompilation_destroy)，释放模型编译实例。

上述流程可参见[SampleCode](https://gitcode.com/HarmonyOS_Samples/cannkit-samplecode-clientdemo-cpp)中“entry/src/main/cpp/Classification.cpp”文件中的LoadModel函数和“entry/src/main/cpp/HIAIModelManager.cpp”中的HIAIModelManager::LoadModelFromBuffer函数。

## 输入输出数据准备

1. 处理模型的输入，例如示例中模型的输入为1*3*227*227格式Float类型的数据，需要把输入的图片转成该格式后传递到NAPI层。
2. 创建模型的输入和输出Tensor，并把应用层传递的数据填充到输入的Tensor中。
    
    1. // 创建输入数据
    2. size_t inputCount = 0;
    3. std::vector<NN_Tensor*> inputTensors;
    4. OH_NN_ReturnCode ret = OH_NNExecutor_GetInputCount(executor, &inputCount); // 创建executor可参考[CANN Kit Codelab](https://developer.huawei.com/consumer/cn/codelabsPortal/carddetails/tutorials_CANNKit-Image-classification)
    5. if (ret != OH_NN_SUCCESS || inputCount != inputData.size()) { // inputData为开发者构造的输入数据
    6.     OH_LOG_ERROR(LOG_APP, "OH_NNExecutor_GetInputCount failed, size mismatch");
    7.     return OH_NN_FAILED;
    8. }
    9. for (size_t i = 0; i < inputCount; ++i) {
    10.     NN_TensorDesc *tensorDesc = OH_NNExecutor_CreateInputTensorDesc(executor, i); // 创建executor可参考[CANN Kit Codelab](https://developer.huawei.com/consumer/cn/codelabsPortal/carddetails/tutorials_CANNKit-Image-classification)
    11.     NN_Tensor *tensor = OH_NNTensor_Create(deviceID, tensorDesc); // deviceID的获取方式可参考[加载离线模型](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-integration-model#section1377917334217)的步骤3或者[CANN Kit Codelab](https://developer.huawei.com/consumer/cn/codelabsPortal/carddetails/tutorials_CANNKit-Image-classification)
    12.     if (tensor != nullptr) {
    13.         inputTensors.push_back(tensor);
    14.     }
    15.     OH_NNTensorDesc_Destroy(&tensorDesc);
    16. }
    17. if (inputTensors.size() != inputCount) {
    18.     OH_LOG_ERROR(LOG_APP, "input size mismatch");
    19.     DestroyTensors(inputTensors); // DestroyTensors为释放tensor内存操作函数，具体实现可参考[CANN Kit Codelab](https://developer.huawei.com/consumer/cn/codelabsPortal/carddetails/tutorials_CANNKit-Image-classification)
    20.     return OH_NN_FAILED;
    21. }
    
    22. // 初始化输入数据
    23. for (size_t i = 0; i < inputTensors.size(); ++i) {
    24.     void *data = OH_NNTensor_GetDataBuffer(inputTensors[i]);
    25.     size_t dataSize = 0;
    26.     OH_NNTensor_GetSize(inputTensors[i], &dataSize);
    27.     if (data == nullptr || dataSize != inputData[i].size()) { // inputData为模型的输入数据，使用方式可参考[CANN Kit Codelab](https://developer.huawei.com/consumer/cn/codelabsPortal/carddetails/tutorials_CANNKit-Image-classification)
    28.         OH_LOG_ERROR(LOG_APP, "invalid data or dataSize");
    29.         return OH_NN_FAILED;
    30.     }
    31.     memcpy(data, inputData[i].data(), inputData[i].size()); // inputData为模型的输入数据，使用方式可参考[CANN Kit Codelab](https://developer.huawei.com/consumer/cn/codelabsPortal/carddetails/tutorials_CANNKit-Image-classification)
    32. }
    
    33. // 创建输出数据，与输入数据的创建方式类似
    34. size_t outputCount = 0;
    35. std::vector<NN_Tensor*> outputTensors;
    36. ret = OH_NNExecutor_GetOutputCount(executor, &outputCount); // 创建executor可参考[CANN Kit Codelab](https://developer.huawei.com/consumer/cn/codelabsPortal/carddetails/tutorials_CANNKit-Image-classification)
    37. if (ret != OH_NN_SUCCESS) {
    38.     OH_LOG_ERROR(LOG_APP, "OH_NNExecutor_GetOutputCount failed");
    39.     DestroyTensors(inputTensors); // DestroyTensors为释放tensor内存操作函数，具体实现可参考[CANN Kit Codelab](https://developer.huawei.com/consumer/cn/codelabsPortal/carddetails/tutorials_CANNKit-Image-classification)
    40.     return OH_NN_FAILED;
    41. }
    42. for (size_t i = 0; i < outputCount; i++) {
    43.     NN_TensorDesc *tensorDesc = OH_NNExecutor_CreateOutputTensorDesc(executor, i); // 创建executor可参考[CANN Kit Codelab](https://developer.huawei.com/consumer/cn/codelabsPortal/carddetails/tutorials_CANNKit-Image-classification)
    44.     NN_Tensor *tensor = OH_NNTensor_Create(deviceID, tensorDesc); // deviceID的获取方式可参考[加载离线模型](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-integration-model#section1377917334217)的步骤3或者[CANN Kit Codelab](https://developer.huawei.com/consumer/cn/codelabsPortal/carddetails/tutorials_CANNKit-Image-classification)
    45.     if (tensor != nullptr) {
    46.         outputTensors.push_back(tensor);
    47.     }
    48.     OH_NNTensorDesc_Destroy(&tensorDesc);
    49. }
    50. if (outputTensors.size() != outputCount) {
    51.     DestroyTensors(inputTensors); // DestroyTensors为释放tensor内存操作函数，具体实现可参考[CANN Kit Codelab](https://developer.huawei.com/consumer/cn/codelabsPortal/carddetails/tutorials_CANNKit-Image-classification)
    52.     DestroyTensors(outputTensors); // DestroyTensors为释放tensor内存操作函数，具体实现可参考[CANN Kit Codelab](https://developer.huawei.com/consumer/cn/codelabsPortal/carddetails/tutorials_CANNKit-Image-classification)
    53.     OH_LOG_ERROR(LOG_APP, "output size mismatch");
    54.     return OH_NN_FAILED;
    55. }
    

上述流程可参见[SampleCode](https://gitcode.com/HarmonyOS_Samples/cannkit-samplecode-clientdemo-cpp)中“entry/src/main/cpp/Classification.cpp”文件中的InitIOTensors函数和“entry/src/main/cpp/HiAiModelManager.cpp”中的HIAIModelManager::InitIOTensors函数。

## 同步推理离线模型

说明

如果不更换模型，则首次编译加载完成后可多次推理，即一次编译加载，多次推理。

调用[OH_NNExecutor_RunSync](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-neural-network-core-h#oh_nnexecutor_runsync)，完成模型的同步推理。

可参见[SampleCode](https://gitcode.com/HarmonyOS_Samples/cannkit-samplecode-clientdemo-cpp)中“entry/src/main/cpp/Classification.cpp”文件中的RunModel函数和“entry/src/main/cpp/HiAiModelManager.cpp”中的HIAIModelManager::RunModel函数。

## 模型输出后处理

1. 调用[OH_NNTensor_GetDataBuffer](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-neural-network-core-h#oh_nntensor_getdatabuffer)，获取输出的Tensor，在输出Tensor中会得到模型的输出数据。
2. 对输出数据进行相应的处理可得到期望的结果。
    
    例如本示例demo中模型的输出是1000个label的概率，期望得到这1000个结果中概率最大的三个标签。
    
3. [销毁申请的Tensor资源和执行器实例](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-model-inference#li172172195213)。

上述流程可参见[SampleCode](https://gitcode.com/HarmonyOS_Samples/cannkit-samplecode-clientdemo-cpp)中“entry/src/main/cpp/Classification.cpp”文件中的GetResult、UnloadModel函数和“entry/src/main/cpp/HiAiModelManager.cpp”中的HIAIModelManager::GetResult、HIAIModelManager::UnloadModel函数。

说明

开发者可根据需要自行设置模型推理优先级。使用[OH_NNCompilation_SetPriority](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-neural-network-core-h#oh_nncompilation_setpriority)接口，默认值为OH_NN_PRIORITY_NONE，本接口应在模型推理前调用。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cannkit-compiling-the-napi "配置项目NAPI")