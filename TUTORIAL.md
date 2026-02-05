# 🚀 5分钟搭建你的 AI 技能商店 - 72+ 技能包 + 2053 个工作流

  

> 一站式 AI Agent Skills 和 N8N 工作流资源中心，完全免费开源！

  

## 🎯 项目简介

  

**AI 技能 & 工作流商店** 是一个开源的资源聚合平台，整合了：

  

- 🎨 **72+ AI Agent Skills** - 涵盖文档处理、内容创作、编程开发等

- ⚡ **2053 个 N8N 工作流** - 支持 365 种服务集成

  

**在线演示：** https://skill.miyucaicai.cn/

  

![首页展示](./screenshots/homepage.png)

  

---

  

## ✨ 核心功能

  

### 1. 统一资源入口

  

一个 URL 访问两种资源，无需多个网站跳转：

  

![双卡片设计](./screenshots/dual-cards.png)

  

### 2. AI Skills 智能浏览

  

- ✅ 实时搜索（响应 < 100ms）

- ✅ 智能分类筛选

- ✅ 精美卡片展示

- ✅ 自动同步 GitHub 最新数据

  

![Skills浏览](./screenshots/skills-browse.png)

  

### 3. N8N Workflows 集合

  

- ✅ 2053 个工作流模板

- ✅ 可视化流程图

- ✅ 一键下载 JSON

- ✅ 按触发类型和复杂度筛选

  

![N8N工作流](./screenshots/n8n-workflows.png)

  

### 4. 完美响应式设计

  

支持桌面、平板、手机全平台访问

  

![响应式设计](./screenshots/responsive.png)

  

---

  

## 🚀 快速部署

  

### 方法一：Vercel 一键部署（推荐）

  

**步骤 1：** Fork 项目到 GitHub

  

**步骤 2：** 登录 [Vercel](https://vercel.com) 并导入仓库

  

![Vercel导入](./screenshots/vercel-import.png)

  

**步骤 3：** 点击 Deploy，等待 1-2 分钟

  

![部署成功](./screenshots/deploy-success.png)

  

**步骤 4：** 绑定自定义域名（可选）

  

![域名绑定](./screenshots/domain-setup.png)

  

**完成！** 你的 AI 技能商店已上线 🎉

  

---

  

### 方法二：Vercel CLI 部署

  

```bash

# 安装 Vercel CLI

npm install -g vercel

  

# 克隆项目

git clone https://github.com/your-username/skill-store.git

cd skill-store

  

# 登录并部署

vercel login

vercel --prod

```

  

---

  

## 📱 使用指南

  

### 浏览 AI Skills

  

1. 访问首页，点击 "浏览 AI Skills"

2. 使用搜索框输入关键词（如 "excel"、"pdf"）

3. 点击分类按钮快速筛选

4. 点击技能卡片查看 GitHub 详情

  

![使用演示](./screenshots/usage-demo.png)

  

### 浏览 N8N Workflows

  

1. 点击 "浏览 N8N Workflows" 跳转到工作流站点

2. 搜索或筛选你需要的工作流

3. 查看可视化流程图

4. 下载 JSON 文件导入 N8N

  

---

  

## 🎨 技术架构

  

```

前端: HTML5 + CSS3 + JavaScript

后端: Python 3.12 + Vercel Serverless

部署: Vercel（免费 + 全球 CDN）

数据: GitHub awesome-agent-skills

```

  

---

  

## 💡 核心优势

  

| 特性 | 说明 |

|-----|------|

| 🎯 统一入口 | 一个 URL 访问两种资源 |

| 🎨 精美设计 | 紫色渐变 + 大卡片布局 |

| ⚡ 快速响应 | 搜索 < 100ms，加载 < 1s |

| 📱 响应式 | 完美支持手机/平板/电脑 |

| 🆓 完全免费 | 开源 MIT 协议 |

| 🌍 全球加速 | Vercel CDN 覆盖全球 |

  

---

  

## ⚙️ 自定义配置

  

### 修改数据源

  

编辑 `api/skills/index.py`：

  

```python

SKILLS_DATA_URL = 'https://your-data-source.com/skills.json'

```

  

### 自定义样式

  

编辑 `public/index.html` 中的 CSS：

  

```css

body {

    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);

    /* 修改为你喜欢的渐变色 */

}

```

  

### 修改 N8N 链接

  

```html

<a href="https://your-n8n-site.com/" target="_blank">

    浏览 N8N Workflows →

</a>

```

  

---

  

## ❓ 常见问题

  

**Q: 部署需要多长时间？**  

A: 使用 Vercel 一键部署，只需 2-3 分钟。

  

**Q: 需要付费吗？**  

A: 完全免费！Vercel 提供免费托管，只需要域名费用（可选）。

  

**Q: 数据会自动更新吗？**  

A: 是的，API 会实时从 GitHub 拉取最新数据。

  

**Q: 可以商用吗？**  

A: 可以！项目采用 MIT 开源协议。

  

**Q: 支持哪些浏览器？**  

A: 支持所有现代浏览器（Chrome、Firefox、Safari、Edge）。

  

---

  

## 🎁 相关资源

  

- 🌟 [项目 GitHub](https://github.com/your-username/skill-store)

- 🌐 [在线演示](https://skill.miyucaicai.cn/)

- 📚 [awesome-agent-skills](https://github.com/VoltAgent/awesome-agent-skills)

- ⚡ [N8N 工作流集合](https://github.com/Zie619/n8n-workflows)

- 📖 [Vercel 文档](https://vercel.com/docs)

  

---

  

## 🚀 立即开始

  

### 三种方式任选：

  

1. **在线体验** → https://skill.miyucaicai.cn/

2. **一键部署** → [![Deploy](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https://github.com/your-username/skill-store)

3. **本地运行** → `git clone && vercel dev`

  

---

  

## 📞 联系方式

  

- 📧 Email: support@miyucaicai.cn

- 🌐 Website: https://skill.miyucaicai.cn/

- 💬 GitHub Issues: 提交问题和建议

  

---

  

## 📄 开源协议

  

本项目采用 [MIT License](https://opensource.org/licenses/MIT) 开源协议。

  

---

  

<div align="center">

  

**⭐ 如果觉得有用，请给个 Star 支持一下！**

  

Made with ❤️ by Skill Store Team

  

[🚀 立即部署](https://vercel.com/new) | [📖 查看文档](./README.md) | [💬 提交反馈](https://github.com/your-username/skill-store/issues)

  

</div>