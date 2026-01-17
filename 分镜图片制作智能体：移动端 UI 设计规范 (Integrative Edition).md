**分镜图片制作智能体：移动端 UI 设计规范 (Integrative Edition)**

**1.** **整合总览 (Overview)**

本规范文档整合了 “分镜图片制作智能体” 的所有核心设计资产，旨在构建一套统一、精致且高可用的移动端设计系统。文档涵盖全局设计令牌 (Design Tokens)、多智能体协作的完整交互逻辑、关键页面的高保真规范以及最终交付的验收标准。

|   |   |
|---|---|
|\|   \|<br>\|---\|<br>\|**整合范围**<br><br>· **视觉核心：** 统一色彩、字体、圆角与动效规范。<br><br>· **交互逻辑：** 多智能体协作状态流与反馈机制。<br><br>· **页面资产：** 10+ 关键页面的高保真还原图。\||\|   \|<br>\|---\|<br>\|**交付目标**<br><br>· **一致性：** 确保从 Token 到 Component 的像素级还原。<br><br>· **可用性：** 触控友好，符合 WCAG 无障碍标准。<br><br>· **落地性：** 提供明确的开发参数与异常处理策略。\||

**2.** **设计令牌 (Design Tokens)**

全局视觉语言的基础定义。开发实现时需严格绑定以下 Token，严禁硬编码 (Hard-coding)。

**色彩系统 (Color System)**

|   |   |   |
|---|---|---|
|Token|Value|Usage & Semantics|
|**Primary**|**#EB2F96**|品牌主色。用于主按钮、选中状态 (Active)、当前进行中的步骤。|
|**Completed**|**#8B5CF6**|完成状态。**注意：**替代传统的绿色，用于已完成步骤的勾选与进度条。|
|**Warning**|**#FFA940**|警告状态。用于一致性问题提示、非阻塞性错误。|
|**Upcoming/Idle**|#9CA3AF|未开始或空闲状态。用于后续步骤图标、禁用态文本。|
|**Text-Primary**|#333333|主要文本。对比度 > 10:1。|
|**Background**|#F5F5F5|页面底色。|

**排版与界面物理 (Typography & Physics)**

|   |   |
|---|---|
|\|   \|<br>\|---\|<br>\|**字体层级**<br><br>· **H1 Page Title:** 24px / Bold<br><br>· **H2 Section:** 18px / Semibold<br><br>· **Body:** 16px / Regular (阅读舒适区)<br><br>· **Caption:** 12px / Regular (辅助说明)\||\|   \|<br>\|---\|<br>\|**界面物理属性**<br><br>· **圆角 (Radius):** 12px (卡片/按钮), 16px (抽屉顶部)。<br><br>· **阴影 (Shadow):** y=6, blur=18pt (常规); y=10, blur=24pt (浮层)。<br><br>· **触控 (Touch):** 交互热区 **≥ 48px**。<br><br>· **动效 (Motion):** 300ms ease-out (淡入淡出)。\||

**3.** **多智能体协作：交互逻辑与状态参数**

本章节定义了用户与多智能体系统互动的核心机制。系统通过明确的步骤导航与状态反馈，降低用户对后台复杂任务的认知负荷。

**步骤导航与状态流 (Stepper Logic)**

|   |   |
|---|---|
|顶部导航条 (Agent Strip) 是任务进度的唯一真值来源。<br><br>· **流程节点：** 脚本理解 › 分镜生成 › 角色一致性 › AI 绘画 › 导出。<br><br>· **独立图标：** 每个步骤拥有独立的圆形 Agent 图标，非通用圆点。<br><br>· **交互路由：** 点击任意节点（含未开始）可跳转至对应详情页。当前所在步骤高亮显示。<br><br>· **进度反馈：** 导航条下方附带 2px 进度条；右侧显示 “x/y” 计数胶囊。<br><br>State<br><br>Visual<br><br>Action<br><br>**Running**<br><br>#EB2F96 (Solid)<br><br>暂停 / 取消<br><br>**Completed**<br><br>#8B5CF6 (Check)<br><br>查看 / 重试<br><br>**Idle**<br><br>#9CA3AF (Outline)<br><br>点击预设<br><br>**Blocked**<br><br>#FFA940 (Alert)<br><br>人工干预|![](file:///C:\Users\13632\AppData\Local\Temp\ksohtml2996\wps1.png) <br><br>多智能体协作：步骤导航与状态映射|

**消息映射与时间线**

时间线卡片明确标识 “谁在说话”。

· **Agent 映射：** System 消息左侧**必须**显示当前步骤对应的彩色 Agent 图标（如：分镜生成步骤对应粉色胶卷图标）。

· **加载状态：** 进行中的任务显示骨架屏与 “处理中...” 微交互，消除等待焦虑。

**4.** **页面：首页 (Home)**

