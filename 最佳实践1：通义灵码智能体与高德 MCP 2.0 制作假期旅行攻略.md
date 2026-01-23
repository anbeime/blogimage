# 最佳实践1：通义灵码智能体与高德 MCP 2.0 制作假期旅行攻略

本文介绍如何使用通义灵码智能体与高德 MCP 2.0 制作为期三天的假期旅行攻略页面。同时，将生成的旅行攻略导入高德地图 APP，以便创建专属地图，以满足在行程中进行探店、导航、打车及购票等出行需求。

  

# 前提条件

- 已在 IDE 中安装通义灵码【1】，并确认版本在 2.5 以上。
    
- 已获取高德申请的 key【2】。
    

  

近期，阿里云正式宣布开源其迄今**最具突破性的AI编程大模型Qwen3-Coder，并宣布**AI编程产品“通义灵码”全面支持，且**向全球开发者免费提供不限量服务，不需要邀请码，你就能即刻体验到全球最领先的编程能力。**

**0****1**

  

**第一步：成为高德开发者并创建 Key**

  

  

帮助文档：https://lbs.amap.com/api/mcp-server/create-project-and-key

  

登录高德开放平台控制台【3】，如果没有开发者账号，请注册成为开发者【4】。

  

创建成功后，可获取 Key 和安全密钥。

  

在高德的控制台选择应用管理， 并创建应用。

  

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/t6t4G0x65m0S9muhiaZeLgiaseumJRuPfHLYlMhqtUsVhJ5jMdO5PFMqYiaPTkYBezUDIG0xlXXPgEVsGjoELsgJg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=0)

  

然后给应用创建对应的 key，选择 Web 端（JS API）模式。

  

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/t6t4G0x65m0S9muhiaZeLgiaseumJRuPfHBXFmLAp1vKBib5rg3FtZEHzQItnibTNZUTyjyOh5oLwibIpk5DibOazRUw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=1)

  

最后得到一个 key（这里需要注意：你在 2021 年 12 月 02 日以后申请的 key 需要配合你的安全密钥一起使用。后面生成代码时， 将不会配置这个安全密钥）。

  

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/t6t4G0x65m0S9muhiaZeLgiaseumJRuPfH9cr7Dqax8tSiaj2I4aZjzXIwnWzWoqjH2SWia4UibjEBgGRpqZuHTaTsA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=2)

#   

**02**

  

**第二步：配置 MCP**

  

#   

单击 IntelliJ IDEA 侧边栏的通义灵码图标进入智能会话。

  

1. 本文使用 IntelliJ IDEA 进行演示，其他 IDE 的灵码图标位置可能稍有不同，您可参见下载和安装【1】进入智能会话。

  

2. 在智能会话页面，您可通过以下两种方式进入 MCP 服务页面。

- 方式一：单击欢迎语中的 MCP 工具链接进入 MCP 服务页面。
    
- 方式二：单击右上角头像，并在下拉菜单中选择个人设置，然后在个人设置页面单击 MCP 服务下的条形框。
    

  

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/t6t4G0x65m0S9muhiaZeLgiaseumJRuPfHp4nm2NkAjQWL1ianGzq1tgBzxloCSVJgB0cGPibjdlovaTZpMXm7P5zA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=3)

  

3. 单击 MCP 服务右侧的 `+`，并选择手动添加，然后在弹出的添加 MCP 服务页面，配置以下选项：

- 名称：输入服务名称，例如：amap-sse。
    
- 类型：选择 SSE。
    
- 服务地址：`https://mcp.amap.com/sse?key=<您在高德申请的key>`。
    

  

使用获取高德申请的 key【2】 替换`<您在高德申请的key>`，注意不要有空格。

  

4. 单击立即添加，等到链接图标变成绿色则代表 MCP 服务添加成功。

  

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/t6t4G0x65m0S9muhiaZeLgiaseumJRuPfHiania3COTk4CPdtHDksEp7iaUEnWe9pwqbAfDtSAPsVMyqv6eib8tK0EHg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=4)

#   

**03**

  

**第三步：生成 travel_tips.html 文件**

  

#   

重要

在通义灵码智能体工作之前，请务必确保已经打开任何一个工程文件，否则 MCP 调用会失败 ，更多通义灵码相关 MCP 使用问题，MCP 常见问题说明【5】。

  

1. 打开通义灵码智能会话对话框，并切换为智能体模式，同时选择 qwen3 coder 这个模型。

  

2. 在对话框中输入以下提示词并回车。

```
##北京3天端午节（25年5月31日到25年6月2日）的旅行攻略。
```

