# 使用AI自动生成n8n工作流（基于GLM-4.7与上下文学习）

## 教程概述

本教程提供一套系统化的方法，利用 AI 模型（如 GLM - 4.7）自动生成 n8n 工作流，减少手动学习成本。内容基于最佳实践和可验证的步骤，确保可落地执行。教程将涵盖环境配置、Skill 创建、工作流生成和测试验证，并引用可靠资源补充细节。

![AI工作流生成架构图](https://s.coze.cn/image/bDOhhJOu4og/)

## 准备工作

### 所需工具与账户

- **智谱 GLM 账户**：注册 [https://open.bigmodel.cn/](https://open.bigmodel.cn/)，获取 API Key（免费 tier 可用）。
    
- **Claude Code 工具**：下载并安装 Claude Code（一个支持 AI 代码生成的本地工具，从官网获取）。
    
- **n8n 实例**：本地安装 n8n 或使用云版（如 n8n.cloud），用于导入生成的工作流。
    
- **可选资源（用于扩展验证）**
    
    - n8n 工作流模板库：[https://e3eb070d.n8n-workflows-bxc.pages.dev/](https://e3eb070d.n8n-workflows-bxc.pages.dev/)（搜索 5000 + 模板参考）。
        
    - 本地模型部署：通过 cursorweb2api 等工具免费使用多模型（如 GPT - 5、Claude - 4.5），作为 GLM - 4.7 的备选。
        

### 核心概念

- **上下文学习（Context Learning）**：AI 通过分析现有工作流模板来生成新内容，避免凭空创造。
    
- **n8n 工作流结构**：由节点（nodes）和连接（connections）组成的 JSON 文件，支持自动化任务。
    

## 步骤 1：配置 AI 模型环境

目标：将 Claude Code 的底层模型切换为 GLM - 4.7，以利用其代码生成能力。

### 操作流程

1. **打开终端，运行以下命令创建 Claude Code 配置文件**：
    

```bash
mkdir -p ~/.claude
cat > ~/.claude/settings.json << EOF
{
  "env": {
    "ANTHROPIC_AUTH_TOKEN": "您的智谱 API_KEY",
    "ANTHROPIC_BASE_URL": "https://open.bigmodel.cn/api/anthropic",
    "ANTHROPIC_DEFAULT_SONNET_MODEL": "glm-4.7-coding-preview",
    "ANTHROPIC_DEFAULT_OPUS_MODEL": "glm-4.7-coding-preview",
    "ANTHROPIC_DEFAULT_HAIKU_MODEL": "glm-4.7-coding-preview"
  }
}
EOF
```

- 替换"您的智谱 API_KEY"为实际 Key。
    

![Claude Code配置界面截图](https://s.coze.cn/image/tstRs9KHqiI/)

2. **重启 Claude Code**，检查界面底部是否显示模型为 glm - 4.7 - coding - preview。
    

说明：GLM - 4.7 在代码任务中表现优异（如 LiveCodeBench v6 得分 84.9），配置后可直接用于生成结构化代码。

## 步骤 2：构建 n8n 工作流生成 Skill

Skill 是 Claude Code 的功能模块，用于定义 AI 的任务逻辑。本节创建一个 Skill，使 AI 能基于模板生成工作流。

### 收集参考工作流模板

首先，让 AI 自动下载现有 n8n 模板作为学习素材：

- 在 Claude Code 中输入以下提示词（使用 Playwright 工具）：  
    调用 playwright mcp 到 [https://n8n.io/workflows/](https://n8n.io/workflows/) 执行以下操作：
    

1. 搜索关键词（如"video generation"或"tiktok"）。
    
2. 在结果页面选择 5 - 10 个相关工作流。
    
3. 点击"Use for Free"按钮，复制 JSON 代码到本地文件，保存为单独 JSON 文件。  
    文件命名与网页标题一致，存储到文件夹“n8n_references”。
    

- 成功后，本地生成 n8n_references 文件夹，包含多个 JSON 模板文件。
    

### 创建 Skill 文件

- 在项目根目录下创建文件夹结构：.claude/skills/n8n - generator/。
    
- 在该文件夹内创建 SKILL.md 文件，内容如下（基于 AI 工作流设计最佳实践）：
    

```markdown
# n8n 工作流生成专家 Skill
你是一个 n8n 自动化架构师，根据用户需求生成可直接导入的工作流 JSON。

## 规则
1. 输入处理：解析用户自然语言需求，拆解为输入源、处理逻辑、输出端。
2. 上下文学习：优先参考本地`n8n_references`文件夹中的模板结构，避免凭空创造。
3. 输出要求：
   - 生成纯净的 n8n 工作流 JSON，包含完整的`nodes`和`connections`。
   - 同时生成 Markdown 文档，说明节点功能、配置参数和错误处理。
   - 使用 Sticky Notes 分区，确保工作流可读性。

## 示例
用户输入："创建一个每天定时备份 Google Sheets 到云盘的工作流"
- AI 需分析：触发器（定时）、输入（Google Sheets）、处理（备份）、输出（云盘）。
- 参考类似模板，生成 JSON 和文档。
```

- 保存文件后，在 Claude Code 中输入/skills，确认 Skill 已加载（显示绿灯标识）。
    

![Claude Code技能加载状态截图](https://p11-doubao-search-sign.byteimg.com/isp-i18n-media/image/712e1ec97bab01dc73bf471689381df2~tplv-be4g95zd3a-image.jpeg?rk3s=542c0f93&x-expires=1782401248&x-signature=OHeOLb6P4IU6%2BIx5uuH8VFxGlNc%3D)

## 步骤 3：生成工作流示例

以“自动生成 TikTok 带货视频”为例，演示完整流程。

### 操作流程

1. **调用 Skill**：在 Claude Code 中输入：  
    调用 n8n - generator，创建一个 n8n 工作流，需求：
    

- 定时触发：每天 23:00 运行。
    
- 输入：从 Google Sheets 读取状态为“未完成”的记录（含产品图 URL 和拍摄风格）。
    
- 处理：循环每个产品图，调用 Veo 3.1 API 生成视频。
    
- 输出：视频上传到 Google Drive，并更新表格状态为“已完成”。
    

2. **AI 生成输出**：
    

- 工作流 JSON 文件（如 tiktok_video_generator.json）：符合 n8n Schema，可直接导入。
    
- Markdown 文档：详细说明架构，例如：
    

```markdown
# 工作流文档
- 触发节点：Schedule Trigger (Cron: 0 23 * * *)
- 核心逻辑：Loop 节点处理每条记录，HTTP 节点调用 API。
- 错误处理：IF 节点检查 API 响应，失败时重试。
```

3. **导入 n8n 测试**：
    

- 在 n8n 界面中，点击"Import from File"，上传 JSON 文件。
    
- 检查节点连接是否完整，如定时器、循环逻辑和 API 调用。
    

![n8n工作流编辑器界面](https://s.coze.cn/image/JZUiYo_6NJA/)

## 步骤 4：验证与优化

### 测试生成的工作流

- **功能验证**：在 n8n 中手动触发工作流，检查是否按预期执行（如读取表格、调用 API）。
    
- **常见问题**：
    
    - API 鉴权错误：确保在 n8n 中预先配置相关服务的凭证（如 Google Sheets、Google Drive）。
        
    - 节点参数缺失：参考生成的 Markdown 文档补充细节。
        

### 扩展验证（使用用户资源）

- **模板对比**：访问 [https://e3eb070d.n8n-workflows-bxc.pages.dev/](https://e3eb070d.n8n-workflows-bxc.pages.dev/)，搜索类似工作流（如"video generation"），对比 AI 生成结果的合理性。
    
- **多模型测试**：如果 GLM - 4.7 受限，使用 cursorweb2api 部署本地模型（如 Claude - 4.5 - sonnet），重复本教程步骤，观察输出差异。
    

![AI代码生成工作流程图](https://s.coze.cn/image/ki-6ydz3o10/)

### 优化建议

- **提示词改进**：如果生成的工作流不理想，在 Skill 中强化约束，例如：
    
    - 要求“所有 HTTP 节点必须包含错误处理”。
        
    - 指定“使用 AI Agent 节点作为核心”。
        
- **性能调优**：对于复杂工作流，分模块生成后再在 n8n 中手动整合。
    

## 结论

本教程通过 AI 自动化大幅降低了 n8n 工作流的学习门槛。核心优势在于：

- **效率提升**：分钟级生成替代手动数小时搭建。
    
- **可扩展性**：结合上下文学习和多模型资源，适应各类场景。
    
- **可靠性**：基于模板的生成方式减少错误。
    

建议在实际使用中，先从小型工作流开始测试，逐步扩展至复杂流程。如有问题，可参考 n8n 官方文档或社区资源调试。

#AI工作流 #n8n自动化 #GLM-4.7应用 #低代码开发