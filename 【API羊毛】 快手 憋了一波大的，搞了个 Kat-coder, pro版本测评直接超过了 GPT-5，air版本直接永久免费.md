【API羊毛】 **快手** 憋了一波大的，搞了个 Kat-coder, pro版本测评直接超过了 GPT-5，**air版本**直接永久免费

简单看了下，兼容OpenAI的sdk以及Claude code接入，还对Cline, RooCode, Kilo的接入做了特别优化

![](assets/【API羊毛】%20快手%20憋了一波大的，搞了个%20Kat-coder,%20pro版本测评直接超过了%20GPT-5，air版本直接永久免费/file-20251203145657353.png)

[https://www.streamlake.ai/product/kat-coder](https://www.streamlake.ai/product/kat-coder) （不要切换语言为中文，中文是国内站，需要实名才能用）

**只有Air 模型永久免费**，RPM：20（每分钟最高20次调用） TPM：2000000（每分钟最高200万token交互）支持工具调用和推理，简单测试了下，效果还不错，速度也快，可能是大家都不知道吧[笑哭] 用来部署一些n8n等工作流也不错。

KAT-Coder-Air V1
KAT-Coder-Exp-72B 目前也免费

![](assets/【API羊毛】%20快手%20憋了一波大的，搞了个%20Kat-coder,%20pro版本测评直接超过了%20GPT-5，air版本直接永久免费/file-20251203145720180.png)

获取步骤：

![](assets/【API羊毛】%20快手%20憋了一波大的，搞了个%20Kat-coder,%20pro版本测评直接超过了%20GPT-5，air版本直接永久免费/file-20251203145731558.png)

创建一个模型端点模型选air的，模型调用ID是这个ep开头的，不能用KAT-Coder-Air-V1

API调用URL是：[https://vanchin.streamlake.ai/api/gateway/v1/endpoints/chat/completions](https://vanchin.streamlake.ai/api/gateway/v1/endpoints/chat/completions)

**举例 Roo Code 配置**

1. **API 提供商** : 选择 OpenAI 兼容
    
2. **基本 URL**: 输入 [https://vanchin.streamlake.ai/api/gateway/v1/endpoints](https://vanchin.streamlake.ai/api/gateway/v1/endpoints)
    
3. **API 密钥：** 输入您的 Streamlake API 密钥
    
4. **模型** : 输入您的 Wanqing 推理端点 ID（例如，ep-xxxxxxxxxxxxx）并选择使用自定义
    
![](assets/【API羊毛】%20快手%20憋了一波大的，搞了个%20Kat-coder,%20pro版本测评直接超过了%20GPT-5，air版本直接永久免费/file-20251203145743651.png)

其他客户端如claude code、cline等 参考说明文档：

[https://www.streamlake.ai/document/DOC/mg6k6nlp8j6qxicx4c9](https://www.streamlake.ai/document/DOC/mg6k6nlp8j6qxicx4c9)
