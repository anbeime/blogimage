请帮我生成一个能够提供公众号接口实现一键自动发布功能的MCP Server。
## WeChatOfficialAccountPublisher

提供微信公众号接口的一键自动发布功能，支持文本、图片、图文消息的自动发布，以及模板消息推送，简化公众号内容管理流程。

部署下载代码

- 工具(4)
    
- 环境变量(4)
    
    必填
    

publish_text_message

2个参数

功能描述: 发布文本消息到微信公众号

详情代码

publish_image_message

2个参数

功能描述: 发布图片消息到微信公众号

详情代码

publish_news_message

2个参数

功能描述: 发布图文消息到微信公众号

详情代码

send_template_message

4个参数

功能描述: 发送模板消息到微信公众号用户

详情代码

**WECHAT_ACCESS_TOKEN 与 WECHAT_TEMPLATE_ID 的含义**

**WECHAT_ACCESS_TOKEN**

- 含义与作用：微信公众号/小程序调用绝大多数微信开放接口时的**全局唯一接口调用凭证**。调用时在请求参数或请求头中携带，用于**身份校验与权限判定**。
- 有效期与特性：有效期通常为**7200秒（2小时）**；**重复获取会使上一次 token 立即失效**；同一 **AppID** 的 token 是**全局唯一**的，建议由**中控服务器集中管理**、统一刷新与分发。
- 获取方式：使用 **AppID** 与 **AppSecret** 调用接口：GET [https://api.weixin.qq.com/cgi-bin/token?grant_type=client_credential&appid=APPID&secret=APPSECRET，返回](https://api.weixin.qq.com/cgi-bin/token?grant_type=client_credential&appid=APPID&secret=APPSECRET%EF%BC%8C%E8%BF%94%E5%9B%9E) JSON 包含 **access_token** 与 **expires_in**。
- 典型用途：获取用户信息、发送服务通知/订阅消息、创建菜单、获取服务器 IP、获取 **jsapi_ticket** 等几乎所有需要鉴权的接口。

**WECHAT_TEMPLATE_ID**

- 含义与作用：指微信**模板消息**的**模板ID**（template_id），用于标识你在公众号后台选择或申请的某一条消息模板。
- 使用场景：在调用“发送模板消息”接口时，作为必填字段随请求一起提交，服务端据此匹配模板并下发消息到用户的**服务通知**。
- 如何获取：登录**微信公众平台** -> 功能 -> 模板消息（或订阅通知）-> 选择/添加模板，即可在模板列表中看到对应的 **模板ID**。

**两者区别与配合**

- 定位不同：**WECHAT_ACCESS_TOKEN** 是调用接口的“**钥匙**”，**WECHAT_TEMPLATE_ID** 是具体“**消息模板的编号**”。
- 配合方式：发送模板消息时，请求中需同时提供有效的 **access_token** 与 **template_id**（以及接收者 **openid**、模板数据等），缺一不可。
- 管理要点：access_token 需**缓存并提前刷新**，避免并发获取导致彼此失效；template_id 与业务场景一一对应，注意不同行业/类目模板的**审核与可用性**。

**安全与配置提示**

- **AppSecret** 等同账号密钥，务必**保密存储**，不要放在前端或客户端代码中。
- 建议启用**IP 白名单**与**服务器时间校准**（NTP），减少鉴权失败。
- 若调用返回 **40001 invalid credential**，通常表示 **access_token 无效或过期**，应触发刷新并重试；若频繁刷新仍异常，检查 **AppID/AppSecret** 与网络环境。

JSON

// mcp_config.json
{
  "env_vars": {
    "WECHAT_APP_ID": "微信公众号AppID，用于身份验证和接口调用",
    "WECHAT_APP_SECRET": "微信公众号AppSecret，用于获取访问令牌",
    "WECHAT_ACCESS_TOKEN": "微信公众号访问令牌，可选，如果不提供会自动获取",
    "WECHAT_TEMPLATE_ID": "公众号模板消息ID，用于模板消息推送"
  },
  "mcp_name": "WeChatOfficialAccountPublisher",
  "mcp_description": "提供微信公众号接口的一键自动发布功能，支持文本、图片、图文消息的自动发布，以及模板消息推送，简化公众号内容管理流程。",
  "requirements": [
    "fastmcp>=0.1.0",
    "requests>=2.31.0",
    "python-dotenv>=1.0.0"
  ]
}  

PYTHON

# mcp_server.py
import os
from typing import Dict, List, Optional, Any
from fastmcp import FastMCP
import requests

# 加载环境变量配置
WECHAT_APP_ID = os.getenv("WECHAT_APP_ID", "")
WECHAT_APP_SECRET = os.getenv("WECHAT_APP_SECRET", "")
WECHAT_ACCESS_TOKEN = os.getenv("WECHAT_ACCESS_TOKEN", "")
WECHAT_TEMPLATE_ID = os.getenv("WECHAT_TEMPLATE_ID", "")

mcp = FastMCP("WeChatOfficialAccountPublisher", instructions="提供微信公众号接口的一键自动发布功能，支持文本、图片、图文消息的自动发布，以及模板消息推送，简化公众号内容管理流程。")

def get_access_token(app_id: str, app_secret: str) -> str:
    url = f"https://api.weixin.qq.com/cgi-bin/token?grant_type=client_credential&appid={app_id}&secret={app_secret}"
    response = requests.get(url)
    data = response.json()
    if 'access_token' in data:
        return data['access_token']
    else:
        raise ValueError(f"获取access_token失败: {data}")

@mcp.tool()
def publish_text_message(content: str, access_token: Optional[str] = None) -> Dict[str, Any]:
    """
    功能描述: 发布文本消息到微信公众号
    参数说明:
    - content (str): 必须。要发布的文本内容
    - access_token (Optional[str]): 可选。微信公众号访问令牌，如果不提供会使用环境变量中的WECHAT_ACCESS_TOKEN或自动获取
    返回值:
    - Dict[str, Any]: 包含发布结果的字典，包括状态和消息ID
    异常处理: 当access_token无效或获取失败时抛出ValueError异常，网络请求失败时抛出requests.exceptions.RequestException
    """
    token = access_token or WECHAT_ACCESS_TOKEN
    if not token:
        token = get_access_token(WECHAT_APP_ID, WECHAT_APP_SECRET)
    url = f"https://api.weixin.qq.com/cgi-bin/message/custom/send?access_token={token}"
    payload = {
        "touser": "OPENID",  # 实际使用时需要替换为具体的用户OpenID
        "msgtype": "text",
        "text": {
            "content": content
        }
    }
    response = requests.post(url, json=payload)
    data = response.json()
    if data.get('errcode') == 0:
        return {"status": "success", "message": "文本消息发布成功", "msgid": data.get('msgid')}
    else:
        raise ValueError(f"文本消息发布失败: {data}")

@mcp.tool()
def publish_image_message(media_id: str, access_token: Optional[str] = None) -> Dict[str, Any]:
    """
    功能描述: 发布图片消息到微信公众号
    参数说明:
    - media_id (str): 必须。图片的媒体ID，需先上传图片获取
    - access_token (Optional[str]): 可选。微信公众号访问令牌，如果不提供会使用环境变量中的WECHAT_ACCESS_TOKEN或自动获取
    返回值:
    - Dict[str, Any]: 包含发布结果的字典，包括状态和消息ID
    异常处理: 当access_token无效或获取失败时抛出ValueError异常，网络请求失败时抛出requests.exceptions.RequestException
    """
    token = access_token or WECHAT_ACCESS_TOKEN
    if not token:
        token = get_access_token(WECHAT_APP_ID, WECHAT_APP_SECRET)
    url = f"https://api.weixin.qq.com/cgi-bin/message/custom/send?access_token={token}"
    payload = {
        "touser": "OPENID",  # 实际使用时需要替换为具体的用户OpenID
        "msgtype": "image",
        "image": {
            "media_id": media_id
        }
    }
    response = requests.post(url, json=payload)
    data = response.json()
    if data.get('errcode') == 0:
        return {"status": "success", "message": "图片消息发布成功", "msgid": data.get('msgid')}
    else:
        raise ValueError(f"图片消息发布失败: {data}")

@mcp.tool()
def publish_news_message(articles: List[Dict[str, str]], access_token: Optional[str] = None) -> Dict[str, Any]:
    """
    功能描述: 发布图文消息到微信公众号
    参数说明:
    - articles (List[Dict[str, str]]): 必须。图文消息列表，每个元素包含title、description、url、picurl等字段
    - access_token (Optional[str]): 可选。微信公众号访问令牌，如果不提供会使用环境变量中的WECHAT_ACCESS_TOKEN或自动获取
    返回值:
    - Dict[str, Any]: 包含发布结果的字典，包括状态和消息ID
    异常处理: 当access_token无效或获取失败时抛出ValueError异常，网络请求失败时抛出requests.exceptions.RequestException
    """
    token = access_token or WECHAT_ACCESS_TOKEN
    if not token:
        token = get_access_token(WECHAT_APP_ID, WECHAT_APP_SECRET)
    url = f"https://api.weixin.qq.com/cgi-bin/message/custom/send?access_token={token}"
    payload = {
        "touser": "OPENID",  # 实际使用时需要替换为具体的用户OpenID
        "msgtype": "news",
        "news": {
            "articles": articles
        }
    }
    response = requests.post(url, json=payload)
    data = response.json()
    if data.get('errcode') == 0:
        return {"status": "success", "message": "图文消息发布成功", "msgid": data.get('msgid')}
    else:
        raise ValueError(f"图文消息发布失败: {data}")

@mcp.tool()
def send_template_message(openid: str, data: Dict[str, Dict[str, str]], access_token: Optional[str] = None) -> Dict[str, Any]:
    """
    功能描述: 发送模板消息到微信公众号用户
    参数说明:
    - openid (str): 必须。接收消息的用户OpenID
    - data (Dict[str, Dict[str, str]]): 必须。模板数据，包含模板字段和对应的值
    - access_token (Optional[str]): 可选。微信公众号访问令牌，如果不提供会使用环境变量中的WECHAT_ACCESS_TOKEN或自动获取
    返回值:
    - Dict[str, Any]: 包含发送结果的字典，包括状态和消息ID
    异常处理: 当access_token无效或获取失败时抛出ValueError异常，网络请求失败时抛出requests.exceptions.RequestException
    """
    token = access_token or WECHAT_ACCESS_TOKEN
    if not token:
        token = get_access_token(WECHAT_APP_ID, WECHAT_APP_SECRET)
    url = f"https://api.weixin.qq.com/cgi-bin/message/template/send?access_token={token}"
    payload = {
        "touser": openid,
        "template_id": WECHAT_TEMPLATE_ID,
        "data": data
    }
    response = requests.post(url, json=payload)
    data = response.json()
    if data.get('errcode') == 0:
        return {"status": "success", "message": "模板消息发送成功", "msgid": data.get('msgid')}
    else:
        raise ValueError(f"模板消息发送失败: {data}")

if __name__ == "__main__":
    mcp.run()