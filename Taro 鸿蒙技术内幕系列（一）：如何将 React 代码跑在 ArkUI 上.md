# Taro 鸿蒙技术内幕系列（一）：如何将 React 代码跑在 ArkUI 上

京东零售：朱鸣辉 Taro社区

 _2024年10月22日 19:33_ _广东_

![图片](https://mmbiz.qpic.cn/mmbiz_png/g9uU4FY8hdcvgUbvSvibKucAJeGOMic3ojGV41J7bp4eQ0IcY0levPIiaG6QeoxEKoMgbTcFjxI4opl0dUhBaUZicQ/640?wx_fmt=png&from=appmsg&tp=wxpic&wxfrom=5&wx_lazy=1#imgIndex=0)

基于 Taro 打造的京东鸿蒙 APP 已跟随鸿蒙 Next 系统公测，本系列文章将深入解析 Taro 如何实现使用 React 开发高性能鸿蒙应用的技术内幕  

  

# **背景**

随着鸿蒙操作系统的快速发展，开发者们期待将现有跨平台应用迁移到鸿蒙平台。Taro作为一个流行的跨平台开发框架，其支持鸿蒙系统的可能性引起了广泛关注。

然而，鸿蒙系统采用全新的ArkUI框架作为原生UI开发方案，与Taro原本支持的平台存在显著差异。将Taro的React开发模式与ArkUI的声明式UI开发范式进行有效对接成为了一个技术难题。

本文将探讨Taro框架如何通过创新方案实现React代码在ArkUI上的运行。我们将解析Taro的运行时原理，剖析其如何将React组件转换为ArkUI可识别的结构，以及相关技术挑战和解决方案。  

  

# **Taro运行时原理介绍**

为了理解Taro适配ArkUI的核心机制，我们首先需要深入了解Taro的运行时原理。Taro通过巧妙的设计，将React代码转换为各平台可执行的形式，其中包括对鸿蒙平台的适配。下面将详细介绍 Taro 是如何将 React 代码转换为ArkUI可执行的形式，以及节点转换的流程细节。![图片](https://mmbiz.qpic.cn/mmbiz_png/g9uU4FY8hdcvgUbvSvibKucAJeGOMic3ojbiakSGmAicJuvEYyKqsfwmyCJiaHA2Z2DlO6aNnvktsvR4MBVicmlic8d4g/640?wx_fmt=png&from=appmsg&tp=wxpic&wxfrom=5&wx_lazy=1#imgIndex=1)

## 1. 从 React 到 Taro

### React 跨平台的秘诀

在 Taro 的运行时中，首先执行的是开发者编写的 React 业务代码。这些代码定义了业务应用的结构、逻辑和状态管理。那么既然要对接React，那肯定先得了解它的核心架构，React是怎么运作的：﻿

![图片](https://mmbiz.qpic.cn/mmbiz_png/g9uU4FY8hdcvgUbvSvibKucAJeGOMic3ojicU9h2QnvEEpGdpDR3eT4AeKopTnNVJsxKnH83Yu1WMdtibTsYSIrjbw/640?wx_fmt=png&from=appmsg&tp=wxpic&wxfrom=5&wx_lazy=1#imgIndex=2)了解了React的基本架构后，我们可以清晰地看到，`**Renderer**` 作为渲染器，负责将React的虚拟节点操作最终映射到相应的平台上。例如，`react-dom`将这些操作对接到浏览器上，而`react-native`则将其对接到iOS或Android平台。这种设计使得React能够适配不同的运行环境。﻿

![图片](https://mmbiz.qpic.cn/mmbiz_png/g9uU4FY8hdcvgUbvSvibKucAJeGOMic3ojInHjFMs2JAibe1zK3grJbvEiaxgZgct3pyfHOmpqf3iaz1WgUYrPYToRw/640?wx_fmt=png&from=appmsg&tp=wxpic&wxfrom=5&wx_lazy=1#imgIndex=3)

正是基于这种思路，Taro 团队设计了 **Taro Renderer**。这个渲染器充当了 React 与 Taro 虚拟节点树之间的桥梁，使得 React 的操作可以被转换为 Taro 的中间表示。  

通过实现 Taro Renderer 生成 Taro 虚拟节点树﻿

![图片](https://mmbiz.qpic.cn/mmbiz_png/g9uU4FY8hdcvgUbvSvibKucAJeGOMic3oj2ibZPogyUzTx1O8jC15KicztghmRIa6659sMN0U0InxGuFFZrqB1UnCQ/640?wx_fmt=png&from=appmsg&tp=wxpic&wxfrom=5&wx_lazy=1#imgIndex=4)

﻿﻿HostConfig接口实现

﻿要实现Taro的Renderer，我们需要实现`ReactReconciler`所需的 `hostConfig` 接口。这个接口定义了一系列方法，用于创建、更新和管理渲染目标平台的元素。以下是一些关键的 hostConfig 方法：

•**createElement：**创建ArkUI对应的元素。

•**createTextInstance**：创建文本节点。

•**appendChild：**将子元素添加到父元素。

•**removeChild：**从父元素中移除子元素。

•**insertBefore：**在指定位置插入元素。

•**commitUpdate：**更新元素属性。

通过实现这些方法，**Taro Rendere**r 能够将 **React 的操作转换为 Taro 虚拟节点树的相应操作**。这个虚拟节点树是 Taro 实现跨平台的核心，它为不同平台的渲染提供了统一的中间表示。

```
// 部分HostConfig接口实现的代码
```

## 2. 从 Taro 到 ArkUI

在将 Taro 虚拟节点树转换为 ArkUI 的过程中，我们需要进行几个关键步骤：﻿

![图片](data:image/svg+xml,%3C%3Fxml%20version='1.0'%20encoding='UTF-8'%3F%3E%3Csvg%20width='1px'%20height='1px'%20viewBox='0%200%201%201'%20version='1.1'%20xmlns='http://www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate\(-249.000000,%20-126.000000\)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

﻿﻿Taro Element转换 ArkUI过程

首先，我们需要在 ArkUI 层面**实现一套与 Taro 组件对应的组件库**。这个步骤至关重要，因为它建立了 Taro 组件和 ArkUI 组件之间的映射关系。例如，我们需要为 Taro 的 `View`、`Text`、`Image` 等基础组件创建对应的 ArkUI 组件。这样，当我们遍历 Taro 虚拟节点树时，就能找到每个节点在 ArkUI 中的对应实现。

在节点映射的过程中，我们注意到 Taro 虚拟节点树与实际 ArkUI 视图结构存在差异。这些差异主要体现在以下几个方面：

•**复合组件结构：**某些 Taro 组件在 ArkUI 中可能需要多个组件配合实现。例如，ScrollView 组件在 ArkUI 中可能需要一个 Scroll 节点搭配一个 Stack 来实现完整功能。

•**层级位置调整：**一些特殊定位的节点（如 Fixed 定位的元素）在最终渲染时的位置可能与其在虚拟节点树中的层级不一致。这需要在生成渲染树时进行特殊处理。

•**平台特定组件：**某些 Taro 组件可能需要使用 ArkUI 特有的组件或布局方式来实现，这要求我们在转换过程中进行适当的调整和映射。﻿

![图片](data:image/svg+xml,%3C%3Fxml%20version='1.0'%20encoding='UTF-8'%3F%3E%3Csvg%20width='1px'%20height='1px'%20viewBox='0%200%201%201'%20version='1.1'%20xmlns='http://www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate\(-249.000000,%20-126.000000\)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

﻿﻿因此，在生成渲染树时，我们需要一个更复杂的转换过程，不仅要考虑简单的一对一映射，还要处理这些结构性的差异，确保最终生成的 ArkUI 组件树能够正确反映预期的视图结构和布局。**因此，在Taro > ArkUI的节点对接中，我们需要维护一棵 Render Tree，用于做中间的桥梁。**

### 1. 根据组件类型 创建 Taro Element

在创建 Taro Element 的过程中，我们根据组件的类型来实例化相应的 Taro 元素。这一步骤是将 React 组件转换为 Taro 内部表示的关键。

```
// 根据组件类型创建对应的Taro节点
```

### 2. Taro Element 创建 Taro RenderNode

在创建完 Taro Element 之后，下一步是将其转换为 Taro RenderNode。这个过程是将 Taro 的内部表示进一步转化为更接近 ArkUI 结构的渲染节点。

```
// 创建 Taro RenderNode
```

### 3. Taro RenderNode 创建 ArkUI Node

最后一步是将 Taro RenderNode 转换为实际的 ArkUI 节点。这个过程涉及到直接与 ArkUI 的底层 API 交互，创建和配置 ArkUI 的原生节点。实现了从 Taro 的渲染节点到 ArkUI 实际可渲染节点的最终转换。

```
// 创建 ArkUI Node
```

通过这三个步骤，我们在 C++ 层面成功实现了 React 组件结构到 ArkUI 原生组件结构的映射。这一过程使 Taro 应用能够在鸿蒙系统上准确地渲染和运行，为跨平台开发提供了有力支持。

# **总结**

最后总结下，本文探讨了Taro框架如何将React代码成功运行在鸿蒙系统的ArkUI上。这个过程主要分为两个关键部分：﻿

![图片](data:image/svg+xml,%3C%3Fxml%20version='1.0'%20encoding='UTF-8'%3F%3E%3Csvg%20width='1px'%20height='1px'%20viewBox='0%200%201%201'%20version='1.1'%20xmlns='http://www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate\(-249.000000,%20-126.000000\)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

﻿﻿React > ArkUI 架构图

## **1. Taro对接React**

Taro通过实现自定义的Renderer来对接React。这个Renderer包含了一系列方法，如createInstance、commitUpdate等，用于将React的操作转换为Taro虚拟节点树的操作。这个虚拟节点树是Taro实现跨平台的核心，为不同平台的渲染提供了统一的中间表示。

## **2. Taro对接ArkUI**

Taro通过自定义Renderer将React操作转换为虚拟节点树，然后通过三步转换过程将其映射到ArkUI结构。这个过程涉及Taro Element、Taro RenderNode和ArkUI Node这三棵树的维护，主要通过这三个流程步骤实现：

1.**创建Taro Element：**这一步将React组件转换为Taro内部表示。

2.**创建Taro RenderNode：**将Taro的内部表示进一步转化为更接近ArkUI层级结构的渲染节点。

3.**创建ArkUI Node：**最后一步是将Taro RenderNode转换为实际的ArkUI节点，直接与ArkUI的底层API交互。

通过这种方式，Taro成功地将React组件结构映射到ArkUI原生组件结构，使得Taro应用能够在鸿蒙系统上准确地渲染和运行，同时也为跨平台开发提供了有力支持。  
  

# **系列往期精选：**

﻿《京东鸿蒙上线前瞻——使用 Taro 打造高性能原生应用》﻿

![图片](data:image/svg+xml,%3C%3Fxml%20version='1.0'%20encoding='UTF-8'%3F%3E%3Csvg%20width='1px'%20height='1px'%20viewBox='0%200%201%201'%20version='1.1'%20xmlns='http://www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate\(-249.000000,%20-126.000000\)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

扫一扫，加入技术交流群