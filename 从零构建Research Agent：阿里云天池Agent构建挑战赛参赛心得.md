# 从零构建Research Agent：阿里云天池Agent构建挑战赛参赛心得

  

## 前言

  

参加阿里云天池"寻找AI全能王"Data+AI工程师全球大奖赛的Agent构建挑战赛，是我2026年开年最有收获的一次技术探索。本文将分享我在构建Research Agent过程中的技术方案、踩过的坑、以及一些个人成长感悟。

  

## 一、比赛背景

  

本次比赛的赛题二要求在PAI-LangStudio平台上，基于Qwen系列模型构建一个Research Agent，能够通过联网搜索回答100道需要多跳推理的问题。

  

核心挑战点：

- **禁止模型微调**：只能通过提示词工程和工具优化

- **多跳推理**：一个问题可能需要多次搜索才能得出答案

- **答案归一化**：判定严格，答案必须与标准答案完全一致

- **免费搜索**：如何在预算有限的情况下实现高质量搜索

  

## 二、技术方案演进

  

### 2.1 初期方案：SerpAPI + ReAct框架

  

最初我采用了经典的ReAct（Reasoning + Acting）框架：

  

```

Thought -> Action -> Observation -> Thought -> Answer

```

  

配置了SerpAPI作为搜索引擎，前期效果不错，但很快遇到了成本问题——100道题测试几次就把免费额度用完了。

  

### 2.2 中期探索：Bing Search API + 多搜索引擎降级

  

为了解决成本问题，我引入了多搜索引擎降级机制：

  

```python

# 搜索引擎优先级

1. SerpAPI (如有额度)

2. Bing Search API (如有API Key)

3. Mock搜索 (测试用)

```

  

同时优化了搜索策略：

- **查询优化**：从问题中提取关键实体，生成精准搜索词

- **并行搜索**：对需要多跳推理的问题，并行执行多个搜索

- **智能缓存**：避免重复搜索相同内容

  

### 2.3 最终方案：DuckDuckGo免费搜索

  

这是我认为最有价值的突破——成功集成了完全免费的DuckDuckGo搜索引擎：

  

```python

class DuckDuckGoSearcher:

    """免费搜索引擎，无需API Key"""

    def search(self, query):

        # 支持多种访问模式

        if self.lessapi_url:

            return self._search_lessapi(query)  # Docker本地服务

        return self._search_html(query)          # 直接访问

```

  

技术亮点：

1. **LessAPI Docker服务**：本地部署，稳定可靠

2. **智能降级**：多种访问模式自动切换

3. **代理支持**：适配国内网络环境

4. **零成本**：完全免费，无API调用限制

  

## 三、核心模块设计

  

### 3.1 问题分析器

  

```python

def analyze_question(question):

    return {

        'language': detect_language(question),      # 中/英文

        'question_type': classify_type(question),   # 人物/时间/比较等

        'key_entities': extract_entities(question), # 关键实体

        'complexity': assess_complexity(question)   # 简单/中等/复杂

    }

```

  

### 3.2 答案验证器

  

根据比赛要求，答案需要严格归一化：

  

```python

def normalize_answer(answer):

    # 1. 转小写

    # 2. 去除首尾空格

    # 3. 格式检查（公司名、人名、数字等）

    return normalized_answer

```

  

### 3.3 多智能体协作（尝试）

  

后期我尝试了多智能体架构，设计了专业化的评审智能体集群：

- **搜索智能体**：负责联网搜索

- **推理智能体**：负责逻辑推理

- **验证智能体**：负责答案校验

  

虽然最终没有完全实现，但这个思路值得继续探索。

  

## 四、踩过的坑

  

### 4.1 网络环境问题

  

国内访问DuckDuckGo经常超时，解决方案：

```bash

# Docker部署LessAPI服务

docker run -d -p 8080:8080 \

    -e PROXY_URL=http://your-proxy:port \

    lessapi/lessapi-duckduckgo:v0.0.1

```

  

### 4.2 答案格式问题

  

比赛对答案格式要求严格，比如：

- 公司名称：必须形如 "Alibaba Group Limited"

- 人名：需要区分中英文格式

- 数字：注意单位和小数位

  

我花了不少时间调试答案验证器，确保格式正确。

  

### 4.3 多跳推理的复杂性

  

比如这道题：《魂武者》的作者和《龙族》的作者是同一个人吗？

  

需要：

1. 搜索《魂武者》作者 -> 江南

2. 搜索《龙族》作者 -> 江南

3. 比较 -> 输出"是"

  

看似简单，但要让Agent稳定执行这个流程，需要精心设计的提示词和状态管理。

  

## 五、个人成长与收获

  

### 5.1 技术能力提升

  

1. **Agent架构理解**：从理论到实践，深入理解了ReAct、Plan-and-Execute等框架

2. **提示词工程**：学会了如何设计高质量的System Prompt和Few-Shot示例

3. **搜索引擎集成**：掌握了DuckDuckGo等免费搜索API的使用

4. **云端部署**：熟悉了PAI-LangStudio和PAI-EAS的使用流程

  

### 5.2 解决问题的思路

  

比赛中遇到的问题让我学会了：

- **成本控制**：如何在有限预算下实现最优效果

- **架构设计**：模块化设计，便于迭代和优化

- **文档习惯**：详细记录每次实验的结果和思考

  

### 5.3 社区交流

  

通过钉钉群和天池论坛，结识了很多志同道合的朋友，大家分享的技术方案和踩坑经验都非常有价值。

  

## 六、对后来者的建议

  

1. **先跑通基线**：不要一开始就追求完美，先确保基本流程能跑通

2. **重视免费方案**：DuckDuckGo真的很好用，推荐优先尝试

3. **答案格式很重要**：花时间打磨答案验证器，能避免很多失分

4. **多看官方文档**：PAI-LangStudio的文档很详细，很多问题都有答案

5. **善用缓存**：本地缓存搜索结果，既省时又省钱

  

## 七、总结

  

这次比赛让我深刻体会到，构建一个"能用"的Agent不难，但要构建一个"好用"的Agent，需要在架构设计、提示词优化、工具集成等多个环节持续打磨。

  

Research Agent是从"能对话"向"能做事"演进的关键，我相信这类技术会在未来发挥越来越重要的作用。感谢阿里云和天池平台提供这次宝贵的学习机会！

  

---

  

**参赛队伍**：Quanking Team  

**比赛链接**：https://tianchi.aliyun.com/competition/entrance/532449  

**分享时间**：2026年3月

  

---

  

#阿里云天池 #Agent #ResearchAgent #DuckDuckGo #PAI-LangStudio #Qwen #大模型 #技术分享