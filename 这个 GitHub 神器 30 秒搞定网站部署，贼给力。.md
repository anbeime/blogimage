原创 逛逛 逛逛GitHub

 _2025年11月18日 15:04_

![](http://mmbiz.qpic.cn/mmbiz_png/ePw3ZeGRruyXo8VzACicO8MVibibicuJUQ8Vzghx6WF8F51breYjBIuYd4cj6wp26BYrg850bNuA20rdic9UyKIUhpg/300?wx_fmt=png&wxfrom=19)

**逛逛GitHub**

热门「开源项目」推送到你眼前，每日为你节省 1 小时。 给我发消息可咨询各种开源项目，专注 AI、硬科技开源领域。

760篇原创内容

公众号

逛 GitHub 发现了一个快速部署网站的开源项目。在 AI 生成 HTML 前端页面成本极低的今天，这个开源项目相当有用。

这个叫 PinMe 的 GitHub 项目可以快速、免费、文档的部署 AI 生成的网页或 **Vue、React 项目。**

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/ePw3ZeGRruzuTSj6hib8AwQoiaQDSq7r81ztFAxVickzTic9JMYLngG1Jfa2fPut8LSag1In5WPbpDt2wucjx9hZzw/640?wx_fmt=png&from=appmsg&tp=wxpic&wxfrom=5&wx_lazy=1#imgIndex=0)

01

**开源项目介绍**

**PinMe 这个一键部署神器，能将静态网站快速部署到网上。搞出来一个链接，微信发出去，别人就能访问了。**

**它的原理是利用  IPFS（一种分布式存储网络）来存储文件，并自动生成一个免费的、基于 ENS 域名的永久链接。**

**无需 DNS，无需服务器。**

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/ePw3ZeGRruzuTSj6hib8AwQoiaQDSq7r81Pwaib1E3axRMib7PS6y1icdb94j8CQmH6lJqadAQRJ7prCibdKcMNw2R6Q/640?wx_fmt=png&from=appmsg&tp=wxpic&wxfrom=5&wx_lazy=1#imgIndex=1)

这个叫 PinMe 开源项目的主要优势是：

- 免费：0 元成本，传统方式仅域名和服务器一年约 300 元。
    
- 极速：30 秒上线，传统部署需要 30 分钟或更久。
    
- 稳定：依托 IPFS 网络，内容分布式存储，不易宕机，传统服务器挂了就无法访问。
    
- 便捷：支持两种方式上传网页拖拽零命令和命令行的方式。
    

```
开源地址：https://github.com/glitternetwork/pinme
```

02

**实战一下**

我使用两种方式，快速部署 AI 生成的静态网页。生成一个外链，谁都能访问。

首先，我让 AI ：搜索《思考快与慢》书籍的核心思想，生产一个美观的 html 网页介绍一下这本书。

① 上传网页的方式部署

可以浏览器打开 PinMe 开源项目官方网站的地址：

```
网站地址：https://pinme.eth.limo
```

![图片](data:image/svg+xml,%3C%3Fxml%20version='1.0'%20encoding='UTF-8'%3F%3E%3Csvg%20width='1px'%20height='1px'%20viewBox='0%200%201%201'%20version='1.1'%20xmlns='http://www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate\(-249.000000,%20-126.000000\)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

把 AI 生成的 HTML 或者将 Vue、React 项目打包好的 dist 文件夹直接拖进网页。

等待上传完成，复制生成的链接即可分享。

，时长00:12

② 使用命令的方式

使用 npm 安装 pinme，在项目目录下执行：pinme upload 命令就能获取链接，完成部署。

![图片](data:image/svg+xml,%3C%3Fxml%20version='1.0'%20encoding='UTF-8'%3F%3E%3Csvg%20width='1px'%20height='1px'%20viewBox='0%200%201%201'%20version='1.1'%20xmlns='http://www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate\(-249.000000,%20-126.000000\)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

然后使用 pinme upload 命令上传你的 html 文件或者部署打包的项目文件夹。

然后它就会返回一个任何人都能访问的 URL 了。

![图片](data:image/svg+xml,%3C%3Fxml%20version='1.0'%20encoding='UTF-8'%3F%3E%3Csvg%20width='1px'%20height='1px'%20viewBox='0%200%201%201'%20version='1.1'%20xmlns='http://www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate\(-249.000000,%20-126.000000\)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

，时长00:09

还有更多进阶的功能

比如可以集成到 GitHub Actions 中，实现代码一推送就自动构建和部署。

还能多环境管理，为测试、预览、正式环境部署不同的链接。还能查看部署历史，并删除旧版本。

如果你需要快速、免费地分享一个前端页面，比如 Demo、简历、作品集，**PinMe 提供了一个近乎完美的解决方案**，让你不再为临时部署而烦恼。

```
立即体验：https://pinme.eth.limo
```

03

**点击下方卡片，关注逛逛 GitHub**

![](http://mmbiz.qpic.cn/mmbiz_png/ePw3ZeGRruyXo8VzACicO8MVibibicuJUQ8Vzghx6WF8F51breYjBIuYd4cj6wp26BYrg850bNuA20rdic9UyKIUhpg/300?wx_fmt=png&wxfrom=19)

**逛逛GitHub**

热门「开源项目」推送到你眼前，每日为你节省 1 小时。 给我发消息可咨询各种开源项目，专注 AI、硬科技开源领域。

760篇原创内容

公众号

这个公众号历史发布过很多有趣的开源项目，如果你懒得翻文章一个个找，你直接关注微信公众号：逛逛 GitHub ，后台对话聊天就行了：

![图片](data:image/svg+xml,%3C%3Fxml%20version='1.0'%20encoding='UTF-8'%3F%3E%3Csvg%20width='1px'%20height='1px'%20viewBox='0%200%201%201'%20version='1.1'%20xmlns='http://www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate\(-249.000000,%20-126.000000\)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

你可以点击底部【阅读原文】跳转到开源项目地址，欢迎收藏 Star 一下。

开源工具 · 目录

上一篇1 个神级智能问数工具，刚开源就 1500 Star 了。

阅读原文

阅读 1.4万

​

[](javacript:;)

![](https://mmbiz.qpic.cn/mmbiz_png/ePw3ZeGRruyXo8VzACicO8MVibibicuJUQ8Vzghx6WF8F51breYjBIuYd4cj6wp26BYrg850bNuA20rdic9UyKIUhpg/300?wx_fmt=png&wxfrom=18)

逛逛GitHub

15个朋友关注

关注

218

1137

142

6

![](https://wx.qlogo.cn/mmopen/nMl9ssowtibXhmqFia0ooOah1ibXbE6bjXGaHPNARVCfUGGtwUU51HoQUPMadRHF3AwGF9icqTzDDXKibv8HM1NR2UickNnbhIEuvj/96)

复制搜一搜

复制搜一搜

暂无评论