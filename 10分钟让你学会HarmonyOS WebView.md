
**HarmonyOS WebView**

今天分享一下 在鸿蒙中使用webview开发，相信前端开发的同学们都遇到过内嵌webview的情况，微信小程序在这方面不是特别友好，尤其是h5和小程序之间的交互，在鸿蒙中与小程序还是稍有不同的。

  

Web组件提供基础的前端页面加载的能力，包括加载网络页面、本地页面、html格式文本数据。

  

Web组件提供丰富的页面交互的方式，包括：设置前端页面深色模式，新窗口中加载页面，位置权限管理，Cookie管理，应用侧使用前端页面JavaScript等能力。

  

**注意：使用 webview 一定要去开启网络权限，否则页面将无法加载**

  

**1.创建一个简单的 webview 页面**

  

**1.1 app端 创建 webview 页面**

```
// 1. 引入依赖
```

**2.app端 输出 h5 的日志**

  

- 正常情况下我们开发会有很多日志输出，开发过webview的同学都知道，h5的日志不太好看，除非使用Vconsole插件
    
- 鸿蒙对这个情况做的比较好，可以直接在app端的日志输出h5的日志
    
- 使用webvivew属性 OnConsole 监听h5的console.log输出，并在控制台输出日志
    
      
    

```
Web({ src: '自己本地随便启动一个项目地址', controller: this.controller })
```

  

**3.h5 和 app端 方法调用（数据传递）**

  

- 方法1：在鸿蒙中 h5 和 app端的交互是通过 window 来进行的
    
- h5 把方法挂载到 window 对象上，app端 可以通过固定方法调用
    
- app端 也可以通过固定api 把方法挂载到 window 对象上让 h5 调用。
    
- 如果要做数据传递，在方法中加上**返参**或者**回调**即可
    
- 方法2：可以通过双向数据通道进行数据传递
    
- 实际上就是通过 postMessage
    

  

**3.1 app端 调用 h5 的方法**

  

**3.1.1 h5 挂载方法到 window 对象上**

```
// 在 h5 中，监听window.onload事件，挂载方法 testA 到 window 对象上
```

**3.1.2 app端 调用 h5 的方法**

```
// app端 创建一个按钮，通过按钮触发 h5 中的 testA 方法
```

**3.2 h5 调用 app端 的方法**

**3.2.1 app端 挂载方法到 window 对象上**

  

- app端 需要创建一个事件对象
    
- 通过固定api挂载到 window对象上
    
- 根据api可以分为两种方式
    

  

**3.2.1.1 创建事件对象**

```
// 通过 class 创建一个全局公共类，里面包含一个方法 testB
```

**3.2.1.2 使用 web 属性 javaScriptProxy 挂载方法到 window 对象上**

```
// app端
```

**3.2.1.3 使用 webview 控制器的方法 registerJavaScriptProxy 挂载方法到 window 对象上，使用此方法后必须调用 refresh，方法才能生效**

```
// app端
```

**3.2.1.4 使用 webview 控制器的方法 registerJavaScriptProxy 挂载方法到 window 对象上，可以在声明周期 onControllerAttached 上调用该方法，此时 h5 还未加载**

```
Web({ src: '自己本地随便启动一个项目地址', controller: this.controller })
```

**3.2.1.5 h5 调用方法，不管 app端 咋么调用，h5 都通过 window 对象来调用**

  

```
// h5
```

**### 3.3 建立 app端 和 h5 双向数据通道**

  

- 1.创建双向数据通道接口
    

- 使用的 API
    
- webview 控制器方法 createWebMessagePorts()
    
- 返回值:
    
- 是一个数组, 数组内有两个接口 [ 接口1, 接口2 ]
    
- [0] : 提供给 h5端 使用的, 需要传递给 h5端, h5端 使用这个接口去监听 App端 发来的消息, 同时也是使用这个接口向 App 端发送消息
    
- [1] : 提供给 App端 使用的, App端 使用这个接口去监听 h5端 发来的消息, 同时也是使用这个接口向 h5端 发送消息
    

  

- 2.把属于 h5端 的接口传递过去
    

- 注意: 此时不是 App端 和 h5端 建立好通道传递
    
- 而是先把建立通道的 "工具" 传递过去
    
- 所以, 此时是 App端 给 window 发送一个消息( 而不是和 h5端 建立通道连接 )
    

  

- 3.建立通道
    

- 使用 webview 控制器方法 postMessage 把 "接口工具" 发过去
    
- App端 和 h5端 都利用 "接口工具" 去建立双向连接通道
    

  

**3.3.1 创建创建双向数据通道接口，并完成事件监听**

  

- 双向通道数据接口通过 webview 控制器方法 createWebMessagePorts() 创建
    

  

```
// ---------- app端
```

**3.3.2 发送消息**

  

- 发送消息通过 通道 发送
    

  

```
// app端
```