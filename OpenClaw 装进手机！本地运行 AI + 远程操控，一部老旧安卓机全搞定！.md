

# OpenClaw 装进手机！本地运行 AI + 远程操控，一部老旧安卓机全搞定！


如果你最近关注过 AI 圈，那你一定听说过“小龙虾 OpenClaw”。它不仅可以作为一个强大的智能助手，还能实现远程控制、自动化任务，甚至接管你的 [手机](https://www.freedidi.com/23603.html#)做各种操作。更关键的是，现在它已经可以直接安装在手机上本地运行，不依赖云端，真正做到低延迟、省电、随时随地可用。

![](https://www.freedidi.com/wp-content/uploads/2026/03/1-1.webp)

这篇文章就带你完整梳理，从下载安装到实际使用，一步步把 OpenClaw 安装进你的安卓手机。

软件

首先来说一个核心亮点：OpenClaw 是可以在手机本地运行的。这意味着它不需要远程服务器支持，也不会因为网络延迟影响体验。你可以把它理解为一个随身携带的 AI 助手，随时唤醒、随时响应。

而且它的硬件要求非常低，一台老旧安卓手机就可以运行。内存大约只需要 500MB，现在大多数手机都远远超过这个配置，所以几乎没有门槛。

## **OpenClaw 手机版下载：**

### **【[点击前往](https://github.com/mithun50/openclaw-termux)】 或 【[备用下载](https://pan.quark.cn/s/e762fb37ebdf)】**

![](https://www.freedidi.com/wp-content/uploads/2026/03/20260331_1774954196.webp)

## 要求

|要求|细节|
|---|---|
|**安卓**|10 或更高（API 29）|
|**贮存**|Ubuntu + Node.js + OpenClaw 大约需要 500MB 内存。|
|**架构**|arm64-v8a、armeabi-v7a、x86_64|
|**Termux**（仅限命令行界面）|来自F-Droid（而非 Play 商店）|

### 首轮

1. 安装APK
2. 按照安装向导操作（下载约 500MB 的 Ubuntu 根文件系统）
3. 从控制面板启动网关
4. 请访问以下网址访问网络控制面板：`http://127.0.0.1:18789`

### 要求

-  [Android](https://www.freedidi.com/23603.html#) 10+（API 29）
- 初始设置需要约 500MB 的可用存储空间
- 首次设置需要连接互联网

它的实现原理其实也很有意思。OpenClaw 并不是直接跑在安卓系统上，而是通过 Proot 在手机里虚拟出一个 Ubuntu 系统，然后在这个环境中安装 NodeJS 和 OpenClaw 主程序，同时提供一个图形化界面进行管理。最重要的一点是：整个过程不需要 Root 权限，这让它的可用性大大提升。

Android 操作系统

![](https://www.freedidi.com/wp-content/uploads/2026/03/20260331_1774953961-scaled.webp)

在安装方式上，它提供了两种方案：一种是通过专门的应用进行安装，另一种是通过命令行安装。对于大多数用户来说，直接使用 APK 安装是最简单的方式。

### 两种使用方法

||**Flutter 应用**（独立版）|**Termux CLI**|
|---|---|---|
|安装|构建 APK 或下载版本|`npm install -g openclaw-termux`|
|设置|点击“开始设置”|`openclawx setup`|
|网关|点击“启动网关”|`openclawx start`|
|终端|内置终端模拟器|Termux shell|
|仪表板|内置 WebView|浏览器`localhost:18789`|

安装流程其实并不复杂。首先下载对应版本的安装包，推荐选择官方推荐版本，它适配绝大多数安卓设备。如果你的 [手机](https://www.freedidi.com/23603.html#)比较旧，可以选择兼容 32 位 ARM 的版本；如果是在模拟器环境，则可以选择 x86 版本。

软件

下载完成后，把 APK 传到手机上进行安装。你可以使用局域网传输工具，比如 LANDrop，在电脑和手机之间快速传文件。只要两台设备在同一网络下，就可以互相识别并直接传输，非常方便。

![](https://www.freedidi.com/wp-content/uploads/2026/03/20260331_1774954335-scaled.webp)

## **LANDrop 神器下载：**

### **1、电脑版: 【[点击下载](https://landrop.app/)】或 【[打包下载](https://pan.quark.cn/s/79560d535c90)】**

### **2、手机版:【[点击下载](https://releases.landrop.app/landrop-v2-flutter/LANDrop-flutter-latest-android.apk)】或 【[下载APK安装包](https://pan.quark.cn/s/79560d535c90)】**

安装完成后，第一次打开应用，会自动进入初始化流程。整个过程分为几个阶段：下载 Ubuntu 虚拟环境、解压系统、安装 NodeJS、部署 OpenClaw，最后进行配置。这一步需要一定时间，尤其是虚拟环境大约有 500MB，需要耐心等待。

软件

![](https://www.freedidi.com/wp-content/uploads/2026/03/20260331_1774954471-scaled.webp)

配置阶段是整个流程中最关键的一步。你需要选择 AI 服务提供商，比如 OpenAI、Claude、DeepSeek、Gemini 等。如果你在海外环境，推荐使用 OpenAI 或 Claude；如果在国内，可以选择 DeepSeek 或 Minimax。

![](https://www.freedidi.com/wp-content/uploads/2026/03/2026-03-31-16-07-17.00_05_52_10.Still016-scaled.webp)

登录方式可以选择 API Key 或网页授权。如果你是免费用户，建议使用网页授权方式，操作更简单。授权完成后，还需要选择具体模型，比如 GPT-4 或 GPT-3.5。

免费软件与共享软件

接下来是一个非常有意思的功能：对接第三方聊天工具。OpenClaw 支持 Telegram、Discord、飞书等平台。以 Telegram 为例，你需要通过 BotFather 创建一个机器人，然后获取 Token 填入配置中。完成后，通过一条配对命令，就可以把 OpenClaw 和 Telegram 连接起来。

![](https://www.freedidi.com/wp-content/uploads/2026/03/2026-03-31-16-07-17.00_07_25_09.Still017-scaled.webp)

当你看到系统返回“approved”，就说明已经对接成功。这时你可以直接在 Telegram 里和你的 AI 助手聊天，它会像一个真正的助手一样回应你、帮你处理任务。

除了聊天能力之外，OpenClaw 的真正强大之处在于“自动化”和“控制能力”。你可以让它帮你写文章、整理资料、编写代码，甚至执行定时任务。它就像一个 24 小时在线的数字员工。

![](https://www.freedidi.com/wp-content/uploads/2026/03/2026-03-31-16-07-17.00_00_00_00.Still018-scaled.webp)

更进一步，它还可以实现远程控制 [手机](https://www.freedidi.com/23603.html#)。例如远程拍照、录制视频、做监控等。这一点对于安防、远程观察等场景非常实用。当然，要使用这些功能，需要开启开发者模式和无线调试，并授予摄像头、录制等权限。

软件

![](https://www.freedidi.com/wp-content/uploads/2026/03/2026-03-31-16-07-17.00_00_15_14.Still019-scaled.webp)

当一切配置完成后，你可以通过浏览器打开 OpenClaw 提供的本地地址，进入控制面板。在这里可以管理模型、技能（Skills）、任务以及各种功能扩展。

整体来看，把 OpenClaw 装进手机，相当于给自己打造了一个随身 AI 中枢。它不依赖云服务器，不受设备限制，可以随时随地运行。无论是日常使用还是技术探索，都有很大的发挥空间。

如果你愿意折腾一点，这套方案不仅仅是“好玩”，甚至可以成为你个人效率系统的一部分

## 📖 图文安装使用教程（2026最新版）

### 一、OpenClaw手机版三种形态对比

|版本类型|安装难度|功能完整性|适合人群|推荐指数|
|---|---|---|---|---|
|**APK直接安装**​|⭐⭐|⭐⭐⭐|小白用户、快速体验|★★★★★|
|**Termux部署**​|⭐⭐⭐⭐|⭐⭐⭐⭐⭐|技术爱好者、深度用户|★★★★☆|
|**中文整合版**​|⭐⭐|⭐⭐⭐⭐|国内用户、中文界面需求|★★★★★|

### 二、APK直接安装（最简单，推荐新手）

#### **步骤1：下载安装包**

- **官方GitHub**：`https://github.com/mithun50/openclaw-termux`
    
- **中文整合版**：`https://github.com/JunWan666/openclaw-termux-zh`
    
- **夸克网盘**：[`https://pan.quark.cn/s/e762fb37ebdf`](https://pan.quark.cn/s/fa1c698da93c)
    

_图片建议：展示GitHub下载页面截图，标注下载按钮位置_

#### **步骤2：安装应用**

1. 在手机设置中开启"未知来源应用"安装权限
    
2. 找到下载的APK文件（如`OpenClaw-v1.8.6-arm64-v8a.apk`）
    
3. 点击安装，按照提示完成
    

_图片建议：展示手机安装界面截图，标注"继续安装"按钮_

#### **步骤3：初始设置**

1. 打开OpenClaw应用
    
2. 授予必要的权限：
    
    - 无障碍服务（必须）
        
    - 通知权限（推荐）
        
    - 存储权限（可选）
        
    
3. 按照向导完成基础配置
    

_图片建议：展示权限请求弹窗和配置向导界面_

### 三、Termux专业部署（功能最全）

#### **环境准备**

bash

bash

复制

```
# 1. 安装F-Droid（不要用Google Play版本）
# 访问：https://f-droid.org 下载安装[10](@ref)

# 2. 在F-Droid中安装Termux套件
# Termux（核心）
# Termux:API（系统调用）
# Termux:Boot（开机自启）[10](@ref)
```

_图片建议：展示F-Droid应用商店界面和Termux安装过程_

#### **一键安装脚本**

bash

bash

复制

```
# 方法1：使用官方脚本
curl -fsSL https://raw.githubusercontent.com/mithun50/openclaw-termux/main/install.sh | bash

# 方法2：中文整合版
curl -sL myopenclawhub.com/install | bash
source ~/.bashrc
```

_图片建议：展示Termux终端运行安装命令的截图_

#### **配置与启动**

bash

bash

复制

```
# 1. 进入Ubuntu环境
proot-distro login ubuntu

# 2. 初始化OpenClaw
openclaw onboard --install-daemon

# 3. 启动网关
openclaw gateway

# 4. 打开控制台
openclaw dashboard
```

_图片建议：展示OpenClaw控制台界面截图_

### 四、中文整合版安装（国内用户首选）

#### **特色功能**

- ✅ 完全汉化界面
    
- ✅ 内置飞书消息平台接入
    
- ✅ 优化安装进度显示
    
- ✅ 支持自定义OpenAI兼容提供商
    

#### **安装流程**

1. **下载APK**：从GitHub Releases下载最新版
    
2. **安装应用**：按提示完成安装（约500MB空间）
    
3. **初始设置**：
    
    - 选择AI模型提供商（MiniMax/DeepSeek/通义千问）
        
    - 配置API密钥
        
    - 选择消息通道（飞书/钉钉/Telegram）
        
    
4. **启动服务**：点击"Start Gateway"按钮
    

_图片建议：展示中文整合版界面截图，标注关键配置选项_

### 五、核心功能配置图解

#### **1. AI模型选择界面**

复制

```
[模型选择]
├── MiniMax（推荐，国内直连）
├── DeepSeek（免费额度）
├── 通义千问
├── OpenAI兼容API
└── 自定义端点
```

_图片建议：展示模型选择界面的截图_

#### **2. 消息通道配置**

- **飞书机器人**：最稳定，企业微信兼容
    
- **钉钉机器人**：办公场景适用
    
- **Telegram**：国际用户首选
    
- **HTTP Webhook**：开发者选项
    

#### **3. 技能市场安装**

bash

bash

复制

```
# 安装技能市场
npx clawhub@latest

# 常用技能推荐
- 自动签到技能（每日收益）
- 电商比价技能（差价返利）
- 社交媒体管理（自动发布）
- 数据采集工具（信息整理）
```

### 六、赚钱任务实战演示

#### **🤑 自动赚钱任务清单**

|任务类型|操作演示|预估收益|所需技能|
|---|---|---|---|
|**APP自动签到**​|每日自动登录30+APP领取积分|50-200元/月|签到技能|
|**电商比价监控**​|监控商品价格波动，自动下单|100-500元/月|比价技能|
|**内容自动发布**​|定时发布社交媒体内容|100-800元/月|发布技能|
|**数据采集整理**​|采集行业数据生成报告|200-1000元/月|采集技能|

_图片建议：展示OpenClaw执行自动化任务的界面截图_

#### **📱 手机界面操作演示**

1. **主界面**：显示任务队列和执行状态
    
2. **技能管理**：安装/卸载/配置技能
    
3. **日志查看**：实时监控任务执行情况
    
4. **设置页面**：模型配置、通道管理、系统设置
    

### 七、常见问题解答（附解决方案截图）

#### **Q1：安装失败怎么办？**

**A**：检查Android版本（需9.0+）、存储空间（500MB+）、网络连接

_图片建议：展示错误提示和解决方案的对比图_

#### **Q2：任务执行慢？**

**A**：优化建议：

1. 关闭手机省电模式
    
2. 执行`termux-wake-lock`防止休眠
    
3. 使用性能更好的AI模型
    

#### **Q3：如何远程访问？**

**A**：配置cpolar或Tailscale实现公网访问

### 八、高级技巧与优化

#### **1. 多设备集群部署**

- 用多部闲置手机组建AI集群
    
- 通过飞书统一调度任务
    
- 负载均衡，效率倍增
    

#### **2. 自定义技能开发**

markdown

markdown

复制

```
# 技能模板
## 技能名称：微信自动回复
## 功能描述：自动回复微信消息
## 触发条件：收到新消息
## 执行动作：根据关键词自动回复
```

#### **3. 性能优化配置**

bash

bash

复制

```
# 内存优化
export NODE_OPTIONS="--max-old-space-size=2048"

# 网络优化
使用VPN提升Claude API响应速度[13](@ref)
```

### 九、安全注意事项

⚠️ **重要提醒**：

1. **使用备用机**：不要在主力机上部署，避免数据丢失
    
2. **权限管理**：谨慎授予文件读写权限
    
3. **定期备份**：备份`~/.config/openclaw`文件夹
    
4. **监控日志**：定期检查任务执行日志
    

### 十、资源下载与社区支持

#### **官方资源**：

- GitHub仓库：`https://github.com/openclaw/openclaw`
    
- 中文文档：`https://openclaw.qt.cool`
    
- 技能市场：`https://clawhub.io`
    

#### **社区支持**：

- 飞书群：`https://applink.feishu.cn/client/chat/chatter/add_by_link?link_token=566r8836-6547-43e0-b6be-d6c4a5b12b74`
    
- GitHub Issues：提交问题和反馈
    
- 中文论坛：`https://clawd.org.cn`
    

---

## 💡 温馨提示

1. **起步建议**：先从APK版本开始，熟悉后再尝试Termux部署
    
2. **设备选择**：推荐4GB+内存的闲置安卓手机
    
3. **网络环境**：稳定WiFi连接，避免使用移动数据
    
4. **学习曲线**：前3天为学习期，第4天开始稳定收益
    
5. **合规使用**：遵守各平台用户协议，合理设置任务频率
    

**让科技为你工作，而不是你为科技工作！一部闲置手机+OpenClaw=你的24小时AI赚钱助手！**