3. 灵码将根据您的需求，自主规格并调用所需工具，最终生成 `travel_tips.html` 文件。

  

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/t6t4G0x65m0S9muhiaZeLgiaseumJRuPfHahMib2yicicBztmmMcrlVib0vznjy2ibMwEcY3KDGVYib1LJYsTeLxibgrMqg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=5)

  

4. 最终生成的页面效果如下所示。

- 如果生成的页面效果、布局、字体及颜色不符合你的预期，你可以多次跟通义灵码沟通和对话。
    
- 如果无法查看预览效果，可以直接选择通义灵码 agent 模型让 AI 帮你生成预览效果。
    

  

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/t6t4G0x65m0S9muhiaZeLgiaseumJRuPfH5l5ta9p2SQg3a1lK7vzRHCk8VKLP9eaWBwTEL7NgtVJLf8BLsXciaHQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=6)

  

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/t6t4G0x65m0S9muhiaZeLgiaseumJRuPfHJG2UUQQeSf7jmicG5zUbhicOk4AwVfmVPtrU2krPpE64YTDIpQVZ4u1g/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=7)

  

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/t6t4G0x65m0S9muhiaZeLgiaseumJRuPfHKNIbRRMRdKEM5Qdf2CpnBckUYGO1jaj7oKRUPy9mZq1gC3zQHllSMQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=8)

  

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/t6t4G0x65m0S9muhiaZeLgiaseumJRuPfHfFT15bZ63JI7GFZwRicibWbV1X9icAIAIejBIKtql72TK3v90ZBm953Cg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=9)

  

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/t6t4G0x65m0S9muhiaZeLgiaseumJRuPfHmn3QWRVFXclicaLHmp8wSH0FG9aPicLC6uzmEmjVW6fJC6zgOmh0kdUg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=10)

  

**04**

  

**第四步：修正地图**

  

  

因为第一次生成时模式没有识别高德的新的 API，这个时候修改 `travel_tips.html` 文件配置 key 也是不生效的。

  

需要同时配置安全密钥，所以需要给模型新的输入：

  

（这个是参考高德文档：https://lbs.amap.com/api/javascript-api-v2/guide/abc/jscode， 注意这里使用的是明文的方式， 不可以用于生产）

  

Prompt：

```
<script src="https://webapi.amap.com/loader.js"></script>
```

重新生成代码后，在代码里配置安全密钥和 key，就可以地图展示坐标和路径了。

  

但是这里有个问题，路径只是画了一个直线，部署实际路径，这个时候需要让灵码再修正。

  

Prompt：

```
似乎高德地图画的路线不是实际道路的路线，请展示实际道路的路径
```

最后得到这个效果。

  

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/t6t4G0x65m0S9muhiaZeLgiaseumJRuPfHwQnYR42J19k5ibauS0MVBUqu66srn1icNkc3icL8CShckW6kiaibFfFVAvQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=11)

  

这里又多了一个问题， 如果三天的行程路径都展示到一起会显得比较难看，我希望可以根据具体的每一天进行过滤查看：

  

Prompt：

```
我希望多一个过滤选择， 来选择具体哪天一的具体路线， 而不是显示所有天的路线
```

然后得到这样一个效果：

  

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/t6t4G0x65m0S9muhiaZeLgiaseumJRuPfHicA5QvIK2xTCelmsBCsE991LQzY0hDFNI54YrsiarTYr7Gm7QEwTrFug/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=12)

  

但是我发现模型生成的代码有问题，当我选择具体哪一天的时候，地图没有刷新线路， 然后我再让灵码进行修复。

```
当我选择了具体哪一天的路线后， 地图没有刷新
```

然后就可以得到一个相对完美的效果了。

  

如果希望再进一步完善：

  

Prompt：

```
我希望选择具体哪一天的行程后， 再展示具体的开车线路信息描述
```

则在选择路线后，还可以得到具体的线路信息，展示如下：

  

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/t6t4G0x65m0S9muhiaZeLgiaseumJRuPfHNic6juf60nichKuibDOUamqichyFWeO9sX3xq9rribweHfSZcaFwlbExS6g/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=13)

#   

**05**

  

**第五步：扩展提示词**

  

```
##成都7天国庆节（25年10月1日到25年10月7日）的旅行攻略。
```

#   

# 接下来，就是大家来体验啦！

#   

```
【1】安装通义灵码
```

```
https://help.aliyun.com/zh/lingma/user-guide/download-the-installation-guide
```

```
【2】获取高德申请的key
```

https://lbs.amap.com/api/mcp-server/create-project-and-key

  

```
【3】高德开放平台控制台
```

```
https://console.amap.com/
```

```
【4】注册成为开发者
```

```
https://console.amap.com/dev/id/phone
```

```
【5】MCP常见问题说明
```

https://help.aliyun.com/zh/lingma/support/faq-mcp