# 变现就看腾讯智能体平台搭建的微信支付的MCP，完成付费闭环最后一公里



读完这篇文章，别忘记给舰长点一个关注！舰长的智能体搭建文章，不仅是节点的构建，也有思路的分享。智能体搭建最重要的就是思路。最希望，能给大家带来不一样的搭建思路和方法。　

点一点上方的🔵蓝色小字关注，你的支持是我最大的动力！🙏谢谢啦！🌟"　

大家好！我是舰长🙏

最近腾讯的智能体开发平台—元器，发布了一个“微信支付MCP”的体验版，体验版的支付金额会“不知去向”也只能供大家自行测试体验。结尾有正式版（自己的收款账户）申请方法。

![Image](https://mmbiz.qpic.cn/mmbiz_png/sqr7oTe0d23wV6JTmkBCp4EHiabNmu7UkQ0Sht0WqAVvwCJRHrVzXLialGu1B4lb4VM58ic7z1MWVTIX7gLfuSZ4A/640?wx_fmt=png&from=appmsg&watermark=1&tp=wxpic&wxfrom=5&wx_lazy=1#imgIndex=1)

  

接下来舰长将带大家用一下微信支付的这个MCP，其实在很久之前支付宝的MCP 也是可以支付的，但微信支付不一样，因为在腾讯生态下。普通的支付需要返回二维码去扫码付款，而加载了微信支付MCP的智能体，在微信中打开会直接跳出支付页！

![Image](https://mmbiz.qpic.cn/mmbiz_png/sqr7oTe0d23wV6JTmkBCp4EHiabNmu7Uk8g0ricdiaTxaLIS5ZOqr0Zwicom4AXZ85vYVYU4ZdTyHUhjCZom9YYkTQ/640?wx_fmt=png&from=appmsg&watermark=1&tp=wxpic&wxfrom=5&wx_lazy=1#imgIndex=2)

![Image](https://mmbiz.qpic.cn/mmbiz_png/sqr7oTe0d23wV6JTmkBCp4EHiabNmu7Uk7YEBAjPOwck9GMhycVuZLEIfeqUo7hOicto3CRJBMnZePweXgxortrg/640?wx_fmt=png&from=appmsg&watermark=1&tp=wxpic&wxfrom=5&wx_lazy=1#imgIndex=3)

  

![Image](https://mmbiz.qpic.cn/mmbiz_png/sqr7oTe0d23wV6JTmkBCp4EHiabNmu7UkqAZBGAo7iatOZjKaeFUNeicLLNOPVnl3St2zDGu60RibFZ7h8zWQ0k0Hg/640?wx_fmt=png&from=appmsg&watermark=1&tp=wxpic&wxfrom=5&wx_lazy=1#imgIndex=4)

跟随舰长一起来测试一下微信支付MCP吧！正好给大家分享一篇腾讯元器的智能体工作流如何搭建：

元器智能体还是有很多优势的第一和微信生态很友好，像舰长这些写公众号比较多的博主就非常需要，因为腾讯元器可以获取舰长所有文章作为知识库使用。包括舰长现在使用的助手也是腾讯元器做的智能体，最起码在应用方面元器的知识库做的真的不错！

  

本次将带搭建搭建一个星座趋势每日分析智能体，知识点将涵盖：

1.元器智能体的搭建

2.元器工作流的搭建

3.微信支付MCP的使用

4.如何申请正式版的微信支付MCP

  

元器智能体平台：https://yuanqi.tencent.com/

![Image](https://mmbiz.qpic.cn/mmbiz_png/sqr7oTe0d23wV6JTmkBCp4EHiabNmu7UkCtGG2KOZsTl9mWvnBxPcTSTp0aZW6N6E1S7WoiaiaWAxqgEVbUerlsDw/640?wx_fmt=png&from=appmsg&watermark=1&tp=wxpic&wxfrom=5&wx_lazy=1#imgIndex=5)

  

### 创建工作流

点击我的创建——在点击工作流

![Image](https://mmbiz.qpic.cn/mmbiz_png/sqr7oTe0d23wV6JTmkBCp4EHiabNmu7UkB7U8Ba14YuiaHWwdUAS7SfiaicoX3RS6r66aLYZTiciafhVspEnAoc4YTAg/640?wx_fmt=png&from=appmsg&watermark=1&tp=wxpic&wxfrom=5&wx_lazy=1#imgIndex=6)

![Image](https://mmbiz.qpic.cn/mmbiz_png/sqr7oTe0d23wV6JTmkBCp4EHiabNmu7UkboSQmBUHbHQoicmakC6xibJAsJP8fg9wp4WV8Y6ykjsU2N4hxG6JnBtg/640?wx_fmt=png&from=appmsg&watermark=1&tp=wxpic&wxfrom=5&wx_lazy=1#imgIndex=7)

  

元器的工作流可以写中文，直接写上功能即可

![Image](https://mmbiz.qpic.cn/mmbiz_png/sqr7oTe0d23wV6JTmkBCp4EHiabNmu7UkaPH4UDgoYMibCsh4rTaP1T2QF9IJzCTpmA89C6qViaiabBwOHpUibc2ZuA/640?wx_fmt=png&from=appmsg&watermark=1&tp=wxpic&wxfrom=5&wx_lazy=1#imgIndex=8)

  

### 开始节点

元器的开始节点是没有变量的，需要手动填写一个"input"，参数描述也需要填写

而上面的参数有参考右边的解释，是为了跟好的去接受用户信息和聊天记录

![Image](https://mmbiz.qpic.cn/mmbiz_png/sqr7oTe0d23wV6JTmkBCp4EHiabNmu7UkiblQhQaYj9QeezicKvRW4JLdMBqzEaeZRUshny9sltbPicoNWHZAiaZpVg/640?wx_fmt=png&from=appmsg&watermark=1&tp=wxpic&wxfrom=5&wx_lazy=1#imgIndex=9)

  

### 添加插件

从左侧栏位中找到插件，点击“+”即可

![Image](https://mmbiz.qpic.cn/mmbiz_png/sqr7oTe0d23wV6JTmkBCp4EHiabNmu7UkEiber2ULtnic5y3koBfEGUObFDUXbIFBKkicGTAhrjTcN4ZG6WSWhU6Jg/640?wx_fmt=png&from=appmsg&watermark=1&tp=wxpic&wxfrom=5&wx_lazy=1#imgIndex=10)

  

点击节点后在点击添加插件

![Image](https://mmbiz.qpic.cn/mmbiz_png/sqr7oTe0d23wV6JTmkBCp4EHiabNmu7UkibtgJBgymcSQ6Uju4zafzQ9gHxj5CtKTMjewkIIwgfPxIAiceoGTNc9w/640?wx_fmt=png&from=appmsg&watermark=1&tp=wxpic&wxfrom=5&wx_lazy=1#imgIndex=11)

  

添加星座运势分析这款插件即可

![Image](https://mmbiz.qpic.cn/mmbiz_png/sqr7oTe0d23wV6JTmkBCp4EHiabNmu7UkxXxvOTUZiaUuTYOV7TxCkfj02aLt31VFf9S4a05ebJYJbX2yiakLWv4g/640?wx_fmt=png&from=appmsg&watermark=1&tp=wxpic&wxfrom=5&wx_lazy=1#imgIndex=12)

  

加入插件后整个版面会进行改动，变成插件的设置页面，该插件的输入只有一个，就是需要提供星座的名称，所以这里引用开始节点我们设置好的参数名为“input”的参数即可

![Image](https://mmbiz.qpic.cn/mmbiz_png/sqr7oTe0d23wV6JTmkBCp4EHiabNmu7UkjQ4Shiclj4vxSdB31GY3IgLUC3DTNKUA0wlDIOqIiaV1EQZGl6sxf4lQ/640?wx_fmt=png&from=appmsg&watermark=1&tp=wxpic&wxfrom=5&wx_lazy=1#imgIndex=13)

  

### 添加大语言模型

在左侧的栏位中添加大预言模型

![Image](https://mmbiz.qpic.cn/mmbiz_png/sqr7oTe0d23wV6JTmkBCp4EHiabNmu7Ukq2wia8sP8HL5ic8wC5MyuSh2gSWvDeP1picPoWWslSUHyrOOXrg4pV2QQ/640?wx_fmt=png&from=appmsg&watermark=1&tp=wxpic&wxfrom=5&wx_lazy=1#imgIndex=14)

  

元器中的大语言模型主流支持模型就是自家的混元大模型以及deepseek模型，有deepseek就好办了，直接用deepseek模型即可。

![Image](https://mmbiz.qpic.cn/mmbiz_png/sqr7oTe0d23wV6JTmkBCp4EHiabNmu7Uk3GzK5rvaF6EAXle65Y7851QkxkmaCGsxmc5q5hAJftqIJfalHohgiag/640?wx_fmt=png&from=appmsg&watermark=1&tp=wxpic&wxfrom=5&wx_lazy=1#imgIndex=15)

  

元器中的参数引用不太好找，但好在变量清晰，找到星座的插件输出在引用“data”即可

![Image](https://mmbiz.qpic.cn/mmbiz_png/sqr7oTe0d23wV6JTmkBCp4EHiabNmu7UkzcREYk9T5dGMUOW6ia0ibFlFLLic5pKaHQFZdicQ1zDIkQmyYII4QiaPyow/640?wx_fmt=png&from=appmsg&watermark=1&tp=wxpic&wxfrom=5&wx_lazy=1#imgIndex=16)

  

想要在元器中执行系统提示词需要开启箭头所指按钮，才可以进行使用

```
# 任务你是一名星座分析师，根据STORY中的内容，进行分析，并且给用户最好的的分析方案。只允许返回分析结果，其余思考过程以及废话不得输出
```

不能直接复制提示词，里面的变量引用需要重新用shift+{进行引用一次

本轮指令直接编写“直接执行流程”即可。

![Image](https://mmbiz.qpic.cn/mmbiz_png/sqr7oTe0d23wV6JTmkBCp4EHiabNmu7Uk2rGOO5iaOOicanlYblNTnHYKhuNEtaBJQeI9kobBp2u2xCsPckp7DeRA/640?wx_fmt=png&from=appmsg&watermark=1&tp=wxpic&wxfrom=5&wx_lazy=1#imgIndex=17)

  

### 结束节点

引用大语言模型的输出即可，也需要设置成置顶回复内容，并引用变量到输出模式框中

![Image](https://mmbiz.qpic.cn/mmbiz_png/sqr7oTe0d23wV6JTmkBCp4EHiabNmu7UknmkAheC2GURibFbI9M3rHOJVrhlaJkp1NywN9n9anKUqMnbiaic1SusgA/640?wx_fmt=png&from=appmsg&watermark=1&tp=wxpic&wxfrom=5&wx_lazy=1#imgIndex=18)

  

搭建好工作流后可以进行运行和发布，接下来配置到智能体当中即可

  

创建智能体——选择对话式智能体

![Image](https://mmbiz.qpic.cn/mmbiz_png/sqr7oTe0d23wV6JTmkBCp4EHiabNmu7Ukicex23voePFkDG4Fj5aOusWapib0ljRaU5JphtHYkSibDVUqPiaHpWamHA/640?wx_fmt=png&from=appmsg&watermark=1&tp=wxpic&wxfrom=5&wx_lazy=1#imgIndex=19)

  

元器的智能体一定要写名字，不写名字关闭网页后智能体就会消失

![Image](https://mmbiz.qpic.cn/mmbiz_png/sqr7oTe0d23wV6JTmkBCp4EHiabNmu7UkyrlVia5v5Cjo5O7ibpicZxgz2f4mK88IuLSX3oP44H4RKYmJ96UNJyoaQ/640?wx_fmt=png&from=appmsg&watermark=1&tp=wxpic&wxfrom=5&wx_lazy=1#imgIndex=20)

  

模型不要修改，默认的模型可以调用MCP

![Image](https://mmbiz.qpic.cn/mmbiz_png/sqr7oTe0d23wV6JTmkBCp4EHiabNmu7UkAhhPaD673Ba5LBQTfhjK3XJTcshialmZ7zksbdJnvxyNCUia05aACLew/640?wx_fmt=png&from=appmsg&watermark=1&tp=wxpic&wxfrom=5&wx_lazy=1#imgIndex=21)

  

接下来把微信支付的MCP和搭建好的工作流添加进来

![Image](https://mmbiz.qpic.cn/mmbiz_png/sqr7oTe0d23wV6JTmkBCp4EHiabNmu7UkmEMgZwy21nhxjgkPjuo31Zltrq8ibKFibEDTf896f6MyjZWf1DZnWfAg/640?wx_fmt=png&from=appmsg&watermark=1&tp=wxpic&wxfrom=5&wx_lazy=1#imgIndex=22)

  

回到基础设定中粘贴提示词即可

```
##星座分析前置要求当用户告诉你星座时1、你需要先调用【create-native-payment】这个工具，为用户生成1分钱支付的付款二维码链接，并将二维码链接(code url)展示给用户。2、并告知用户需要扫码付款来获取设计结果，同时告知用户付款后可以跟你说“我已赞赏”##验证付款当用户说已支付后，你需要调用【query-order-by-out-trade-no】这个工具，验证这个订单号是否是已支付状态，当验证是已支付时，为用户调用“调coze完整工作流”工作流进行分析，并给到输出结果
```

![Image](https://mmbiz.qpic.cn/mmbiz_png/sqr7oTe0d23wV6JTmkBCp4EHiabNmu7UkibNFmlcFs7gOm9jOibUdGpo1xQKcNohxtwIhP01tfyDzliax0farLlX6g/640?wx_fmt=png&from=appmsg&watermark=1&tp=wxpic&wxfrom=5&wx_lazy=1#imgIndex=23)

  

接下来就可以进行测试使用

![Image](https://mmbiz.qpic.cn/mmbiz_png/sqr7oTe0d23wV6JTmkBCp4EHiabNmu7UkEjI89RibtvuSIoVU9ecSR2RhUcWVFKHm5emVUszYgHqT3Q0lKlCsRqg/640?wx_fmt=png&from=appmsg&watermark=1&tp=wxpic&wxfrom=5&wx_lazy=1#imgIndex=24)

  

这样搭建出来的智能体是没有办法发布的，因为使用的是体验版的微信支付MCP，所以需要去申请正式版的微信支付MCP：

申请地址：https://wj.qq.com/s2/23001898/lpyn/

通过申请后就可以和自己的收款账户绑定进行收款，让使用者付费使用您的智能体

  

![Image](https://mmbiz.qpic.cn/mmbiz_png/sqr7oTe0d23wV6JTmkBCp4EHiabNmu7UkuMH3XMm3KsnmoaUBhBzvTKVxngy64d8iaOyzJmJL5mDWD29Xv3w6DMw/640?wx_fmt=png&from=appmsg&watermark=1&tp=wxpic&wxfrom=5&wx_lazy=1#imgIndex=25)

  

在申请表当中，最重要的就是您的智能体的链接，这个智能体是需要你搭建好且没有添加微信支付MCP（体验版）的智能体去申请即可。

![Image](https://mmbiz.qpic.cn/mmbiz_png/sqr7oTe0d23wV6JTmkBCp4EHiabNmu7Ukz9KLQ2pXA9FfyhZItj7rkjOY0Ls6MIK7c0CA72q8doZ1iaiakrb3EwLA/640?wx_fmt=png&from=appmsg&watermark=1&tp=wxpic&wxfrom=5&wx_lazy=1#imgIndex=26)

好了本次的分享就到～

  

关注公众号并添加舰长微信，领取智能体学习资料，并参与Coze技术直播讲解

![Image](https://mmbiz.qpic.cn/mmbiz_png/sqr7oTe0d23wV6JTmkBCp4EHiabNmu7Ukia1Wj573jX0Cicj044IaPYOoABm9tMpgicsvRucibicgrHosIEHbLfzOdMA/640?wx_fmt=png&from=appmsg&watermark=1&tp=wxpic&wxfrom=5&wx_lazy=1#imgIndex=27)

另外非常欢迎大家加入[唐舰长AI落地智能体交流群],主要交流群每周都会进行公益直播教大家搭建AI智能体工作流

![Image](https://mmbiz.qpic.cn/mmbiz_png/sqr7oTe0d23wV6JTmkBCp4EHiabNmu7UkrYUX6TdDZdpvoHyXb3bDHYGY4qzDx36hdTY65aSB0sfWiaSCvCRW8vw/640?wx_fmt=png&from=appmsg&watermark=1&tp=wxpic&wxfrom=5&wx_lazy=1#imgIndex=28)

![Image](https://mmbiz.qpic.cn/mmbiz_png/sqr7oTe0d23wV6JTmkBCp4EHiabNmu7UkszMxesmU2NTLZ0gO7OIqcvELv6s0gtXQaPkLRBg2ic2tYopoIxeSgvw/640?wx_fmt=png&from=appmsg&watermark=1&tp=wxpic&wxfrom=5&wx_lazy=1#imgIndex=29)

  

  

![](https://mmbiz.qlogo.cn/sz_mmbiz_jpg/BRGtHcDMdURGCLfwSxgrT1lP7OmdswVgEjpszdCkHWwXV9ia82ibibia8IloPce9ibicxyY16bCDuzmfnwvl4E1jx47Q/0?wx_fmt=jpeg)

杰克船长的AIGC

 谢谢您的鼓励 

钟意作者

阅读 2307

​

**留言 3**

作者已设置关注后可以留言

- ![](https://wx.qlogo.cn/finderhead/Jiavz9UrH80nKiaqliaAiaL1Uvxx1RZskX4Ar2RVwyarLU3yYibTYCEuOlw/64)
    
    码农奶爸学AI
    
    广东7月10日
    
    赞
    
    谢谢分享
    
- ![](https://wx.qlogo.cn/mmopen/SXryYH6DzyaRB1yJKXcuibrYly7gLm0ibwJibtcH8SdqZIsyvlqPobhc6gxpD2aaKLehLjmTcB673wnmKMIdPflJQ/64)
    
    杰克船长
    
    广东7月7日
    
    赞
    
    群二维码少了半截
    
    ![](https://wx.qlogo.cn/mmopen/gzmFd21gONSp1EibraPEwSFpGRGo4WNnCJPJiaTBBHgJ5KrDdLLf2tqpLh8gia1oIloNjsmUa7DynVY1uE5GJwicMribCdkr2U2ms/64)
    
    施玮
    
    江苏7月8日
    
    赞
    
    那咋加呢？
    

已无更多数据