|   |   |
|---|---|
|首页经过功能重排，强调效率与引导。<br><br>· **顶部导航 (Tabs):** 首页 (高亮) / 分镜 / 参数 / 导出 / 检查 / 角色库。<br><br>· **快捷操作区：** 首屏顶部展示 “新建分镜”、“导入脚本”、“一键生成” 三大高频入口。<br><br>· **内容流顺序：** 快捷模板 (横滑) → 分镜列表 (纵向) → 任务队列 → 新手教程。<br><br>· **卡片细节：** 分镜卡片右侧集成 16px 一致性状态点（红/黄/绿）。|![](file:///C:\Users\13632\AppData\Local\Temp\ksohtml2996\wps2.png) <br><br>首页：功能重排版|

**5.** **页面：分镜详情 (Detail)**

|   |   |
|---|---|
|聚焦单镜头精修，支持深度编辑。<br><br>· **预览区：** 16:9 宽幅 Banner，集成播放控件。<br><br>· **表单控件：** 标题（H2 Bold）、描述域（支持长按粘贴）、标签云 (Chips)。<br><br>· **场景选择：** 下拉菜单支持快速切换预设场景。<br><br>· **底部固定：** “保存” (Primary Button) 与 “应用到所有” (Checkbox)。|![](file:///C:\Users\13632\AppData\Local\Temp\ksohtml2996\wps3.png) <br><br>分镜详情页|

**6.** **页面：AI 参数设置 (Parameters)**

|   |   |
|---|---|
|复杂的参数配置通过层级化梳理。<br><br>· **分组导航：** 顶部 Segment Control (基本/风格/高级)。<br><br>· **交互组件：** 强度滑块 (0-100，支持步进)，风格预设 (横向图片流)。<br><br>· **操作抽屉：** 底部浮层提供应用与重置操作，避免跳出页面。|![](file:///C:\Users\13632\AppData\Local\Temp\ksohtml2996\wps4.png) <br><br>AI 参数设置页|

**7.** **页面：导出与完成总结 (Export)**

|   |   |
|---|---|
|清晰的交付流程与最终反馈。<br><br>· **格式选择：** PNG/PDF/ZIP 格式卡片，点击展开分辨率选项。<br><br>· **导出范围：** 单选组 (Radio Group) 切换 “全部导出” 或 “仅选中”。<br><br>· **完成总结：** 导出成功后展示 Summary 页，顶部显示紫色 (#8B5CF6) 大勾选徽标与 100% 进度条。|\|   \|   \|<br>\|---\|---\|<br>\|![](file:///C:\Users\13632\AppData\Local\Temp\ksohtml2996\wps5.png) <br><br>导出设置\|![](file:///C:\Users\13632\AppData\Local\Temp\ksohtml2996\wps6.png) <br><br>完成总结页\||

**8.** **页面：一致性检查 (Consistency)**

|   |   |
|---|---|
|质量控制仪表盘。<br><br>· **状态总览：** 顶部展示通过率 %。问题按 “警告 (Yellow)” 与 “错误 (Red)” 分类。<br><br>· **快速修复：** 错误项右侧提供 “Fix” 按钮，支持一键应用建议。<br><br>· **筛选 Chips：** 快速过滤显示 “仅看问题项”。|![](file:///C:\Users\13632\AppData\Local\Temp\ksohtml2996\wps7.png) <br><br>一致性检查报告|

**9.** **页面：角色管理库 (Role Library)**

|   |   |
|---|---|
|资产复用与管理中心。<br><br>· **网格布局：** 双列卡片，圆形大头像强调角色特征。<br><br>· **筛选体系：** 性别 / 年龄 / 风格 组合筛选。<br><br>· **空态处理：** 加载中显示骨架屏 (Skeleton)，无数据展示插画引导新建。|![](file:///C:\Users\13632\AppData\Local\Temp\ksohtml2996\wps8.png) <br><br>角色库|

**10.** **页面：工作过程 (Work Process)**

|   |   |
|---|---|
|多智能体实时协作视图。<br><br>· **全景导航：** 顶部完整展示 5 步流程，当前步骤 (AI 绘画) 粉色高亮。<br><br>· **消息流：** 中央区域实时刷出 System 进度日志与生成结果图。<br><br>· **FAB 与抽屉：** 右下角悬浮按钮呼出 “多智能体面板”，底部抽屉承载用户输入 (Chips + TextField)。|![](file:///C:\Users\13632\AppData\Local\Temp\ksohtml2996\wps9.png) <br><br>工作过程与输入抽屉|

**11.** **弹窗与底部抽屉规范 (Modals & Sheets)**

所有浮层容器必须遵循统一的视觉物理规范：白色背景、顶部 16px 圆角、y=10 阴影。

|   |   |   |
|---|---|---|
|![](file:///C:\Users\13632\AppData\Local\Temp\ksohtml2996\wps10.png) <br><br>设置弹窗|![](file:///C:\Users\13632\AppData\Local\Temp\ksohtml2996\wps11.png) <br><br>风格选择抽屉|![](file:///C:\Users\13632\AppData\Local\Temp\ksohtml2996\wps12.png) <br><br>分类 Action Sheet|

**12.** **附录：设计图索引**

本次交付的核心高保真设计图清单。

|   |   |
|---|---|
|文件名|用途|
|mobile_home_reordered_v3.jpeg|首页 (功能重排版)|
|mobile_detail_v2.jpeg|分镜详情页|
|workflow_process_agent_icons_non.jpeg|多智能体协作流程图|
|workflow_complete_summary_edit.jpeg|任务完成总结页|
|redesign_settings_modal_edit.jpeg|通用设置弹窗规范|

**13.** **验收标准 (Acceptance Criteria)**

|   |
|---|
|**交付验收清单**<br><br>· **视觉一致性：** 所有圆角统一为 12px/16px，阴影严格执行 Token 参数。<br><br>· **色彩执行：** 确认 "完成" 状态为 Lavender #8B5CF6，严禁使用系统默认绿色。<br><br>· **多智能体反馈：** 步骤导航必须与当前 Agent 图标/颜色 (Pink) 实时同步。<br><br>· **性能指标：** 核心路径（首页→导出）点击数 ≤ 3；页面 TTI ≤ 1.5s。<br><br>· **异常处理：** 弱网环境下必须支持断点续传与重试队列。|