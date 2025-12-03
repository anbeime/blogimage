

Github:[github.com/GewoonJaap/gemini-cli-openai](https://github.com/GewoonJaap/gemini-cli-openai?tab=readme-ov-file)

使用 Cloudflare Workers 将 Google 的 Gemini 模型转换为 OpenAI 兼容的端点。通过熟悉的 OpenAI API 模式访问 Google 最先进的 AI 模型，该模型由 OAuth2 身份验证和驱动官方 Gemini CLI 的相同基础设施提供支持。

**注意：** Gemini 2.5 模型默认启用思考功能。API 会自动管理此功能：

- 当实际思考被禁用（环境设置）时，思考预算设置为 0 以禁用它
    
- 当实际思考被启用（环境设置）时，思考预算默认为 -1（由 Gemini 动态分配）
    

**思考支持** 有两种模式：

- **模拟思考** ：设置 ENABLE_FAKE_THINKING=true 以生成合成推理文本（适用于测试）
    
- **真实思考** ：将 ENABLE_REAL_THINKING=true 设置为使用 Gemini 的原生推理能力
    

**Gemini CLI OpenAI Worker 详细安装指南（小白版）**

这个项目的作用是将 Google Gemini 模型转换成兼容 OpenAI API 的接口，部署在 Cloudflare Workers 上。

**准备工作**

**1. 注册必要的账号**

你需要准备两个账号：

- **Google 账号**：用于访问 Gemini
    
- **Cloudflare 账号**：用于部署服务（免费即可）
    

**2. 安装必要的软件**

**安装 Node.js**

1. 访问 [Node.js 官网](https://nodejs.org/)
    
2. 下载 LTS 版本（推荐 18.x 或更高版本）
    
3. 双击安装包，一路下一步即可
    
4. 验证安装：打开命令行（Windows 按 Win+R，输入 cmd），输入：
    

复制

```
node --version
npm --version
```

如果显示版本号，说明安装成功

**安装 Git**

1. 访问 [Git 官网](https://git-scm.com/)
    
2. 下载对应系统的安装包
    
3. 安装时保持默认设置即可
    

**详细部署步骤**

**第一步：获取 OAuth2 认证凭据**

**1. 安装 Gemini CLI**

打开命令行，输入：

```
npm install -g @google/gemini-cli
```

**2. 启动 Gemini CLI 并登录**

```
gemini
```

运行后会显示选项，选择 ● Login with Google

**3. 完成 Google 账号登录**

- 浏览器会自动打开
    
- 使用你的 Google 账号登录
    
- 授权访问权限
    

**4. 找到凭据文件**

登录成功后，凭据会保存在：

- **Windows 系统**：C:\Users\你的用户名\.gemini\oauth_creds.json
    
- **Mac/Linux 系统**：~/.gemini/oauth_creds.json
    

打开这个文件，你会看到类似这样的内容：

```
{
  "access_token": "ya29.a0AS3H6Nx...",
  "refresh_token": "1//09FtpJYpxOd...",
  "scope": "https://www.googleapis.com/auth/cloud-platform ...",
  "token_type": "Bearer",
  "id_token": "eyJhbGciOiJSUzI1NiIs...",
  "expiry_date": 1750927763467
}
```

**保存好这个内容，后面会用到！**

**第二步：注册 Cloudflare 账户**

1. 访问 [Cloudflare 官网](https://www.cloudflare.com/)
    
2. 点击"Sign Up"注册账户
    
3. 填写邮箱和密码
    
4. 验证邮箱
    
5. 登录后进入控制面板
    

**获取 Cloudflare API Token**

1. 在 Cloudflare 控制面板右上角点击头像
    
2. 选择"My Profile"（配置文件）
    
3. 点击"API Tokens"（API令牌）选项卡
    
4. 点击"Create Token"（创建令牌）
    
5. 选择"Custom token"（创建自定义令牌）
    
6. 配置如下：
    

- **令牌名称**: Gemini Worker
    
- **权限**:
    

- 账户 - Workers 脚本 - 编辑
    
- 区域 - 区域 - 读取
    
- 区域 - 区域设置 - 编辑
    

- **账户资源**: 包含 - 所有账户
    
- **区域资源**: 包含 - 所有区域
    ![](assets/将Gemini%20CLI变成通用型的模型调用API/file-20251203145604060.png)

7. 点击"Continue to summary"
    
8. 点击"Create Token"
    
9. **重要**：复制生成的 Token 并保存到安全地方
    

**第三步：下载项目代码**

1. 创建一个工作文件夹（比如在桌面创建 gemini-project 文件夹）
    
2. 打开命令行，进入这个文件夹：
    

```
cd Desktop/gemini-project
```

3. 克隆项目：
    

```
git clonehttps://github.com/GewoonJaap/gemini-cli-openai.gitcd gemini-cli-openai
```

**第三步：安装 Wrangler（Cloudflare 部署工具）**

在项目目录下运行：

```
npm install -g wrangler
```

**第四步：登录 Cloudflare**

```
wrangler login
```

浏览器会打开，登录你的 Cloudflare 账号并授权。

![](assets/将Gemini%20CLI变成通用型的模型调用API/file-20251203145604059.png)

**第五步：创建 KV 存储空间**

运行以下命令

```
wrangler kv namespace create "GEMINI_CLI_KV"
```

这会返回类似这样的信息：

```
Add the following to your configuration file in your kv_namespaces array:
{ binding = "GEMINI_CLI_KV", id = "abcd1234567890..." }
```

**记下这个 id 值！**

**第六步：配置项目**

**1. 修改 wrangler.toml 文件**

用记事本打开项目根目录的 wrangler.toml 文件，找到 kv_namespaces 部分，替换为你的 ID：

```
kv_namespaces = [
  { binding = "GEMINI_CLI_KV", id = "你刚才记下的ID" }
]
```

![](assets/将Gemini%20CLI变成通用型的模型调用API/file-20251203145604058.png)

**注意**：

- GCP_SERVICE_ACCOUNT= 后面直接粘贴整个 JSON，不要换行
    
- GEMINI_PROJECT_ID=Google Cloud的项目ID
    

**第七步：安装项目依赖**

在项目目录运行：

```
npm install
```

**第八步：部署到 Cloudflare**

**1. 设置生产环境密钥**

```
wrangler secret put GCP_SERVICE_ACCOUNT
```

粘贴你的 OAuth 凭据 JSON（就是 oauth_creds.json 的全部内容）

```
wrangler secret put OPENAI_API_KEY
```

输入你设置的 API 密钥（比如 sk-myapikey123456 自己设定）

**2. 部署项目**

```
wrangler deploy
```

部署成功后，会显示你的 API 地址，类似：

```
https://gemini-cli-openai.你的用户名.workers.dev
```

**使用方法**

**测试 API**

你可以使用以下方式测试：

**cherry studio:**

![](assets/将Gemini%20CLI变成通用型的模型调用API/file-20251203145604057.png)

**Roo code：**

![](assets/将Gemini%20CLI变成通用型的模型调用API/file-20251203145604056.png)

**在任何支持 OpenAI API 的应用中使用**：

- API 地址：https://你的API地址/v1
    
- API 密钥：你设置的密钥（如 sk-myapikey123456）
    
- 模型选择：gemini-2.5-flash 或 gemini-2.5-pro
    

**常见问题**

1. **如果部署失败**：
    

- 检查是否正确登录了 Cloudflare
    
- 确认 KV namespace ID 是否正确
    
- 确保 OAuth 凭据格式正确
    

2. **如果 API 调用失败**：
    

- 检查 API 密钥是否正确
    
- 确认 OAuth 凭据是否有效
    
- 查看 Cloudflare Workers 的日志
    

3. **如何更新凭据**：
    

如果 OAuth 凭据过期，重新运行 gemini 命令获取新凭据，然后更新 secret：

复制

```
wrangler secret put GCP_SERVICE_ACCOUNT
```