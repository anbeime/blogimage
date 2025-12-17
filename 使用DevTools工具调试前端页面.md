# 使用DevTools工具调试前端页面

更新时间: 2025-12-16 16:38

Web组件支持使用DevTools工具调试前端页面。DevTools是Web前端开发调试工具，支持在电脑上调试移动设备前端页面。开发者通过[setWebDebuggingAccess()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#setwebdebuggingaccess)接口开启Web组件前端页面调试能力，使用DevTools在电脑上调试移动前端网页，设备需为4.1.0及以上版本。

## 无线调试

从API version 20开始，可使用无线调试接口[setWebDebuggingAccess20+](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#setwebdebuggingaccess20)，来简化调试流程。

### 应用代码开启Web调试开关

调试网页前，需要应用侧代码调用setWebDebuggingAccess()接口开启Web调试开关。

如果没有开启Web调试开关，则DevTools无法发现被调试的网页。

1. 在应用代码中开启Web调试开关，应用需要调用[setWebDebuggingAccess20+](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#setwebdebuggingaccess20)接口，设置TCP Socket端口号并启用Web调试功能。

2. // xxx.ets
3. import { webview } from '@kit.ArkWeb';
4. import { BusinessError } from '@kit.BasicServicesKit';

5. @Entry
6. @Component
7. struct WebComponent {
8.   controller: webview.WebviewController = new webview.WebviewController();

9.   aboutToAppear(): void {
10.     try {
11.       // 配置Web开启无线调试模式，指定TCP Socket的端口。
12.       webview.WebviewController.setWebDebuggingAccess(true, 8888);
13.     } catch (error) {
14.       console.error(`ErrorCode: ${(error as BusinessError).code},  Message: ${(error as BusinessError).message}`);
15.     }
16.   }

17.   build() {
18.     Column() {
19.       Web({ src: 'www.example.com', controller: this.controller })
20.     }
21.   }
22. }

说明

代码中使用的8888端口仅作为示例展示，开发者使用过程中，应保证端口号可以被应用使用。如果因为端口被占用或者应用无权限使用等因素导致端口无法被应用使用，会导致接口抛出异常或者ArkWeb无法开启调试模式。

1. 开启调试功能需要在DevEco Studio应用工程hap模块的module.json5文件中增加如下权限，添加方法请参考[在配置文件中声明权限](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/declare-permissions#%E5%9C%A8%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6%E4%B8%AD%E5%A3%B0%E6%98%8E%E6%9D%83%E9%99%90)。

2. "requestPermissions":[
3.    {
4.      "name" : "ohos.permission.INTERNET"
5.    }
6.  ]

### 在Chrome浏览器上打开调试工具页面

1. 在电脑端Chrome浏览器地址栏中输入调试工具地址 chrome://inspect/#devices 并打开该页面。
2. 修改Chrome调试工具的配置。
    
    确保已勾选 "Discover network targets"，以便从指定的IP地址和端口号发现被调试网页。
    
    (1) 点击 "Configure" 按钮。
    
    (2) 在 "Target discovery settings" 中添加被调试设备的IP地址和[setWebDebuggingAccess20+](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#setwebdebuggingaccess20)接口中指定的port端口，比如：192.168.0.3:8888。
    

说明

调试工具和被调试设备要在同一局域网下，并且能够相互访问。如果被调试设备有多个IP地址，要使用与调试工具同一个网段的IP地址。

### 等待发现被调试页面

如果前面的步骤执行成功，Chrome的调试页面将显示待调试的网页。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163828.98022088189509133056509219811688:50001231000000:2800:EB2A279B9EDC4AD7FFAAC0E987B2DECEA5FD9F2FE49EC899D901F5D6E771B2CB.jpg)

### 开始网页调试

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163828.66566578695371686979174062025640:50001231000000:2800:6AD2377DAC95B690EBF563475FE868927FA128C3A577BDDFC4F801249EB40741.png)

## USB连接调试

### 应用代码开启Web调试开关

调试网页前，需要应用侧代码调用[setWebDebuggingAccess()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#setwebdebuggingaccess)接口开启Web调试开关。

如果没有开启Web调试开关，则DevTools无法发现被调试的网页。

1. 在应用代码中开启Web调试开关，具体如下：
    
    1. // xxx.ets
    2. import { webview } from '@kit.ArkWeb';
    
    3. @Entry
    4. @Component
    5. struct WebComponent {
    6.   controller: webview.WebviewController = new webview.WebviewController();
    
    7.   aboutToAppear() {
    8.     // 配置Web开启调试模式
    9.     webview.WebviewController.setWebDebuggingAccess(true);
    10.   }
    
    11.   build() {
    12.     Column() {
    13.       Web({ src: 'www.example.com', controller: this.controller })
    14.     }
    15.   }
    16. }
    
2. 开启调试功能需要在DevEco Studio应用工程hap模块的module.json5文件中增加如下权限，添加方法请参考[在配置文件中声明权限](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/declare-permissions#%E5%9C%A8%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6%E4%B8%AD%E5%A3%B0%E6%98%8E%E6%9D%83%E9%99%90)。
    
    1. "requestPermissions":[
    2.    {
    3.      "name" : "ohos.permission.INTERNET"
    4.    }
    5.  ]
    

### 将设备连接至电脑

请将设备连接至电脑，随后开启开发者模式，为后续的端口转发操作做好准备。

1. 请开启设备上的开发者模式，并启用USB调试功能。
    
    (1) 终端系统查看“设置 > 系统”中是否有“开发者选项”，如果不存在，可在“设置 > 关于本机”连续七次单击“版本号”，直到提示“开启开发者模式”，点击“确认开启”后输入PIN码（如果已设置），设备将自动重启。
    
    (2) USB数据线连接终端和电脑，在“设置 > 系统 > 开发者选项”中，打开“USB调试”开关，弹出的“允许USB调试”的弹框，点击“允许”。
    
2. 使用hdc命令连接上设备。
    
    打开命令行执行如下命令，查看hdc能否发现设备。
    
    1. hdc list targets
    
    - 如果命令返回设备的ID，表示hdc已连接上设备。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163828.27635676583830908647484806416691:50001231000000:2800:96020FE88C2395F64ACC63ED6AF15DA3B10E94CF398659BFD597E57F0CB226AE.png)
        
    - 如果命令返回 [Empty]，则说明hdc还没有发现设备。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163828.75940432861503801157073151297052:50001231000000:2800:71545F433D6CDF8AA2F720C25A3371D2448F7A9904B5A7B80CDAA7319E403B13.jpg)
        
3. 进入hdc shell。
    
    连接设备后，执行以下命令进入hdc shell。
    
    1. hdc shell
    

### 端口转发

当应用代码调用setWebDebuggingAccess接口开启Web调试开关后，ArkWeb内核将启动一个domain socket的监听，以此实现DevTools对网页的调试功能。

Chrome浏览器无法直接访问到设备上的domain socket， 因此需要将设备上的domain socket转发到电脑上。

**推荐使用[自动映射WebView调试链接](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-run-debug-configurations#section48387420516)**。

若当前DevEco版本低，可参考以下方法：

1. 先在hdc shell里执行如下命令，查询ArkWeb在设备里创建的domain socket。
    
    1. cat /proc/net/unix | grep devtools
    
    - 如果前几步操作无误，该命令的执行结果将显示用于查询的domain socket端口。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163828.42536183812992592542057283721227:50001231000000:2800:485BE3AA434FF3568286F205A9B3F4304A5AB2DF3EA9B3B535A3F8347951F052.jpg)
        
    - 如果没有查询到结果， 请再次确认。
        
        (1) 应用开启了Web调试开关。
        
        (2) 应用使用Web组件加载了网页。
        
2. 将查询到的domain socket转发至电脑的TCP 9222端口。
    
    执行exit退出hdc shell。
    
    1. exit
    
    在命令行里执行如下命令转发端口。
    
    2. hdc fport tcp:9222 localabstract:webview_devtools_remote_38532
    
    说明
    
    "webview_devtools_remote_" 后面的数字，代表ArkWeb所在应用的进程号， 该数字不是固定的。请将”webview_devtools_remote_“后面的数字改为自己查询到的值。
    
    如果应用的进程号发生变化，例如，应用重新启动，则需要重新配置端口转发。
    
    命令执行成功示意图：
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163828.40542669833419236779588088073656:50001231000000:2800:6AFD9309BFF7CEB3022A2488893F2A54CC3C97A7E0A91567CAFEAA9D0E9C79FA.jpg)
    
3. 在命令行里执行如下命令，检查端口是否转发成功。
    
    1. hdc fport ls
    
    - 如果有返回端口转发的任务，则说明端口转发成功。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163828.30671779698650181887053155509747:50001231000000:2800:1E700BE5D4AA59932E495B62DC6D09381AAEADD0CCED08864B9583F80DB09E8E.png)
        
    - 如果返回 [Empty]， 则说明端口转发失败。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163828.22063406539817070560762569701402:50001231000000:2800:6BDB73190F0039E8CA254876F3BE24C5F52A7515BA701C25C7CE93EC58F48542.jpg)
        

### 便捷脚本

**Windows平台**

请复制以下信息创建bat文件，开启调试应用后执行。

1. @echo off
2. setlocal enabledelayedexpansion

3. :: Initialize port number and PID list
4. set PORT=9222
5. set PID_LIST=

6. :: Get the list of all forwarded ports and PIDs
7. for /f "tokens=2,5 delims=:_" %%a in ('hdc fport ls') do (
8.     if %%a gtr !PORT! (
9.         set PORT=%%a
10.     )
11.     for /f "tokens=1 delims= " %%c in ("%%b") do (
12.         set PID_LIST=!PID_LIST! %%c
13.     )
14. )

15. :: Increment port number for next application
16. set temp_PORT=!PORT!
17. set /a temp_PORT+=1
18. set PORT=!temp_PORT!

19. :: Get the domain socket name of devtools
20. for /f "tokens=*" %%a in ('hdc shell "cat /proc/net/unix | grep devtools"') do (
21.     set SOCKET_NAME=%%a

22.     :: Extract process ID
23.     for /f "delims=_ tokens=4" %%b in ("!SOCKET_NAME!") do set PID=%%b

24.     :: Check if PID already has a mapping
25.     echo !PID_LIST! | findstr /C:" !PID! " >nul
26.     if errorlevel 1 (
27.         :: Add mapping
28.         hdc fport tcp:!PORT! localabstract:webview_devtools_remote_!PID!
29.         if errorlevel 1 (
30.             echo Error: Failed to add mapping.
31.             pause
32.             exit /b
33.         )

34.         :: Add PID to list and increment port number for next application
35.         set PID_LIST=!PID_LIST! !PID!
36.         set temp_PORT=!PORT!
37.         set /a temp_PORT+=1
38.         set PORT=!temp_PORT!
39.     )
40. )

41. :: If no process ID was found, prompt the user to open debugging in their application code and provide the documentation link
42. if "!SOCKET_NAME!"=="" (
43.     echo No process ID was found. Please open debugging in your application code using the corresponding interface. You can find the relevant documentation at this link: [https://gitcode.com/openharmony/docs/blob/master/zh-cn/application-dev/web/web-debugging-with-devtools.md]
44.     pause
45.     exit /b
46. )

47. :: Check mapping
48. hdc fport ls

49. echo.
50. echo Script executed successfully. Press any key to exit...
51. pause >nul

52. :: Try to open the page in Edge
53. start msedge chrome://inspect/#devices

54. :: If Edge is not available, then open the page in Chrome
55. if errorlevel 1 (
56.     start chrome chrome://inspect/#devices
57. )

58. endlocal

**Linux或Mac平台**

请复制以下信息创建sh文件，注意chmod以及格式转换，开启调试应用后执行。

本脚本会先删除所有的端口转发，如果有其他的工具(如：DevEco Studio)也在使用端口转发功能，会受到影响。

1. #!/bin/bash

2. # Get current fport rule list
3. CURRENT_FPORT_LIST=$(hdc fport ls)

4. # Delete the existing fport rule one by one
5. while IFS= read -r line; do
6.     # Extract the taskline
7.     IFS=' ' read -ra parts <<< "$line"
8.     taskline="${parts[1]} ${parts[2]}"

9.     # Delete the corresponding fport rule
10.     echo "Removing forward rule for $taskline"
11.     hdc fport rm $taskline
12.     result=$?

13.     if [ $result -eq 0 ]; then
14.         echo "Remove forward rule success, taskline:$taskline"
15.     else
16.         echo "Failed to remove forward rule, taskline:$taskline"
17.     fi

18. done <<< "$CURRENT_FPORT_LIST"

19. # Initial port number
20. INITIAL_PORT=9222

21. # Get the current port number, use initial port number if not set previously
22. CURRENT_PORT=${PORT:-$INITIAL_PORT}

23. # Get the list of all PIDs that match the condition
24. PID_LIST=$(hdc shell cat /proc/net/unix | grep webview_devtools_remote_ | awk -F '_' '{print $NF}')

25. if [ -z "$PID_LIST" ]; then
26.     echo "Failed to retrieve PID from the device"
27.     exit 1
28. fi

29. # Increment the port number
30. PORT=$CURRENT_PORT

31. # Forward ports for each application one by one
32. for PID in $PID_LIST; do
33.     # Increment the port number
34.     PORT=$((PORT + 1))

35.     # Execute the hdc fport command
36.     hdc fport tcp:$PORT localabstract:webview_devtools_remote_$PID

37.     # Check if the command executed successfully
38.     if [ $? -ne 0 ]; then
39.         echo "Failed to execute hdc fport command"
40.         exit 1
41.     fi
42. done

43. # List all forwarded ports
44. hdc fport ls

### 在Chrome浏览器上打开调试工具页面

1. 在电脑端Chrome浏览器地址栏中输入调试工具地址 chrome://inspect/#devices 并打开该页面。
    
2. 修改Chrome调试工具的配置。
    
    需要从本地的TCP 9222端口发现被调试网页，所以请确保已勾选 "Discover network targets"。然后再进行网络配置。
    
    (1) 点击 "Configure" 按钮。
    
    (2) 在 "Target discovery settings" 中添加要监听的本地端口localhost:9222。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163828.53308143251100350114540105604261:50001231000000:2800:C84F3183A8BF23BA9BE9BB59E59765673CFFD857961FB23E88D123B13264F389.jpg)
    
3. 为了同时调试多个应用，请在Chrome浏览器的调试工具网页内，于“Devices”选项中的“configure”部分添加多个端口号。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163829.02381185823420455288078170254636:50001231000000:2800:C4BBC06FEA7E3B54232D4F554553FE688724063E968764A138952FD95817A54B.png)
    

### 等待发现被调试页面

如果前面的步骤执行成功，Chrome的调试页面将显示待调试的网页。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163829.76768686571588470717970987552748:50001231000000:2800:C01DE67EEF2305C2EBDAA0502D0573232EFED111D602FD08E86795A7DAA155B4.jpg)

### 开始网页调试

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163829.16779607935999526127598932924887:50001231000000:2800:E46DDD07D398C85B4B868389539C12B06446E99B14386031D068DC7EAE16C30B.png)

## 常见问题与解决方法

### 可以调试系统浏览器打开的网页吗？

能否调试系统浏览器打开的网页，取决于系统浏览器是否开启Web调试开关。

- 当前系统浏览器已启用Web调试开关，可继续执行[USB连接调试](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-debugging-with-devtools#usb%E8%BF%9E%E6%8E%A5%E8%B0%83%E8%AF%95)中的后续步骤。

### hdc无法发现设备

**问题现象**

在命令行里执行如下命令后，没有列出设备ID。

1. hdc list targets

**解决方法**

- 请确保设备上的USB调试开关已开启。
- 请确保设备与电脑相连。

### hdc的命令显示设备"未授权"或"unauthorized"

**问题现象**

执行hdc命令时，提示设备"未授权"或"unauthorized"。

**问题原因**

设备没有授权该台电脑进行调试。

**解决方法**

开启USB调试开关的设备连接没有授权的电脑后，会弹框提示"是否允许USB调试？"，请选择允许。

### 找不到DevTools的domain socket

**问题现象**

在hdc shell里执行如下命令后，没有结果。

1. cat /proc/net/unix | grep devtools

**解决方法**

- 请确保应用[开启了Web调试开关](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-debugging-with-devtools#%E5%BA%94%E7%94%A8%E4%BB%A3%E7%A0%81%E5%BC%80%E5%90%AFweb%E8%B0%83%E8%AF%95%E5%BC%80%E5%85%B3)。
- 请确保应用使用Web组件加载了网页。

### 端口转发不成功

**问题现象**

在命令行里执行如下命令后，没有列出之前设置过转发任务。

1. hdc fport ls

**解决方法**

- 请确保设备里的domain socket存在。
- 请确保电脑端的tcp:9222没有被占用。
    
    如果tcp:9222被占用，可以将domain socket转发到其他未被占用的TCP端口， 比如9223等。
    
    如果转发到了新的TCP端口， 需要同步修改电脑端Chrome浏览器"Target discovery settings"中的端口号。
    

### 端口转发成功后，电脑端Chrome无法发现被调试网页

**问题现象**

电脑端Chrome浏览器无法发现被调试网页。

**问题原因**

端口转发失效可能是以下原因：

- 设备与电脑断连，会导致hdc里的所有转发任务被清空。
- hdc服务重启，也会导致hdc里的所有转发任务被清空。
- 设备里应用的进程号发生了变更（应用重新启动等），会导致hdc里旧的转发任务失效。
- 多个转发任务转发到了同一个端口等异常配置，会导致转发异常。

**解决方法**

- 请确保电脑端的本地tcp:9222（其他TCP端口同理）没有被占用。
    
- 请确保设备端的domain socket还存在。
    
- 请确保domain socket名称里的进程号与被调试的应用的进程号相同。
    
- 请删除hdc里其他不必要的转发任务。
    
- 转发成功后，请用电脑端的Chrome浏览器打开网址 [http://localhost:9222/json](http://localhost:9222/json) ，URL里的9222需要改为自己实际配置的TCP端口。
    
    - 如果网页有内容， 说明端口转发成功，请在Chrome的调试页面[等待被调试页面的出现](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-debugging-with-devtools#%E7%AD%89%E5%BE%85%E5%8F%91%E7%8E%B0%E8%A2%AB%E8%B0%83%E8%AF%95%E9%A1%B5%E9%9D%A2)。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163829.14133337921900292963179800830868:50001231000000:2800:448D668D7B534795C2DD09959AC3FA2C53DCBEAE1040F14A1E62BC8FB1FA0ED4.jpg)
        
    - 如果展示的是错误网页， 说明端口转发失败， 请参阅[端口转发不成功](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-debugging-with-devtools#%E7%AB%AF%E5%8F%A3%E8%BD%AC%E5%8F%91%E4%B8%8D%E6%88%90%E5%8A%9F)中的解决方法。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163829.58794300635682116505227558514615:50001231000000:2800:CFF2D0F327CCD535A97F13000968BFCB80D12ABD4609EF8FCE23428201249D7C.jpg)
        
- 电脑端Chrome浏览器打开 [http://localhost:9222/json](http://localhost:9222/json) 页面有内容，但是Chrome的调试工具界面还是无法发现调试目标。
    
    - 请确保Chrome调试工具界面的 "Configure" 中配置的端口号，与端口转发指定的TCP端口号一致。
    - 在本文档中，默认使用的TCP端口号为9222。
        
        如果开发者使用了其他的TCP端口号(比如9223)，请同时修改[端口转发](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-debugging-with-devtools#%E7%AB%AF%E5%8F%A3%E8%BD%AC%E5%8F%91)中的TCP端口号和[Chrome调试工具界面"Configure"配置](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-debugging-with-devtools#%E5%9C%A8chrome%E6%B5%8F%E8%A7%88%E5%99%A8%E4%B8%8A%E6%89%93%E5%BC%80%E8%B0%83%E8%AF%95%E5%B7%A5%E5%85%B7%E9%A1%B5%E9%9D%A2)中的端口号。
        

### 开启了无线调试模式后，电脑端Chrome无法发现被调试网页

**问题现象**

ArkWeb开启了无线调试模式后，电脑端Chrome浏览器无法发现被调试网页。

**问题原因**

- 无线调试模式没有成功开启。
- 调试工具和被调试设备之间网络不通。

**解决方法**

- 请确保使用的端口可以被应用使用。
- 请确保调试工具和被调试设备在同一个局域网内，且它们之间网络通畅。

### Web组件无法使用DevTools工具进行调试

**问题现象**

电脑端Chrome浏览器无法发现被调试网页。

**问题原因**

- 当同时使用HDC和ADB时，ADB会干扰DevTools与设备之间的WebSocket连接。

**解决方法**

- 如果同时使用HDC和ADB，先关闭ADB进程，确保DevTools与设备建立WebSocket连接。

### 使用DevTools工具进行调试出现404报错

**问题现象**

在电脑端Chrome浏览器中调试网页时，出现报错：“HTTP/1.1 404 Not Found”。

**问题原因**

- Chrome浏览器版本较低，导致无法使用DevTools调试。

**解决方法**

- 方案一，将电脑端Chrome升级到最新版本。
- 方案二，如果不希望升级浏览器，可以手动拼接调试URL。完整的URL链接为：“devtools://devtools/bundled/inspector.html?ws=localhost:9222/devtools/page/xxx”。
    - 该链接由两部分组成：“devtools://devtools/bundled/inspector.html”前半段固定不变。“?ws=localhost:9222/devtools/page/xxx”后半段需要根据实际配置修改。
    - 端口转发成功后，使用Chrome浏览器打开 [http://localhost:9222/json](http://localhost:9222/json) 页面。请注意，URL中的9222应替换为实际配置的TCP端口。然后取“devtoolsFrontendUrl”后的value值“?ws”及其后部分。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-debugging "Web调试维测")
# 使用crashpad收集Web组件崩溃信息

更新时间: 2025-12-16 16:38

Web组件支持使用crashpad记录进程崩溃信息。crashpad是chromium内核提供的进程崩溃信息处理工具，在应用使用Web组件导致的进程（Web渲染进程）崩溃出现后，crashpad会在应用主进程沙箱目录写入minidump文件。该文件为二进制格式，后缀为dmp，其记录了进程崩溃的原因、线程信息、寄存器信息等，应用可以使用该文件分析Web组件相关进程崩溃问题。

使用步骤如下：

1. 在应用使用Web组件导致的进程崩溃出现后，会在应用主进程沙箱目录下产生对应的dmp文件，对应的沙箱路径如下：
    
    1. /data/storage/el2/log/crashpad
    
2. 参考[Native访问应用沙箱](https://developer.huawei.com/consumer/cn/doc/best-practices/bpta-file-native-side)实现访问应用沙箱dmp文件。
    
3. 获取dmp文件后进行解析，具体步骤如下：
    
    - 通过minidump_stackwalk工具解析dmp文件，可以得到上述dmp文件对应的进程崩溃信息（崩溃的原因、线程信息、寄存器信息等），示例如下（Linux环境）：
        
        1. ./minidump_stackwalk b678e0b5-894b-4794-9ab3-fb5d6dda06a3.dmp > parsed_stacktrace.txt
        
        minidump_stackwalk由breakpad项目源码编译得到，编译方法见项目仓库：[breakpad仓库地址](https://chromium.googlesource.com/breakpad/breakpad)。
        
    - 查看解析后的文件，以下示例列出部分内容：
        
        1. Crash reason:  SIGSEGV /SEGV_MAPERR    表示导致进程crash的信号，此处示例为段错误
        2. Crash address: 0x0
        3. Process uptime: 12 seconds
        
        4. Thread 0 (crashed)                     表示Thread 0发生crash
        5.  0  libweb_engine.so + 0x2e0b340       0层调用栈，0x2e0b340为so偏移地址，可用来反编译解析crash源码（依赖unstripped so）
        6.      x0 = 0x00000006a5719ff8    x1 = 0x000000019a5a28c0
        7.      x2 = 0x0000000000020441    x3 = 0x00000000000001b6
        8.      x4 = 0x0000000000000018    x5 = 0x0000000000008065
        9.      x6 = 0x0000000000008065    x7 = 0x63ff686067666d60
        10.      x8 = 0x0000000000000000    x9 = 0x5f129cf9e7bf008c
        11.     x10 = 0x0000000000000001   x11 = 0x0000000000000000
        12.     x12 = 0x000000069bfcc6d8   x13 = 0x0000000009a1746e
        13.     x14 = 0x0000000000000000   x15 = 0x0000000000000000
        14.     x16 = 0x0000000690df4850   x17 = 0x000000010c0d47f8
        15.     x18 = 0x0000000000000000   x19 = 0x0000005eea827db8
        16.     x20 = 0x0000005eea827c38   x21 = 0x00000006a56b1000
        17.     x22 = 0x00000006a8b85020   x23 = 0x00000020002103c0
        18.     x24 = 0x00000006a56b8a70   x25 = 0x0000000000000000
        19.     x26 = 0x00000006a8b84e00   x27 = 0x0000000000000001
        20.     x28 = 0x0000000000000000    fp = 0x0000005eea827c10
        21.      lr = 0x000000069fa4b33c    sp = 0x0000005eea827c10
        22.      pc = 0x000000069fa4b340
        23.     Found by: given as instruction pointer in context
        24.  1  libweb_engine.so + 0x2e0b338
        25.      fp = 0x0000005eea827d80    lr = 0x000000069fa48d44
        26.      sp = 0x0000005eea827c20    pc = 0x000000069fa4b33c
        27.     Found by: previous frame's frame pointer
        28.  2  libweb_engine.so + 0x2e08d40
        29.      fp = 0x0000005eea827e50    lr = 0x00000006a385cef8
        30.      sp = 0x0000005eea827d90    pc = 0x000000069fa48d44
        31.     Found by: previous frame's frame pointer
        32.  3  libweb_engine.so + 0x6c1cef4
        33.      fp = 0x0000005eea828260    lr = 0x00000006a0f11298
        34.      sp = 0x0000005eea827e60    pc = 0x00000006a385cef8
        35.  ......
        
    - 使用llvm工具链解析crash源码位置，示例如下（Linux环境）：
        
        1. ./llvm-addr2line -Cfpie libweb_engine.so 0x2e0b340
        
        llvm-addr2line工具链位于sdk中。
        

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-debugging-with-devtools "使用DevTools工具调试前端页面")
# 定位与解决Web白屏问题

更新时间: 2025-12-16 16:38

Web页面出现白屏的原因众多，本文列举了若干常见白屏问题的排查步骤，供开发者快速定位。

1. 首先排查权限和网络状态。
2. 通过[使用DevTools工具调试前端页面](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-debugging-with-devtools)定位具体报错类型（跨域、资源404、JS异常）。
3. 在复杂布局场景中，排查渲染模式及组件约束条件的问题。
4. 处理H5代码兼容性问题。
5. 从日志中排查生命周期和网络加载相关关键字。
6. 检查是否开启坚盾守护模式，坚盾守护模式开启后相关限制见：[坚盾守护模式](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-secure-shield-mode#arkweb%E9%99%90%E5%88%B6%E7%9A%84html5%E7%89%B9%E6%80%A7)。

## 检查权限和网络状态

如果应用未开启联网或文件访问权限或者设备网络状态不佳，将导致Web组件加载失败或页面元素缺失，进而引起白屏。

- 验证设备的网络状态，包括是否已连接网络，设备自带的浏览器能否正常访问网页等（在线页面场景）。
    
- 确保应用已添加网络权限：ohos.permission.INTERNET（在线页面必需）。
    
    1. // 在module.json5中添加相关权限
    2. "requestPermissions":[
    3.    {
    4.       "name" : "ohos.permission.INTERNET"
    5.    }
    6. ]
    
- 开启相关权限：
    
    |名称|说明|
    |:--|:--|
    |[domStorageAccess](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#domstorageaccess)|DOM Storage API权限，若不开启，无法使用localStorage存储数据，任何调用localStorage的代码都将失效，依赖本地存储的功能会异常。|
    |[fileAccess](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#fileaccess)|‌若不开启，文件读写功能完全被阻断，依赖文件的模块会崩溃。|
    |[imageAccess](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#imageaccess)|设置是否允许自动加载图片资源。|
    |[onlineImageAccess](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#onlineimageaccess)|设置是否允许从网络加载图片资源（通过HTTP和HTTPS访问的资源）。|
    |[javaScriptAccess](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#javascriptaccess)|设置是否允许执行JavaScript脚本。|
    
    1. // xxx.ets
    2. import { webview } from '@kit.ArkWeb';
    
    3. @Entry
    4. @Component
    5. struct WebComponent {
    6.   controller: webview.WebviewController = new webview.WebviewController();
    
    7.   build() {
    8.     Column() {
    9.       Web({ src: 'www.example.com', controller: this.controller })
    10.         .domStorageAccess(true)
    11.         .fileAccess(true)
    12.         .imageAccess(true)
    13.         .onlineImageAccess(true)
    14.         .javaScriptAccess(true)
    15.     }
    16.   }
    17. }
    
- 修改[UserAgent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#setcustomuseragent10)后再观察页面是否恢复正常。
    
    1. // xxx.ets
    2. import { webview } from '@kit.ArkWeb';
    3. import { BusinessError } from '@kit.BasicServicesKit';
    
    4. @Entry
    5. @Component
    6. struct WebComponent {
    7.   controller: webview.WebviewController = new webview.WebviewController();
    8.   @State customUserAgent: string = ' DemoApp';
    
    9.   build() {
    10.     Column() {
    11.       Web({ src: 'www.example.com', controller: this.controller })
    12.       .onControllerAttached(() => {
    13.         console.info("onControllerAttached");
    14.         try {
    15.           let userAgent = this.controller.getUserAgent() + this.customUserAgent;
    16.           this.controller.setCustomUserAgent(userAgent);
    17.         } catch (error) {
    18.           console.error(`ErrorCode: ${(error as BusinessError).code},  Message: ${(error as BusinessError).message}`);
    19.         }
    20.       })
    21.     }
    22.   }
    23. }
    

## 使用DevTools工具进行页面内容验证

在确保网络与权限配置无误后，若仍出现白屏，则应利用DevTools工具调试前端页面以及监听Web相关错误上报接口，来定位具体报错类型。

1. 查阅控制台的错误信息，定位具体的资源加载失败问题。资源加载失败会导致页面元素缺失，布局紊乱，图片和动画效果失效等，严重时可能导致渲染进程崩溃，页面呈现空白。如图所示，依次排查：
    
    （1）元素是否完整，html元素、结构是否正确。
    
    （2）控制台是否有报错。
    
    （3）网络里面是否有资源加载时间特别长等。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163840.31716823875676273731566287504312:50001231000000:2800:904BD52120D8E6794ED2965EE51CD88D9A0ADF78FB649D2289B8AC0AA21048ED.png)
    
2. 检查控制台，确认是否存在因MixedContent策略或CORS策略导致的异常，或JS错误等。可参考[解决Web组件本地资源跨域问题](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-cross-origin)。为了提高安全性，ArkWeb内核禁止file协议和resource协议访问跨域请求。因此，在使用Web组件加载本地离线资源的时候，Web组件会拦截file协议和resource协议的跨域访问。Web组件无法访问本地跨域资源时，DevTools控制台会显示报错信息：
    
    1. Access to script at 'xxx' from origin 'xxx' has been blocked by CORS policy: Cross origin requests are only supported for protocol schemes:   http, arkweb, data, chrome-extension, chrome, https, chrome-untrusted.
    
    有如下两种解决方法：
    
    方法一：
    
    开发者应使用http或https协议替代file或resource协议，确保Web组件能够成功访问跨域资源。替代的URL域名应为自定义构造，仅限于个人或组织使用，以防止与互联网上的实际域名冲突。此外，开发者需要利用Web组件的[onInterceptRequest](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#oninterceptrequest9)方法，对本地资源进行拦截和相应替换。
    
    以下结合示例说明如何使用http或者https等协议解决本地资源跨域访问失败的问题。其中，index.html和js/script.js文件置于工程的rawfile目录下。当使用resource协议访问index.html时，js/script.js文件因跨域而被拦截，无法加载。在示例中，使用https://www.example.com/域名替换了原有的resource协议，同时利用onInterceptRequest接口替换资源，确保js/script.js文件可以成功加载，从而解决跨域拦截问题。
    
    2. // main/ets/pages/Index.ets
    3. import { webview } from '@kit.ArkWeb';
    
    4. @Entry
    5. @Component
    6. struct Index {
    7.   @State message: string = 'Hello World';
    8.   webviewController: webview.WebviewController = new webview.WebviewController();
    9.   // 构造域名和本地文件的映射表
    10.   schemeMap = new Map([
    11.     ["https://www.example.com/index.html", "index.html"],
    12.     ["https://www.example.com/js/script.js", "js/script.js"],
    13.   ])
    14.   // 构造本地文件和构造返回的格式mimeType
    15.   mimeTypeMap = new Map([
    16.     ["index.html", 'text/html'],
    17.     ["js/script.js", "text/javascript"]
    18.   ])
    
    19.   build() {
    20.     Row() {
    21.       Column() {
    22.         // 针对本地index.html,使用http或者https协议代替file协议或者resource协议，并且构造一个属于自己的域名。
    23.         // 本例中构造www.example.com为例。
    24.         Web({ src: "https://www.example.com/index.html", controller: this.webviewController })
    25.           .javaScriptAccess(true)
    26.           .fileAccess(true)
    27.           .domStorageAccess(true)
    28.           .geolocationAccess(true)
    29.           .width("100%")
    30.           .height("100%")
    31.           .onInterceptRequest((event) => {
    32.             if (!event) {
    33.               return;
    34.             }
    35.             // 此处匹配自己想要加载的本地离线资源，进行资源拦截替换，绕过跨域
    36.             if (this.schemeMap.has(event.request.getRequestUrl())) {
    37.               let rawfileName: string = this.schemeMap.get(event.request.getRequestUrl())!;
    38.               let mimeType = this.mimeTypeMap.get(rawfileName);
    39.               if (typeof mimeType === 'string') {
    40.                 let response = new WebResourceResponse();
    41.                 // 构造响应数据，如果本地文件在rawfile下，可以通过如下方式设置
    42.                 response.setResponseData($rawfile(rawfileName));
    43.                 response.setResponseEncoding('utf-8');
    44.                 response.setResponseMimeType(mimeType);
    45.                 response.setResponseCode(200);
    46.                 response.setReasonMessage('OK');
    47.                 response.setResponseIsReady(true);
    48.                 return response;
    49.               }
    50.             }
    51.             return null;
    52.           })
    53.       }
    54.       .width('100%')
    55.     }
    56.     .height('100%')
    57.   }
    58. }
    
    59. <!-- main/resources/rawfile/index.html -->
    60. <!DOCTYPE html>
    61. <html>
    62. <head>
    63.     <meta name="viewport" content="width=device-width,initial-scale=1">
    64. </head>
    65. <body>
    66.   <script crossorigin src="./js/script.js"></script>
    67. </body>
    68. </html>
    
    69. // main/resources/rawfile/js/script.js
    70. const body = document.body;
    71. const element = document.createElement('div');
    72. element.textContent = 'success';
    73. body.appendChild(element);
    
    方法二：
    
    通过[setPathAllowingUniversalAccess](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#setpathallowinguniversalaccess12)设置一个路径列表。当使用file协议访问该列表中的资源时，允许进行跨域访问本地文件。此外，一旦设置了路径列表，file协议将仅限于访问列表内的资源(此时，[fileAccess](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#fileaccess)的行为将会被此接口行为覆盖)。路径列表中的路径应符合以下任一路径格式：
    
    1.应用文件目录通过[Context.filesDir](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inner-application-context#context)获取，其子目录示例如下：
    
    - /data/storage/el2/base/files/example
    - /data/storage/el2/base/haps/entry/files/example
    
    2.应用资源目录通过[Context.resourceDir](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inner-application-context#context)获取，其子目录示例如下：
    
    - /data/storage/el1/bundle/entry/resource/resfile
    - /data/storage/el1/bundle/entry/resource/resfile/example
    
    3.从API version 21开始，还包括了应用缓存目录通过[Context.cacheDir](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inner-application-context#context)获取，其子目录示例如下：
    
    - /data/storage/el2/base/cache
    - /data/storage/el2/base/haps/entry/cache/example
    - 设置的目录路径中，不允许包含cache/web，否则会抛出异常码401。如果设置目录路径是cache，cache/web也不允许访问。
    
    4.从API version 21开始，还包括了应用临时目录通过[Context.tempDir](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inner-application-context#context)获取，其子目录示例如下：
    
    - /data/storage/el2/base/temp
    - /data/storage/el2/base/haps/entry/temp/example
    
    当路径列表中的任一路径不满足上述条件时，系统将抛出异常码401，并判定路径列表设置失败。如果路径列表设置为空，file协议的可访问范围将遵循[fileAccess](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#fileaccess)规则，具体示例如下。
    
    1. // main/ets/pages/Index.ets
    2. import { webview } from '@kit.ArkWeb';
    3. import { BusinessError } from '@kit.BasicServicesKit';
    
    4. @Entry
    5. @Component
    6. struct WebComponent {
    7.   controller: WebviewController = new webview.WebviewController();
    8.   uiContext: UIContext = this.getUIContext();
    
    9.   build() {
    10.     Row() {
    11.       Web({ src: "", controller: this.controller })
    12.         .onControllerAttached(() => {
    13.           try {
    14.             // 设置允许可以跨域访问的路径列表
    15.             this.controller.setPathAllowingUniversalAccess([
    16.               this.uiContext.getHostContext()!.resourceDir,
    17.               this.uiContext.getHostContext()!.filesDir + "/example"
    18.             ])
    19.             this.controller.loadUrl("file://" + this.uiContext.getHostContext()!.resourceDir + "/index.html")
    20.           } catch (error) {
    21.             console.error(`ErrorCode: ${(error as BusinessError).code}, Message: ${(error as BusinessError).message}`);
    22.           }
    23.         })
    24.         .javaScriptAccess(true)
    25.         .fileAccess(true)
    26.         .domStorageAccess(true)
    27.     }
    28.   }
    29. }
    
    30. <!-- main/resources/resfile/index.html -->
    31. <!DOCTYPE html>
    32. <html lang="en">
    
    33. <head>
    34.     <meta charset="utf-8">
    35.     <title>Demo</title>
    36.     <meta name="viewport" content="width=device-width, initial-scale=1, user-scalable=no, viewport-fit=cover">
    37.     <script>
    38.         function getFile() {
    39.             var file = "file:///data/storage/el1/bundle/entry/resources/resfile/js/script.js";
    40.       // 使用file协议通过XMLHttpRequest跨域访问本地js文件。
    41.             var xmlHttpReq = new XMLHttpRequest();
    42.             xmlHttpReq.onreadystatechange = function(){
    43.                 console.info("readyState:" + xmlHttpReq.readyState);
    44.                 console.info("status:" + xmlHttpReq.status);
    45.                 if(xmlHttpReq.readyState == 4){
    46.                     if (xmlHttpReq.status == 200) {
    47.                 // 如果ets侧正确设置路径列表，则此处能正常获取资源
    48.                         const element = document.getElementById('text');
    49.                         element.textContent = "load " + file + " success";
    50.                     } else {
    51.                 // 如果ets侧不设置路径列表，则此处会触发CORS跨域检查错误
    52.                         const element = document.getElementById('text');
    53.                         element.textContent = "load " + file + " failed";
    54.                     }
    55.                 }
    56.             }
    57.             xmlHttpReq.open("GET", file);
    58.             xmlHttpReq.send(null);
    59.         }
    60.     </script>
    61. </head>
    
    62. <body>
    63.   <div class="page">
    64.       <button id="example" onclick="getFile()">loadFile</button>
    65.   </div>
    66. <div id="text"></div>
    67. </body>
    
    68. </html>
    
    69. // main/resources/resfile/js/script.js
    70. const body = document.body;
    71. const element = document.createElement('div');
    72. element.textContent = 'success';
    73. body.appendChild(element);
    
3. 查看onErrorReceive、onHttpErrorReceive、onSslErrorEvent、onHttpAuthRequest、onClientAuthenticationRequest等错误上报接口是否有被调用。请根据返回的错误码，对照[网络协议栈错误列表](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-neterrorlist)进行排查。
    
    |名称|说明|
    |:--|:--|
    |[onErrorReceive](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onerrorreceive)|资源加载失败会上报该回调，比如访问内核不支持的scheme， 会报302(UNKNOWN_URL_SCHEME)。|
    |[onHttpErrorReceive](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onhttperrorreceive)|服务器返回HTTP错误码，这类问题一般需要跟服务器进行联调。|
    |[onHttpAuthRequest](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onhttpauthrequest9)|服务器返回407需要端侧提供用户名密码认证，如果不正确处理，可能会导致加载异常、白屏。|
    |[onClientAuthenticationRequest](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onclientauthenticationrequest9)|服务器向端侧请求证书，如果不正确处理，会导致页面加载异常。|
    |[onSslErrorEvent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onsslerrorevent12)|证书错误，需要应用根据证书错误信息进行排查，是证书配错了？还是过期了。|
    

## 复杂的布局与渲染模式导致白屏

若页面使用了复杂布局或渲染模式，需注意其应用场景和约束条件，不当使用可能导致布局混乱或白屏。

Web组件提供了两种渲染模式，能够根据不同的容器大小进行适配，从而满足使用场景中对容器尺寸的需求，详情见[Web组件渲染模式](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-render-mode)。在使用过程中需要注意以下几点：

- 异步渲染模式下（renderMode: [RenderMode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-e#rendermode12).ASYNC_RENDER），Web组件的宽高不能超过7,680px（物理像素），超过会导致白屏。

Web组件提供了自适应页面布局的能力，详情见 [Web组件大小自适应页面内容布局](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-fit-content)，使用时也需要注意以下约束条件：

- 配置同步渲染模式：webSetting({renderingMode: WebRenderingMode.SYNCHRONOUS})。
    
- 关闭滚动效果：webSetting({overScrollMode: OverScrollMode.NEVER})。
    
- 此模式下不支持动态调整组件高度，确保页面高度固定。
    
- 避免在FIT_CONTENT模式下启用键盘避让属性RESIZE_CONTENT，以免导致布局失效。
    
- css样式height：<number> vh和Web组件大小自适应页面布局存在计算冲突，请检查height：<number> vh是否是由body节点而内的第一个高度css样式。如以下结构，id为2的dom节点高度将为0，导致白屏。
    
    1. <body>
    2.   <div id = "1">
    3.     <div id = "2" style = "height: 100vh">子dom</div>
    4.     <div id = "3" style = "height: 20px">子dom</div>
    5.   </div>
    6. </body>
    
    解决此白屏问题的参考方案如下：
    
    - 子dom使用具体高度样式撑开父元素。
        
        1. <body>
        2.   <div id = "1">
        3.     <div id = "2"><div style = "height: 20px"><div/></div>
        4.     <div id = "3" style = "height: 20px">子dom</div>
        5.   </div>
        6. </body>
        
    - 父元素使用实际高度样式。
        
        1. <body>
        2.   <div id = "1">
        3.     <div id = "2" style = "height: 20px">子dom</div>
        4.     <div id = "3" style = "height: 20px">子dom</div>
        5.   </div>
        6. </body>
        

## 处理H5代码兼容性

兼容性问题处理不当也会导致页面白屏。

- 特殊协议拦截。
- 若H5页面调用tel:、mailto:等协议导致白屏，需通过onInterceptRequest拦截并调用系统拨号能力：
    
    1. .onInterceptRequest((event) => {
    2.     if (event.request.url.startsWith('tel:')) {
    3.         // 调用系统拨号能力
    4.         call.makeCall({ phoneNumber: '123456' });
    5.         return { responseCode: 404 }; // 阻止默认行为
    6.     }
    7.     return null;
    8. })
    

## 监控内存与生命周期

内存达到阈值会导致渲染进程被终止，从而引发白屏现象；同样，渲染进程创建失败或非正常销毁也会导致白屏。可从日志中排查原因。检查Web组件是否与WebController正确绑定，或是否因过早释放导致白屏。关注日志中与Render进程相关的信息：是否存在内存泄漏使渲染内存不足。关键字“MEMORY_PRESSURE_LEVEL_CRITICAL”表明内存已达到阈值，此情形下Web可能遭遇黑屏、花屏或闪屏等异常状况，需排查是否存在内存泄漏问题。Render进程是否成功启动或异常退出。

下面列举一些日志中的关键字和对应的情况说明：

|日志关键字|说明|
|:--|:--|
|StartRenderProcess failed|渲染render进程启动失败。|
|MEMORY_PRESSURE_LEVEL_CRITICAL|整机内存压力达到阈值，继续使用可能造成黑屏、闪屏白屏等问题。|
|crashpad SandboxedHandler::HandlerCrash, received signo = xxx|渲染render进程crash，会造成白屏、Web组件卡死等问题。|
|SharedContextState context lost via Skia OOM|共享内存不足，会导致应用闪退、花屏卡死等问题。|
|CreateNativeViewGLSurfaceEGLOhos::normal surface|创建egl surface成功，如果没有该日志打印则会造成白屏问题。|
|INFO: request had no response within 5 seconds|网络超时。|
|final url: ***, error_code xxx(net::ERR_XXX)|主资源加载报错。|

下面说明一下Web组件网络加载过程中的关键日志，正常情况下一个Web组件的加载过程应该包含这些关键节点：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163840.34411538460818644506699979193486:50001231000000:2800:7A81726EA9E745956480DC964583642D5CDAA14F866460629BA2B7A6B15207C4.png)

|日志关键字|说明|
|:--|:--|
|NWebRenderMain start|子进程启动。|
|RendererMain startup 、<br><br>render thread init|子进程初始化开始。|
|event_message: WillProcessNavigationResponse source_id xxx navigation_handle id: xxx|收到主资源的response。|
|event_message: commit navigation in main frame, routing_id: 4, url: ***|Commit到子进程。|
|RenderFrameImpl::CommitNavigation、<br><br>event_message: page load start|子进程收到commit。|
|NWebHandlerDelegate::OnNavigationEntryCommitted、<br><br>event_message: Commit source_id xxx|主进程收到DidCommitNavigation。|
|event_message: load_timing_info errpr_code:0,...|主资源加载完成，以及各阶段耗时。|
|event_message: MarkFirstContentfulPaint|标记解析到有可显示内容的元素。|
|NWebHandlerDelegate::OnPageVisible|第一帧展示。|
|NWebHandlerDelegate::OnFirstContentfulPaint|第一帧有内容展示。|
|event_message: content load finished|页面解析完成。|
|event_message: page load finished、<br><br>NWebHandlerDelegate::OnLoadEnd、<br><br>NWebHandlerDelegate::MainFrame OnLoadEnd、<br><br>NWebHandlerDelegate::OnFirstMeaningfulPaint|页面以及子资源加载完成。|

## 设备的WebView默认加载进程不一致导致加载H5页面白屏

**问题：**

用WebView加载H5在Phone上表现正常，但是在Table/PC/2in1上白屏。

**原因：**

Table/PC/2in1的WebView默认采用多进程加载，iframe默认使用子进程加载。主进程加载完成后，若子进程尚未加载完成，会导致白屏现象。

**解决方案：**

通过setRenderProcessMode()设置WebView渲染模式为单进程加载。

1. webview.WebviewController.setRenderProcessMode(webview.RenderProcessMode.SINGLE);

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-crashpad "使用crashpad收集Web组件崩溃信息")
# 使用Hypium实现ArkWeb自动化测试

更新时间: 2025-12-16 16:38

## 概述

ArkWeb页面支持使用Hypium集成Selenium框架、ChromeDriver驱动进行UI自动化测试。

## 环境配置

1.Hypium环境搭建

参考：[应用UI测试（基于Python）](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/hypium-python-guidelines)。

2.安装Selenium

Selenium主要用于Web应用程序的自动化测试，核心功能是模拟用户在浏览器中的操作，例如点击按钮、输入文本、导航页面等。

1. pip install selenium

3.集成ChromeDriver驱动

ChromeDriver充当了Selenium WebDriver和Web页面之间的中介。通过Selenium发送命令时，ChromeDriver会将这些命令转换为Web内核能够理解的协议，并将响应返回给Selenium。ArkWeb基于谷歌Chromium内核开发，系统版本与Chromium版本的对应关系参考：ArkWeb简介[约束与限制](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-component-overview#%E7%BA%A6%E6%9D%9F%E4%B8%8E%E9%99%90%E5%88%B6)。访问ChromeDriver官方网站[ChromeDriver下载|Chrome for Developers](https://developer.chrome.google.cn/docs/chromedriver/downloads?hl=zh-cn)，获取与Chromium版本对应的ChromeDriver。

首先将ChromeDriver集成到测试工程的resource文件夹下，然后调用WebDriverSetupTool类中的set_chromedriver_exe_path方法指定chromedriver文件的存放路径或者调用set_chromedriver_exe_search_path方法指定chromedriver所在文件夹的路径。

1. self.web_tools = WebDriverSetupTool(self.driver)
2. # 使用set_chromedriver_exe_path指定chromedriver路径，需指定到对应版本的可执行chromedriver文件
3. self.web_tools.set_chromedriver_exe_path(r"D:\WebAutoTest\resource\web_debug_tools\chromedriver_132\chromedriver.exe")

4. self.web_tools = WebDriverSetupTool(self.driver)
5. # 使用set_chromedriver_ext_search_path方法指定chromedriver所在文件夹，Hypium在指定的文件夹寻找对应版本的chromedriver文件
6. self.web_tools.set_chromedriver_exe_search_path(r"D:\WebAutoTest\resource\web_debug_tools")

说明

- 使用set_chromedriver_exe_search_path方法指定chromedriver所在文件夹的路径时，下层文件夹命名规则为chromedriver_版本号，参考下图。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163845.73837036253659735437250295788353:50001231000000:2800:144797A0F4786979D7B0E9E8A53795A8D37FF47946E66A428B61DE74C3B0729E.png)
    

## 示例代码

参考以下代码完成ArkWeb页面的自动化测试，先初始化Selenium的webdriver，后通过webdriver与Web页面交互的API，实现导航页面、查找页面元素操作。

webdriver更多使用方法参考Selenium官方文档：[驱动会话 | Selenium](https://www.selenium.dev/zh-cn/documentation/webdriver/drivers/)。

1. from devicetest.core.test_case import TestCase, Step, CheckPoint
2. from hypium import UiDriver, BY
3. from hypium.webdriver.webdriver_setup_tool import WebDriverSetupTool

4. class ArkWeb_AutoTests(TestCase):
5.     def __init__(self, configs):
6.         self.TAG = self.__class__.__name__
7.         TestCase.__init__(self, self.TAG, configs)
8.         self.driver = UiDriver(self.device1)
9.         self.driver_width, self.driver_height = self.driver.get_display_size()
10.         self.web_tools = WebDriverSetupTool(self.driver)
11.         # 设置chromedriver存放路径
12.         self.web_tools.set_chromedriver_exe_search_path(r"D:\WebAutoTest\resource\web_debug_tools")
13.         # 使用应用包名连接到指定应用的webview页面
14.         self.web_tools.connect("com.huawei.hmos.browser")
15.         # 初始化Selenium的webdriver
16.         self.web_driver = self.web_tools.driver

17.     def setup(self):
18.         pass

19.     def process(self):
20.         # 导航页面：使用Selenium的webdriver访问https://developer.huawei.com/网站
21.         self.web_driver.get("https://developer.huawei.com/")
22.         # 查找页面元素：使用Selenium的webdriver查找页面ID为th的元素
23.         self.web_driver.find_element(BY.ID, "th")

24.     def teardown(self):
25.         # 使用结束需要调用webdriver_setup_tool中的close方法关闭web_tools建立的连接
26.         self.web_tools.close()

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-white-screen "定位与解决Web白屏问题")
# Background Tasks Kit简介

更新时间: 2025-12-16 16:38

## 功能介绍

设备返回主界面、锁屏、应用切换等操作会使应用退至后台。应用退至后台后，如果继续在后台运行，可能会造成设备耗电快、用户界面卡顿等现象。为了降低设备耗电速度、保障用户使用流畅度，系统会对退至后台的应用进行管控，包括[进程](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/process-model-stage)挂起和进程终止。典型场景包括：应用退至后台一段时间应用进程会被挂起、资源不足时系统会终止部分应用进程（即回收该进程的所有资源）。应用进程挂起后，无法使用软件资源（如公共事件、定时器等）和硬件资源（CPU、网络、GPS、蓝牙等）。如何合理使用请参考[合理使用后台硬件资源](https://developer.huawei.com/consumer/cn/doc/best-practices/bpta-use-of-background-hardware-resources)。

为了保障后台音乐播放、日历提醒等功能的正常使用，Background Tasks Kit提供了规范内受约束的后台任务，扩展应用在后台的运行时间。

## 约束与限制

资源使用约束：对于运行的进程，系统会给予一定的资源配额约束，包括进程在连续一段时间内内存的使用、[CPU使用占比](https://developer.huawei.com/consumer/cn/doc/best-practices/bpta-controlling-background-process-cpu)，以及24小时磁盘写的IO量，均有对应的配额上限。超过配额上限时，如果进程处于前台，系统会有对应的warning日志，如果进程处于后台，系统会终止该进程。

## 后台任务类型

Background Tasks Kit提供了规范内受约束的后台任务，包括短时任务、长时任务、延迟任务、代理提醒。

开发者可以根据如下的功能介绍，选择合适的后台任务，以满足应用退至后台后继续运行的需求。

- **短时任务**：适用于实时性要求高、耗时不长的任务，例如状态保存。
    
- **长时任务**：适用于长时间运行在后台、用户可感知的任务，例如后台播放音乐、导航、设备连接等，使用长时任务避免应用进程被挂起。
    
- **延迟任务**：对于实时性要求不高、可延迟执行的任务，系统提供了延迟任务，即满足条件的应用退至后台后被放入执行队列，系统会根据内存、功耗等统一调度。
    
- **代理提醒**：代理提醒是指应用退后台或进程终止后，系统会代理应用做相应的提醒。适用于定时提醒类业务，当前支持的提醒类型包括倒计时、日历和闹钟三类。
    
    **图1** 后台任务类型选择
    

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163817.58441373365616432601099236713500:50001231000000:2800:6A4D32737E08426B19EE06A6943AC8BF10C0F84081AD2513AA63472E1F6CA48C.png)

说明

1. 系统仅支持规范内受约束的后台任务。应用退至后台后，若未使用规范内的后台任务或选择的后台任务类型不正确，对应的应用进程会被挂起或终止。
    
2. 应用申请了规范内的后台任务，仅会提升应用进程被回收的优先级。当系统资源严重不足时，即使应用进程申请了规范内的后台任务，系统仍会终止部分进程，用以保障系统稳定性。
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/background-task-kit "Background Tasks Kit（后台任务开发服务）")
# 短时任务(ArkTS)

更新时间: 2025-12-16 16:38

## 概述

应用退至后台一小段时间后，应用进程会被挂起，无法执行对应的任务。如果应用需在被挂起前，执行一些耗时不长的任务，如状态保存、消息发送等，可以通过本文申请短时任务，扩展应用在后台的运行时间。

## 约束与限制

- **申请时机**：应用需要在前台或[onBackground](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-app-ability-uiability#onbackground)回调内，申请短时任务，否则会申请失败。
    
- **数量限制**：一个应用同一时刻最多申请3个短时任务。以图1为例，在①②③时间段内的任意时刻，应用申请了2个短时任务；在④时间段内的任意时刻，应用申请了1个短时任务。
    
- **配额机制**：一个应用会有一定的短时任务配额（根据系统状态和用户习惯调整），单日（24小时内）配额默认为10分钟，单次配额最大为3分钟，[低电量](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-battery-info)时单次配额默认为1分钟，配额消耗完后不允许再申请短时任务。同时，系统提供获取对应短时任务剩余时间的查询接口[backgroundTaskManager.getRemainingDelayTime](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-resourceschedule-backgroundtaskmanager#backgroundtaskmanagergetremainingdelaytime-1)，用以查询本次短时任务剩余时间，以确认是否继续运行其他业务。
    
- **配额计算**：仅当应用在后台时，对应用下的短时任务计时；同一个应用下的同一个时间段的短时任务，不重复计时。以下图为例：应用有两个短时任务A和B，在前台时申请短时任务A，应用退至后台后开始计时为①，应用进入前台②后不计时，再次进入后台③后开始计时，短时任务A结束后，由于阶段④仍然有短时任务B，所以该阶段继续计时。因此，在这个过程中，该应用短时任务总耗时为①+③+④。
    
    **图1** 短时任务配额计算原理图
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163819.83355052541494679875123079445770:50001231000000:2800:B2D346E936138009C724E2D14920E1D6E23C29B0F0EAAEC453D8FD13ACCFD91A.png)
    
    说明
    
    任务完成后，应用需主动取消短时任务，否则会影响应用当日短时任务的剩余配额。
    
- **超时**：短时任务即将超时时，系统会回调应用，应用需要取消短时任务。如果超时不取消，系统会对应用进行管控，包括进程挂起和进程终止。
    

## 接口说明

**表1** 主要接口

以下是短时任务开发使用的主要接口，更多接口及使用方式请见[后台任务管理](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-resourceschedule-backgroundtaskmanager)。

|接口名|描述|
|:--|:--|
|[requestSuspendDelay(reason: string, callback: Callback<void>): DelaySuspendInfo](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-resourceschedule-backgroundtaskmanager#backgroundtaskmanagerrequestsuspenddelay)|申请短时任务。|
|[getRemainingDelayTime(requestId: number): Promise<number>](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-resourceschedule-backgroundtaskmanager#backgroundtaskmanagergetremainingdelaytime-1)|获取对应短时任务的剩余时间。|
|[cancelSuspendDelay(requestId: number): void](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-resourceschedule-backgroundtaskmanager#backgroundtaskmanagercancelsuspenddelay)|取消短时任务。|

## 开发步骤

1. 导入模块。
    
    1. import { backgroundTaskManager } from '@kit.BackgroundTasksKit';
    2. import { BusinessError } from '@kit.BasicServicesKit';
    
2. 申请短时任务并实现回调。此处回调在短时任务即将结束时触发，与应用的业务功能不耦合，短时任务申请成功后，正常执行应用本身的任务。
    
    1. let id: number;         // 申请短时任务ID
    2. let delayTime: number;  // 本次申请短时任务的剩余时间
    
    3. // 申请短时任务
    4. function requestSuspendDelay() {
    5.   let myReason = 'test requestSuspendDelay';   // 申请原因
    6.   try {
    7.     let delayInfo = backgroundTaskManager.requestSuspendDelay(myReason, () => {
    8.     // 回调函数。应用申请的短时任务即将超时，通过此函数回调应用，执行一些清理和标注工作，并取消短时任务
    9.       console.info('suspend delay task will timeout');
    10.       try {
    11.         backgroundTaskManager.cancelSuspendDelay(id);
    12.       } catch (error) {
    13.         console.error(`Operation cancelSuspendDelay failed. code is ${(error as BusinessError).code} message is ${(error as BusinessError).message}`);
    14.       }
    15.     })
    16.     id = delayInfo.requestId;
    17.     delayTime = delayInfo.actualDelayTime;
    18.   } catch (error) {
    19.     console.error(`Operation requestSuspendDelay failed. code is ${(error as BusinessError).code} message is ${(error as BusinessError).message}`);
    20.   }
    21. }
    
    22. // 执行应用本身业务
    
3. 获取短时任务剩余时间。查询本次短时任务的剩余时间，用以判断是否继续运行其他业务，例如应用有两个小任务，在执行完第一个小任务后，可以判断本次短时任务是否还有剩余时间来决定是否执行第二个小任务。
    
    1. let id: number; // 申请短时任务ID
    
    2. async function getRemainingDelayTime() {
    3.   backgroundTaskManager.getRemainingDelayTime(id).then((res: number) => {
    4.     console.info('Succeeded in getting remaining delay time.');
    5.   }).catch((err: BusinessError) => {
    6.     console.error(`Failed to get remaining delay time. Code: ${err.code}, message: ${err.message}`);
    7.   })
    8. }
    
4. 取消短时任务。
    
    1. let id: number; // 申请短时任务ID
    
    2. function cancelSuspendDelay() {
    3.   try {
    4.     backgroundTaskManager.cancelSuspendDelay(id);
    5.   } catch (error) {
    6.     console.error(`Operation cancelSuspendDelay failed. code is ${(error as BusinessError).code} message is ${(error as BusinessError).message}`);
    7.   }
    8. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/background-task-overview "Background Tasks Kit简介")
# 短时任务(C/C++)

更新时间: 2025-12-16 16:38

## 场景介绍

应用退至后台一小段时间后，应用进程会被挂起，无法执行对应的任务。如果应用在后台仍需要执行耗时不长的任务，如状态保存等，可以通过本文申请短时任务，扩展应用在后台的运行时间。

## 接口说明

常用接口如下表所示，具体API说明详见[API参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-transient-task-api-h#%E5%87%BD%E6%95%B0)。

|接口名|描述|
|:--|:--|
|[int32_t OH_BackgroundTaskManager_RequestSuspendDelay(const char *reason, TransientTask_Callback callback, TransientTask_DelaySuspendInfo *info)](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-transient-task-api-h#oh_backgroundtaskmanager_requestsuspenddelay)|申请短时任务。|
|[int32_t OH_BackgroundTaskManager_GetRemainingDelayTime(int32_t requestId, int32_t *delayTime)](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-transient-task-api-h#oh_backgroundtaskmanager_getremainingdelaytime)|获取对应短时任务的剩余时间。|
|[int32_t OH_BackgroundTaskManager_CancelSuspendDelay(int32_t requestId)](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-transient-task-api-h#oh_backgroundtaskmanager_cancelsuspenddelay)|取消短时任务。|
|[int32_t OH_BackgroundTaskManager_GetTransientTaskInfo(TransientTask_TransientTaskInfo *transientTaskInfo)](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-transient-task-api-h#oh_backgroundtaskmanager_gettransienttaskinfo)|获取所有短时任务信息，如当日剩余总配额等。|

## 开发步骤

### 在napi_init.cpp文件中封装接口并注册模块

1. 封装函数
    
    1. #include "napi/native_api.h"
    2. #include "transient_task/transient_task_api.h"
    
    3. TransientTask_DelaySuspendInfo delaySuspendInfo;
    
    4. static void callback(void)
    5. {
    6.    // 短时任务即将结束，业务在这里取消短时任务
    7.    OH_BackgroundTaskManager_CancelSuspendDelay(delaySuspendInfo.requestId);
    8. }
    
    9. // 申请短时任务
    10. static napi_value RequestSuspendDelay(napi_env env, napi_callback_info info)
    11. {
    12.       napi_value result;
    13.       int32_t res = OH_BackgroundTaskManager_RequestSuspendDelay("test", callback, &delaySuspendInfo);
    14.       if (res == 0) {
    15.          napi_create_int32(env, delaySuspendInfo.requestId, &result);
    16.       } else {
    17.          napi_create_int32(env, -1, &result);
    18.       }
    19.       return result;
    20. }
    
    21. // 获取剩余时间
    22. static napi_value GetRemainingDelayTime(napi_env env, napi_callback_info info)
    23. {
    24.       napi_value result;
    25.       int32_t delayTime = 0;
    26.       int32_t res = OH_BackgroundTaskManager_GetRemainingDelayTime(delaySuspendInfo.requestId, &delayTime);
    27.       if (res == 0) {
    28.          napi_create_int32(env, delayTime, &result);
    29.       } else {
    30.          napi_create_int32(env, -1, &result);
    31.       }
    32.       return result;
    33. }
    
    34. // 取消短时任务
    35. static napi_value CancelSuspendDelay(napi_env env, napi_callback_info info)
    36. {
    37.       napi_value result;
    38.       int32_t res = OH_BackgroundTaskManager_CancelSuspendDelay(delaySuspendInfo.requestId);
    39.       napi_create_int32(env, res, &result);
    40.       return result;
    41. }
    
    42. // 获取所有短时任务信息
    43. TransientTask_TransientTaskInfo transientTaskInfo;
    
    44. static napi_value GetTransientTaskInfo(napi_env env, napi_callback_info info)
    45. {
    46.    napi_value result;
    47.    napi_create_object(env, &result);
    48.    int32_t res = OH_BackgroundTaskManager_GetTransientTaskInfo(&transientTaskInfo);
    49.    napi_value napiRemainingQuota = nullptr;
    50.    // 获取成功，格式化数据并返回给接口
    51.    if (res == 0) {
    52.       napi_create_int32(env, transientTaskInfo.remainingQuota, &napiRemainingQuota);
    53.       napi_set_named_property(env, result, "remainingQuota", napiRemainingQuota); // 格式化当日总配额
    
    54.       napi_value info {nullptr};
    55.       napi_create_array(env, &info);
    56.       uint32_t count = 0;
    57.       // 格式化所有已申请的短时任务信息
    58.       for (int index = 0; index < 3; index++) {
    59.          if (transientTaskInfo.transientTasks[index].requestId == 0) {
    60.              continue;
    61.          }
    
    62.          napi_value napiWork = nullptr;
    63.          napi_create_object(env, &napiWork);
    
    64.          napi_value napiRequestId = nullptr;
    65.          napi_create_int32(env, transientTaskInfo.transientTasks[index].requestId, &napiRequestId);
    66.          napi_set_named_property(env, napiWork, "requestId", napiRequestId);
    
    67.          napi_value napiActualDelayTime = nullptr;
    68.          napi_create_int32(env, transientTaskInfo.transientTasks[index].actualDelayTime, &napiActualDelayTime);
    69.          napi_set_named_property(env, napiWork, "actualDelayTime", napiActualDelayTime);
    
    70.          napi_set_element(env, info, count, napiWork);
    71.          count++;
    72.       }
    73.       napi_set_named_property(env, result, "transientTasks", info);
    74.    } else {
    75.       napi_create_int32(env, 0, &napiRemainingQuota);
    76.       napi_set_named_property(env, result, "remainingQuota", napiRemainingQuota);
    77.       napi_value info {nullptr};
    78.       napi_create_array(env, &info);
    79.       napi_set_named_property(env, result, "transientTasks", info);
    80.    }
    81.    return result;
    82. }
    
2. 注册函数
    
    1. EXTERN_C_START
    2. static napi_value Init(napi_env env, napi_value exports)
    3. {
    4.     napi_property_descriptor desc[] = {
    5.         {"RequestSuspendDelay", nullptr, RequestSuspendDelay, nullptr, nullptr, nullptr, napi_default, nullptr},
    6.         {"GetRemainingDelayTime", nullptr, GetRemainingDelayTime, nullptr, nullptr, nullptr, napi_default, nullptr},
    7.         {"CancelSuspendDelay", nullptr, CancelSuspendDelay, nullptr, nullptr, nullptr, napi_default, nullptr},
    8.         {"GetTransientTaskInfo", nullptr, GetTransientTaskInfo, nullptr, nullptr, nullptr, napi_default, nullptr },
    9.     };
    10.     napi_define_properties(env, exports, sizeof(desc) / sizeof(desc[0]), desc);
    11.     return exports;
    12. }
    13. EXTERN_C_END
    
3. 注册模块
    
    1. static napi_module demoModule = {
    2.     .nm_version = 1,
    3.     .nm_flags = 0,
    4.     .nm_filename = nullptr,
    5.     .nm_register_func = Init,
    6.     .nm_modname = "entry",
    7.     .nm_priv = ((void*)0),
    8.     .reserved = { 0 },
    9. };
    
    10. extern "C" __attribute__((constructor)) void RegisterEntryModule(void)
    11. {
    12.     napi_module_register(&demoModule);
    13. }
    

### 在index.d.ts文件中声明函数

1. import backgroundTaskManager from '@kit.BackgroundTasksKit';

2. export const RequestSuspendDelay: () => number;
3. export const GetRemainingDelayTime: () => number;
4. export const CancelSuspendDelay: () => number;
5. export const GetTransientTaskInfo: () => backgroundTaskManager.TransientTaskInfo;

### 在index.ets文件中调用函数

1. import testTransientTask from 'libentry.so';

2. @Entry
3. @Component
4. struct Index {
5.   @State message: string = '';

6.   build() {
7.     Row() {
8.       Column() {
9.         Text(this.message)
10.           .fontSize(50)
11.           .fontWeight(FontWeight.Bold)
12.         Button('申请短时任务').onClick(event => {
13.           this.RequestSuspendDelay();
14.         })
15.         Button('获取剩余时间').onClick(event =>{
16.           this.GetRemainingDelayTime();
17.         })
18.         Button('取消短时任务').onClick(event =>{
19.           this.CancelSuspendDelay();
20.         })
21.         Button('获取所有短时任务信息').onClick(event =>{
22.           this.GetTransientTaskInfo();
23.         })
24.       }
25.       .width('100%')
26.      }
27.     .height('100%')
28.   }

29.   RequestSuspendDelay() {
30.     let requestId = testTransientTask.RequestSuspendDelay();
31.     console.info("The return requestId is " + requestId);
32.   }

33.   GetRemainingDelayTime() {
34.     let time = testTransientTask.GetRemainingDelayTime();
35.     console.info("The time is " + time);
36.   }

37.   CancelSuspendDelay() {
38.     let ret = testTransientTask.CancelSuspendDelay();
39.     console.info("The ret is " + ret);
40.   }

41.   GetTransientTaskInfo() {
42.     let ret = testTransientTask.GetTransientTaskInfo();
43.     console.info("The ret is " + JSON.stringify(ret));
44.   }
45. }

### 配置库依赖

配置CMakeLists.txt，本模块需要用到的共享库是libtransient_task.so，在工程自动生成的CMakeLists.txt中的target_link_libraries中添加此共享库。

1. target_link_libraries(entry PUBLIC libace_napi.z.so libtransient_task.so)

## 测试步骤

1. 连接设备并运行程序。
    
2. 点击 申请短时任务 按钮，控制台会打印日志，示例如下：
    
    1. The return requestId is 1
    
3. 点击 获取剩余时间 按钮，控制台会打印日志，示例如下：
    
    1. The return requestId is 18000
    
4. 点击 取消短时任务 按钮，控制台会打印日志，示例如下：
    
    1. The ret is 0
    
5. 点击 获取所有短时任务信息 按钮，控制台会打印日志，示例如下：
    
    1. The ret is {"remainingQuota":600000,"transientTasks":[]}
    

说明

申请短时任务的按钮，不可连续点击超过3次，否则会超出短时任务数量限制并报错。使用过程中更多的约束与限制请参考[短时任务(ArkTS)](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/transient-task#%E7%BA%A6%E6%9D%9F%E4%B8%8E%E9%99%90%E5%88%B6)。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/transient-task "短时任务(ArkTS)")
# 长时任务(ArkTS)

更新时间: 2025-12-16 16:38

## 概述

### 功能介绍

应用退至后台后，在后台需要长时间运行用户可感知的任务，如播放音乐、导航等。为防止应用进程被挂起，导致对应功能异常，可以申请长时任务，使应用在后台长时间运行。在长时任务中，支持同时申请多种类型的任务，也可以对任务类型进行更新。应用退至后台执行业务时，系统会做一致性校验，确保应用在执行相应的长时任务。应用在申请长时任务成功后，通知栏会显示与长时任务相关联的消息，用户删除通知栏消息时，系统会自动停止长时任务。

### 使用场景

下表给出了当前长时任务支持的类型，包含数据传输、音视频播放、录制、定位导航、蓝牙相关业务、多设备互联、音视频通话和计算任务。可以参考下表中的场景举例，选择合适的长时任务类型。

**表1** 长时任务类型

|参数名|描述|配置项|场景举例|
|:--|:--|:--|:--|
|DATA_TRANSFER|数据传输。|dataTransfer|非托管形式的上传、下载，如在浏览器后台上传或下载数据。|
|AUDIO_PLAYBACK|音视频播放。|audioPlayback|音频、视频在后台播放，音视频投播。<br><br>**说明：** 支持在元服务中使用。|
|AUDIO_RECORDING|录制。|audioRecording|录音、录屏退后台。|
|LOCATION|定位导航。|location|定位、导航。|
|BLUETOOTH_INTERACTION|蓝牙相关业务。|bluetoothInteraction|通过蓝牙传输文件时退后台。|
|MULTI_DEVICE_CONNECTION|多设备互联。|multiDeviceConnection|分布式业务连接、投播。<br><br>**说明：** 支持在元服务中使用。|
|VOIP13+|音视频通话。|voip|某些聊天类应用（具有音视频业务）音频、视频通话时退后台。|
|TASK_KEEPING|计算任务（仅对PC/2in1设备开放）。<br><br>**说明：** 从API version 21开始，对PC/2in1设备、非PC/2in1设备但申请了ACL权限为[ohos.permission.KEEP_BACKGROUND_RUNNING_SYSTEM](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/restricted-permissions#ohospermissionkeep_background_running_system)的应用开放。 API version 20及之前版本，仅对PC/2in1设备开放。|taskKeeping|如杀毒软件。|

关于DATA_TRANSFER（数据传输）说明：

- 在数据传输时，若应用使用[上传下载代理接口](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-request)托管给系统，即使申请DATA_TRANSFER的后台任务，应用退后台时还是会被挂起。
    
- 在数据传输时，应用需要更新进度，如果进度长时间（首次更新超过10分钟）未更新，数据传输的长时任务会被取消。更新进度的通知类型必须为实况窗，具体实现可参考[startBackgroundRunning()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-resourceschedule-backgroundtaskmanager#backgroundtaskmanagerstartbackgroundrunning12)中的示例。
    

关于AUDIO_PLAYBACK（音视频播放）说明：

- 音视频投播，是指将一台设备的音视频投至另一台设备播放。投播退至后台，长时任务会检测音视频播放和投屏两个业务，只要有其一正常运行，长时任务就不会终止。
    
- 当应用需要在后台播放媒体类型（流类型为STREAM_USAGE_MUSIC、STREAM_USAGE_MOVIE和STREAM_USAGE_AUDIOBOOK）和游戏类型（流类型为STREAM_USAGE_GAME）时，必须接入媒体会话服务（[AVSession](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/avsession-overview)）并申请AUDIO_PLAYBACK类型长时任务。
    
- 除了上述播放类型，针对用户可感知的其他播放任务，如果应用需要在后台长时间运行该任务，必须申请AUDIO_PLAYBACK类型长时任务，无需接入AVSession。
    
- 如果应用不满足上述接入规范，退至后台播放时会被系统静音并冻结，无法在后台正常播放，直到应用重新切回前台时，才会解除静音并恢复播放。
    
- 从API version 20开始，申请AUDIO_PLAYBACK类型长时任务但不接入AVSession，申请长时任务成功后会在通知栏显示通知；接入AVSession后，后台任务模块不会发送通知栏通知，由AVSession发送通知。对于API version 19及之前的版本，后台任务模块不会在通知栏显示通知。
    

### 约束与限制

**申请限制**：Stage模型中，长时任务仅支持UIAbility申请；FA模型中，长时任务仅支持ServiceAbility申请。长时任务支持设备当前应用申请，也支持跨设备或跨应用申请，跨设备或跨应用仅对系统应用开放。

**数量限制**：

- 从API version 21开始，支持一个UIAbility同一时刻申请多个长时任务，最多可申请10个，具体实现可参考[startBackgroundRunning()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-resourceschedule-backgroundtaskmanager#backgroundtaskmanagerstartbackgroundrunning21)。对于API version 20及之前版本，一个UIAbility（FA模型则为ServiceAbility）同一时刻仅支持申请一个长时任务，即在一个长时任务结束后才能继续申请。如果一个应用同时需要申请多个长时任务，需要创建多个UIAbility。
- 如果一个应用创建了多个UIAbility，一个UIAbility申请长时任务后，整个应用下的所有进程均不会被挂起。

**运行限制**：

- 申请长时任务后，应用未执行相应的业务，系统会对应用进行管控，即应用退至后台会被挂起。如系统检测到应用申请了AUDIO_PLAYBACK（音视频播放），但实际未播放音乐。
    
- 申请长时任务后，应用执行的业务类型与申请的不一致，系统会对应用进行管控，即应用退至后台会被挂起。如系统检测到应用只申请了AUDIO_PLAYBACK（音视频播放），但实际上除了播放音乐（对应AUDIO_PLAYBACK类型），还在进行录制（对应AUDIO_RECORDING类型）。
    
- 申请长时任务后，应用的业务已执行完，系统会对应用进行管控，即应用退至后台会被挂起。
    
- 若运行长时任务的进程后台负载持续高于所申请类型的典型负载，系统会对应用进行管控，即应用退至后台会被挂起或终止。
    

说明

应用按需求申请长时任务，当应用无需在后台运行（任务结束）时，要及时主动取消长时任务，否则应用退至后台会被系统挂起。例如用户主动点击音乐暂停播放时，应用需及时取消对应的长时任务；用户再次点击音乐播放时，需重新申请长时任务。

若音频在后台播放时被[打断](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/audio-playback-concurrency)，系统会自行检测和停止长时任务，音频重启播放时，需要再次申请长时任务。

后台播放音频的应用，在停止长时任务的同时，需要暂停或停止音频流，否则应用会被系统强制终止。

## 接口说明

**表2** 主要接口

以下是长时任务开发使用的相关接口，下表均以Promise形式为例，更多接口及使用方式请见[后台任务管理](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-resourceschedule-backgroundtaskmanager)。

|接口名|描述|
|:--|:--|
|[startBackgroundRunning(context: Context, bgMode: BackgroundMode, wantAgent: WantAgent): Promise<void>](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-resourceschedule-backgroundtaskmanager#backgroundtaskmanagerstartbackgroundrunning-1)|申请长时任务，本接口一个UIAbility同一时刻仅支持申请一个长时任务，即在一个长时任务结束后才能继续申请。|
|[stopBackgroundRunning(context: Context): Promise<void>](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-resourceschedule-backgroundtaskmanager#backgroundtaskmanagerstopbackgroundrunning-1)|取消长时任务。|
|[startBackgroundRunning(context: Context, request: ContinuousTaskRequest): Promise<ContinuousTaskNotification>](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-resourceschedule-backgroundtaskmanager#backgroundtaskmanagerstartbackgroundrunning21)|申请多个长时任务。本接口支持一个UIAbility同一时刻申请多个长时任务，最多可申请10个。|
|[stopBackgroundRunning(context: Context, continuousTaskId: number): Promise<void>](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-resourceschedule-backgroundtaskmanager#backgroundtaskmanagerstopbackgroundrunning21)|取消指定Id的长时任务。|

## 开发步骤

本文以申请一个录制长时任务为例，实现如下功能：

- 点击“申请长时任务”按钮，应用申请录制长时任务成功，通知栏显示“正在运行录制任务”通知。
    
- 点击“取消长时任务”按钮，取消长时任务，通知栏撤销相关通知。
    

### Stage模型

1. 需要申请ohos.permission.KEEP_BACKGROUND_RUNNING权限，配置方式请参见[声明权限](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/declare-permissions)。
    
2. 声明后台模式类型。
    
    在[module.json5配置文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file)中abilities下的backgroundModes字段里，为需要使用长时任务的UIAbility声明相应的长时任务类型，配置文件中填写长时任务类型的[配置项](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/continuous-task#%E4%BD%BF%E7%94%A8%E5%9C%BA%E6%99%AF)。
    
    1.  "module": {
    2.      "abilities": [
    3.          {
    4.              "backgroundModes": [
    5.               // 长时任务类型的配置项
    6.              "audioRecording",
    7.              "bluetoothInteraction",
    8.              "audioPlayback"
    9.              ]
    10.          }
    11.      ],
    12.      // ...
    13.  }
    
3. 导入模块。
    
    长时任务相关的模块为@ohos.resourceschedule.backgroundTaskManager和@ohos.app.ability.wantAgent，其余模块按实际需要导入。
    
    1.  import { backgroundTaskManager } from '@kit.BackgroundTasksKit';
    2.  import { BusinessError } from '@kit.BasicServicesKit';
    3.  import { wantAgent, WantAgent } from '@kit.AbilityKit';
    4.  // 在元服务中，请删除WantAgent导入
    
4. 申请和取消长时任务。
    
    **设备当前应用**申请和取消长时任务示例代码如下：
    
    1.  function callback(info: backgroundTaskManager.ContinuousTaskCancelInfo) {
    2.    // 长时任务id
    3.    console.info('OnContinuousTaskCancel callback id ' + info.id);
    4.    // 长时任务取消原因
    5.    console.info('OnContinuousTaskCancel callback reason ' + info.reason);
    6.  }
    
    7.  @Entry
    8.  @Component
    9.  struct Index {
    10.    @State message: string = 'ContinuousTask';
    11.   // 通过getUIContext().getHostContext()方法，来获取page所在的UIAbility上下文
    12.    private context: Context | undefined = this.getUIContext().getHostContext();
    
    13.    OnContinuousTaskCancel() {
    14.      try {
    15.         backgroundTaskManager.on("continuousTaskCancel", callback);
    16.         console.info(`Succeeded in operationing OnContinuousTaskCancel.`);
    17.      } catch (error) {
    18.         console.error(`Operation OnContinuousTaskCancel failed. code is ${(error as BusinessError).code} message is ${(error as BusinessError).message}`);
    19.      }
    20.    }
    
    21.    OffContinuousTaskCancel() {
    22.      try {
    23.         // callback参数不传，则取消所有已注册的回调
    24.         backgroundTaskManager.off("continuousTaskCancel", callback);
    25.         console.info(`Succeeded in operationing OffContinuousTaskCancel.`);
    26.      } catch (error) {
    27.         console.error(`Operation OffContinuousTaskCancel failed. code is ${(error as BusinessError).code} message is ${(error as BusinessError).message}`);
    28.      }
    29.    }
    
    30.    // 申请长时任务.then()写法
    31.    startContinuousTask() {
    32.      let wantAgentInfo: wantAgent.WantAgentInfo = {
    33.        // 点击通知后，将要执行的动作列表
    34.        // 添加需要被拉起应用的bundleName和abilityName
    35.        wants: [
    36.          {
    37.            bundleName: "com.example.myapplication",
    38.            abilityName: "MainAbility"
    39.          }
    40.        ],
    41.        // 指定点击通知栏消息后的动作是拉起ability
    42.        actionType: wantAgent.OperationType.START_ABILITY,
    43.        // 使用者自定义的一个私有值
    44.        requestCode: 0,
    45.        // 点击通知后，动作执行属性
    46.        actionFlags: [wantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG],
    47.        // 车钥匙长时任务子类型，从API version 16开始支持。只有申请bluetoothInteraction类型的长时任务，车钥匙子类型才能生效。
    48.        // 确保extraInfo参数中的Key值为backgroundTaskManager.BackgroundModeType.SUB_MODE，否则子类型不生效。
    49.        // extraInfo: { [backgroundTaskManager.BackgroundModeType.SUB_MODE] : backgroundTaskManager.BackgroundSubMode.CAR_KEY }
    50.      };
    
    51.      try {
    52.        // 通过wantAgent模块下getWantAgent方法获取WantAgent对象
    53.        // 在元服务中，使用wantAgent.getWantAgent(wantAgentInfo).then((wantAgentObj: object) => {替换下面一行代码
    54.        wantAgent.getWantAgent(wantAgentInfo).then((wantAgentObj: WantAgent) => {
    55.          try {
    56.            let list: Array<string> = ["audioRecording"];
    57.            // let list: Array<string> = ["bluetoothInteraction"]; 长时任务类型包含bluetoothInteraction，CAR_KEY子类型合法
    58.            // 在元服务中，let list: Array<string> = ["audioPlayback"];
    59.            backgroundTaskManager.startBackgroundRunning(this.context, list, wantAgentObj).then((res: backgroundTaskManager.ContinuousTaskNotification) => {
    60.              console.info("Operation startBackgroundRunning succeeded");
    61.              // 此处执行具体的长时任务逻辑，如录音，录制等。
    62.              // 系统会对业务场景的真实性进行检测，如果没有实际执行对应的业务，系统可能会取消对应的长时任务并挂起应用。
    63.            }).catch((error: BusinessError) => {
    64.              console.error(`Failed to Operation startBackgroundRunning. code is ${error.code} message is ${error.message}`);
    65.            });
    66.          } catch (error) {
    67.            console.error(`Failed to Operation startBackgroundRunning. code is ${(error as BusinessError).code} message is ${(error as BusinessError).message}`);
    68.          }
    69.        });
    70.      } catch (error) {
    71.        console.error(`Failed to Operation getWantAgent. code is ${(error as BusinessError).code} message is ${(error as BusinessError).message}`);
    72.      }
    73.    }
    
    74.    // 取消长时任务.then()写法
    75.    stopContinuousTask() {
    76.       backgroundTaskManager.stopBackgroundRunning(this.context).then(() => {
    77.         console.info(`Succeeded in operationing stopBackgroundRunning.`);
    78.       }).catch((err: BusinessError) => {
    79.         console.error(`Failed to operation stopBackgroundRunning. Code is ${err.code}, message is ${err.message}`);
    80.       });
    81.    }
    
    82.    build() {
    83.      Row() {
    84.        Column() {
    85.          Text("Index")
    86.            .fontSize(50)
    87.            .fontWeight(FontWeight.Bold)
    
    88.         Button() {
    89.            Text('申请长时任务').fontSize(25).fontWeight(FontWeight.Bold)
    90.          }
    91.          .type(ButtonType.Capsule)
    92.          .margin({ top: 10 })
    93.          .backgroundColor('#0D9FFB')
    94.          .width(250)
    95.          .height(40)
    96.          .onClick(() => {
    97.            // 通过按钮申请长时任务
    98.            this.startContinuousTask();
    99.          })
    
    100.          Button() {
    101.            Text('取消长时任务').fontSize(25).fontWeight(FontWeight.Bold)
    102.          }
    103.          .type(ButtonType.Capsule)
    104.          .margin({ top: 10 })
    105.          .backgroundColor('#0D9FFB')
    106.          .width(250)
    107.          .height(40)
    108.          .onClick(() => {
    109.            // 此处结束具体的长时任务的执行
    
    110.            // 通过按钮取消长时任务
    111.            this.stopContinuousTask();
    112.          })
    
    113.          Button() {
    114.            Text('注册长时任务取消回调').fontSize(25).fontWeight(FontWeight.Bold)
    115.          }
    116.          .type(ButtonType.Capsule)
    117.          .margin({ top: 10 })
    118.          .backgroundColor('#0D9FFB')
    119.          .width(250)
    120.          .height(40)
    121.          .onClick(() => {
    122.            // 通过按钮注册长时任务取消回调
    123.            this.OnContinuousTaskCancel();
    124.          })
    
    125.          Button() {
    126.            Text('取消注册长时任务取消回调').fontSize(25).fontWeight(FontWeight.Bold)
    127.          }
    128.          .type(ButtonType.Capsule)
    129.          .margin({ top: 10 })
    130.          .backgroundColor('#0D9FFB')
    131.          .width(250)
    132.          .height(40)
    133.          .onClick(() => {
    134.            // 通过按钮取消注册长时任务取消回调
    135.            this.OffContinuousTaskCancel();
    136.          })
    137.        }
    138.        .width('100%')
    139.      }
    140.      .height('100%')
    141.    }
    142.  }
    
5. 申请和取消长时任务async/await写法。
    
    **设备当前应用**申请和取消长时任务async/await写法示例代码如下：
    
    1.  @Entry
    2.  @Component
    3.  struct Index {
    4.    @State message: string = 'ContinuousTask';
    5.   // 通过getUIContext().getHostContext()方法，来获取page所在的UIAbility上下文
    6.    private context: Context | undefined = this.getUIContext().getHostContext();
    
    7.    // 申请长时任务async/await写法
    8.    async startContinuousTask() {
    9.      let wantAgentInfo: wantAgent.WantAgentInfo = {
    10.        // 点击通知后，将要执行的动作列表
    11.        // 添加需要被拉起应用的bundleName和abilityName
    12.        wants: [
    13.          {
    14.            bundleName: "com.example.myapplication",
    15.            abilityName: "MainAbility"
    16.          }
    17.        ],
    18.        // 指定点击通知栏消息后的动作是拉起ability
    19.        actionType: wantAgent.OperationType.START_ABILITY,
    20.        // 使用者自定义的一个私有值
    21.        requestCode: 0,
    22.        // 点击通知后，动作执行属性
    23.        actionFlags: [wantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG],
    24.        // 车钥匙长时任务子类型，从API version 16开始支持。只有申请bluetoothInteraction类型的长时任务，车钥匙子类型才能生效。
    25.        // 确保extraInfo参数中的Key值为backgroundTaskManager.BackgroundModeType.SUB_MODE，否则子类型不生效。
    26.        // extraInfo: { [backgroundTaskManager.BackgroundModeType.SUB_MODE] : backgroundTaskManager.BackgroundSubMode.CAR_KEY }
    27.      };
    
    28.      try {
    29.        // 通过wantAgent模块下getWantAgent方法获取WantAgent对象
    30.        // 在元服务中，使用const wantAgentObj: object = await wantAgent.getWantAgent(wantAgentInfo);替换下面一行代码
    31.        const wantAgentObj: WantAgent = await wantAgent.getWantAgent(wantAgentInfo);
    32.        try {
    33.          let list: Array<string> = ["audioRecording"];
    34.          // let list: Array<string> = ["bluetoothInteraction"]; 长时任务类型包含bluetoothInteraction，CAR_KEY子类型合法
    35.          // 在元服务中，let list: Array<string> = ["audioPlayback"];
    36.          const res: backgroundTaskManager.ContinuousTaskNotification = await backgroundTaskManager.startBackgroundRunning(this.context as Context, list, wantAgentObj);
    37.          console.info(`Operation startBackgroundRunning succeeded, notificationId: ${res.notificationId}`);
    38.          // 此处执行具体的长时任务逻辑，如录音，录制等。
    39.        } catch (error) {
    40.          console.error(`Failed to Operation startBackgroundRunning. Code is ${(error as BusinessError).code}, message is ${(error as BusinessError).message}`);
    41.        }
    42.      } catch (error) {
    43.        console.error(`Failed to Operation getWantAgent. Code is ${(error as BusinessError).code}, message is ${(error as BusinessError).message}`);
    44.      }
    45.    }
    
    46.    // 取消长时任务async/await写法
    47.    async stopContinuousTask() {
    48.      try {
    49.        await backgroundTaskManager.stopBackgroundRunning(this.context);
    50.        console.info(`Succeeded in operationing stopBackgroundRunning.`);
    51.      } catch (error) {
    52.        console.error(`Failed to operation stopBackgroundRunning. Code is ${(error as BusinessError).code}, message is ${(error as BusinessError).message}`)
    53.      }
    54.    }
    
    55.    build() {
    56.      Row() {
    57.        Column() {
    58.          Text("Index")
    59.            .fontSize(50)
    60.            .fontWeight(FontWeight.Bold)
    
    61.         Button() {
    62.            Text('申请长时任务').fontSize(25).fontWeight(FontWeight.Bold)
    63.          }
    64.          .type(ButtonType.Capsule)
    65.          .margin({ top: 10 })
    66.          .backgroundColor('#0D9FFB')
    67.          .width(250)
    68.          .height(40)
    69.          .onClick(() => {
    70.            // 通过按钮申请长时任务
    71.            this.startContinuousTask();
    72.          })
    
    73.          Button() {
    74.            Text('取消长时任务').fontSize(25).fontWeight(FontWeight.Bold)
    75.          }
    76.          .type(ButtonType.Capsule)
    77.          .margin({ top: 10 })
    78.          .backgroundColor('#0D9FFB')
    79.          .width(250)
    80.          .height(40)
    81.          .onClick(() => {
    82.            // 此处结束具体的长时任务的执行
    
    83.            // 通过按钮取消长时任务
    84.            this.stopContinuousTask();
    85.          })
    86.        }
    87.        .width('100%')
    88.      }
    89.      .height('100%')
    90.    }
    91.  }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/native-transient-task "短时任务(C/C++)")
# 延迟任务(ArkTS)

更新时间: 2025-12-16 16:38

## 概述

### 功能介绍

应用退至后台后，需要执行实时性要求不高的任务，例如有网络时不定期主动获取邮件等，可以使用延迟任务。当应用满足设定的触发条件（包括网络类型、充电类型、存储状态、电池状态、定时状态等）时，将任务添加到执行队列，系统会根据内存、功耗、设备温度、用户使用习惯等统一调度拉起应用，执行相应的延迟任务。

### 运行原理

**图1** 延迟任务实现原理

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163821.92941784775567584157264454689669:50001231000000:2800:B5A143C88CDC37C260D0093FE655994F307D71DDC30F63BBD1E991E4D4654915.png)

应用调用延迟任务接口添加、删除、查询延迟任务，延迟任务管理模块会根据任务设置的条件（通过[WorkInfo](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-resourceschedule-workscheduler#workinfo)参数设置，包括网络类型、充电类型、存储状态等）和系统状态（包括内存、功耗、设备温度、用户使用习惯等）统一决策调度时机。

当满足调度条件或调度结束时，系统会回调应用[WorkSchedulerExtensionAbility](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-workschedulerextensionability)中 onWorkStart() 或 onWorkStop() 的方法，同时会为应用单独创建一个Extension扩展进程用以承载[WorkSchedulerExtensionAbility](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-workschedulerextensionability)，并给[WorkSchedulerExtensionAbility](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-workschedulerextensionability)一定的活动周期，开发者可以在对应回调方法中实现自己的任务逻辑。

### 约束与限制

- **数量限制**：一个应用同一时刻最多申请10个延迟任务。
    
- **执行频率限制**：系统会根据应用的活跃分组，对延迟任务做分级管控，限制延迟任务调度的执行频率。
    
    **表1** 应用活跃程度分组
    
    |应用活跃分组|延迟任务执行频率|
    |:--|:--|
    |活跃分组|最小间隔2小时|
    |经常使用分组|最小间隔4小时|
    |常用分组|最小间隔24小时|
    |极少使用分组|最小间隔48小时|
    |受限使用分组|禁止|
    |从未使用分组|禁止|
    
- **超时**：WorkSchedulerExtensionAbility单次回调最长运行2分钟。如果超时不取消，系统会终止对应的Extension进程。
    
- **调度延迟**：系统会根据内存、功耗、设备温度、用户使用习惯等统一调度，如当系统内存资源不足或温度达到一定档位时，系统将延迟调度该任务。
    
- **WorkSchedulerExtensionAbility接口调用限制**：为实现对WorkSchedulerExtensionAbility能力的管控，在WorkSchedulerExtensionAbility中限制以下接口的调用：
    
    [@ohos.resourceschedule.backgroundTaskManager (后台任务管理)](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-resourceschedule-backgroundtaskmanager)
    
    [@ohos.backgroundTaskManager (后台任务管理)](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-backgroundtaskmanager)
    
    [@ohos.multimedia.camera (相机管理)](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera)
    
    [@ohos.multimedia.audio (音频管理)](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-audio)
    
    [@ohos.multimedia.media (媒体服务)](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-media)
    

## 接口说明

**表2** 延迟任务主要接口

以下是延迟任务开发使用的相关接口，更多接口及使用方式请见[延迟任务调度](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-resourceschedule-workscheduler)文档。

|接口名|接口描述|
|:--|:--|
|[startWork(work: WorkInfo): void](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-resourceschedule-workscheduler#workschedulerstartwork)|申请延迟任务。|
|[stopWork(work: WorkInfo, needCancel?: boolean): void](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-resourceschedule-workscheduler#workschedulerstopwork)|取消延迟任务。|
|[getWorkStatus(workId: number, callback: AsyncCallback<WorkInfo>): void](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-resourceschedule-workscheduler#workschedulergetworkstatus)|获取延迟任务状态（Callback形式）。|
|[getWorkStatus(workId: number): Promise<WorkInfo>](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-resourceschedule-workscheduler#workschedulergetworkstatus-1)|获取延迟任务状态（Promise形式）。|
|[obtainAllWorks(callback: AsyncCallback<Array<WorkInfo>>): void](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-resourceschedule-workscheduler#workschedulerobtainallworks10)|获取所有延迟任务（Callback形式）。|
|[obtainAllWorks(): Promise<Array<WorkInfo>>](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-resourceschedule-workscheduler#workschedulerobtainallworks)|获取所有延迟任务（Promise形式）。|
|[stopAndClearWorks(): void](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-resourceschedule-workscheduler#workschedulerstopandclearworks)|停止并清除任务。|
|[isLastWorkTimeOut(workId: number, callback: AsyncCallback<boolean>): void](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-resourceschedule-workscheduler#workschedulerislastworktimeout10)|获取上次任务是否超时（针对RepeatWork，Callback形式）。|
|[isLastWorkTimeOut(workId: number): Promise<boolean>](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-resourceschedule-workscheduler#workschedulerislastworktimeout)|获取上次任务是否超时（针对RepeatWork，Promise形式）。|

**表3** 延迟任务回调接口

以下是延迟任务回调开发使用的相关接口，更多接口及使用方式请见[延迟任务调度回调](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-workschedulerextensionability)文档。

|接口名|接口描述|
|:--|:--|
|[onWorkStart(work: workScheduler.WorkInfo): void](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-workschedulerextensionability#onworkstart)|延迟调度任务开始的回调。|
|[onWorkStop(work: workScheduler.WorkInfo): void](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-workschedulerextensionability#onworkstop)|延迟调度任务结束的回调。|

## 开发步骤

延迟任务调度开发步骤分为两步：实现延迟任务调度扩展能力、实现延迟任务调度。

1. **延迟任务调度扩展能力**：实现WorkSchedulerExtensionAbility开始和结束的回调接口。
    
2. **延迟任务调度**：调用延迟任务接口，实现延迟任务申请、取消等功能。
    

### 实现延迟任务回调扩展能力

1. 新建工程目录。
    
    在工程entry Module对应的ets目录(./entry/src/main/ets)下，新建目录及ArkTS文件，例如新建一个目录并命名为WorkSchedulerExtension。在WorkSchedulerExtension目录下，新建一个ArkTS文件并命名为WorkSchedulerExtension.ets，用以实现延迟任务回调接口。
    
2. 导入模块。
    
    1. import { WorkSchedulerExtensionAbility, workScheduler } from '@kit.BackgroundTasksKit';
    
3. 实现WorkSchedulerExtension生命周期接口。
    
    1. export default class MyWorkSchedulerExtensionAbility extends WorkSchedulerExtensionAbility {
    2.   // 延迟任务开始回调
    3.   onWorkStart(workInfo: workScheduler.WorkInfo) {
    4.     console.info(`onWorkStart, workInfo = ${JSON.stringify(workInfo)}`);
    5.     // 打印 parameters中的参数，如：参数key1
    6.     // console.info(`work info parameters: ${JSON.parse(workInfo.parameters?.toString()).key1}`)
    7.   }
    
    8.   // 延迟任务结束回调。当延迟任务2分钟超时或应用调用stopWork接口取消任务时，触发该回调。
    9.   onWorkStop(workInfo: workScheduler.WorkInfo) {
    10.     console.info(`onWorkStop, workInfo is ${JSON.stringify(workInfo)}`);
    11.   }
    12. }
    
4. 在[module.json5配置文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file)中注册WorkSchedulerExtensionAbility，并设置如下标签：
    
    - type标签设置为“workScheduler”。
        
    - srcEntry标签设置为当前ExtensionAbility组件所对应的代码路径。
        
    
    1. {
    2.   "module": {
    3.       "extensionAbilities": [
    4.         {
    5.           "name": "MyWorkSchedulerExtensionAbility",
    6.           "srcEntry": "./ets/WorkSchedulerExtension/WorkSchedulerExtension.ets",
    7.           "type": "workScheduler"
    8.         }
    9.       ]
    10.   }
    11. }
    

### 实现延迟任务调度

1. 导入模块。
    
    1. import { workScheduler } from '@kit.BackgroundTasksKit';
    2. import { BusinessError } from '@kit.BasicServicesKit';
    
2. 申请延迟任务。
    
    1. // 创建workinfo
    2. const workInfo: workScheduler.WorkInfo = {
    3.   workId: 1,
    4.   networkType: workScheduler.NetworkType.NETWORK_TYPE_WIFI,
    5.   bundleName: 'com.example.application',
    6.   abilityName: 'MyWorkSchedulerExtensionAbility'
    7. }
    
    8. try {
    9.   workScheduler.startWork(workInfo);
    10.   console.info(`startWork success`);
    11. } catch (error) {
    12.   console.error(`startWork failed. code is ${(error as BusinessError).code} message is ${(error as BusinessError).message}`);
    13. }
    
3. 取消延迟任务。
    
    1. // 创建workinfo
    2. const workInfo: workScheduler.WorkInfo = {
    3.   workId: 1,
    4.   networkType: workScheduler.NetworkType.NETWORK_TYPE_WIFI,
    5.   bundleName: 'com.example.application',
    6.   abilityName: 'MyWorkSchedulerExtensionAbility'
    7. }
    
    8. try {
    9.   workScheduler.stopWork(workInfo);
    10.   console.info(`stopWork success`);
    11. } catch (error) {
    12.   console.error(`stopWork failed. code is ${(error as BusinessError).code} message is ${(error as BusinessError).message}`);
    13. }
    

### 延迟任务调度功能验证

确认延迟任务WorkSchedulerExtensionAbility回调方法onWorkStart、onWorkStop实现是否正确、是否可以成功回调

延迟任务申请成功之后，需要等到条件满足后才可以执行延迟任务回调，为了快速验证延迟任务回调功能是否正确，可以通过以下[hidumper命令](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/hidumper)手动触发延迟任务执行回调。

1. $ hidumper -s 1904 -a '-t com.example.application MyWorkSchedulerExtensionAbility'

2. -------------------------------[ability]-------------------------------

3. ----------------------------------WorkSchedule----------------------------------

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/continuous-task "长时任务(ArkTS)")
# Core File Kit简介

更新时间: 2025-12-16 16:38

Core File Kit（文件基础服务）为开发者提供一套访问和管理应用文件和用户文件的能力。帮助用户更高效地管理、查找和备份各类文件，使用户能够轻松应对各种文件管理的需求。

## Core File Kit概述

在Core File Kit套件中，按文件所有者的不同，有如下文件分类模型，其示意图如下：

- [应用文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-file-overview)：文件所有者为应用，包括应用安装文件、应用资源文件、应用缓存文件等。
    
- [用户文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/user-file-overview)：文件所有者为登录到该终端设备的用户，包括用户私有的图片、视频、音频、文档等。
    
- 系统文件：与应用和用户无关的其它文件，包括公共库、设备文件、系统资源文件等。这类文件不需要开发者进行文件管理，本文不展开介绍。
    

按文件系统管理的文件存储位置（数据源位置）的不同，有如下文件系统分类模型：

- 本地文件系统：提供本地设备或外置存储设备（如U盘、移动硬盘）的文件访问能力。本地文件系统是最基本的文件系统，本文不展开介绍。
    
- [分布式文件系统](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/distributed-fs-overview)：提供跨设备的文件访问能力。所谓跨设备，指文件不一定存储在本地设备或外置存储设备，而是通过计算机网络与其它分布式设备相连。
    

**图1** 文件分类模型示意图

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163818.12343297878782675776484284853112:50001231000000:2800:AE73EAD40596ACF515996D91A46E492CF7CFDB38C913F324D1F71B14612773F1.png)

## Kit使用场景

Core File Kit常见的使用场景：

- 应用文件访问和文件分享。
- 应用数据备份恢复。
- 选择与保存用户文件。
- 跨设备的文件访问和分享能力。

## 能力范围

- 支持对应用文件进行查看、创建、读写、删除、移动、复制、获取属性等访问操作。
- 支持应用文件上传到网络服务器和网络服务器下载网络资源文件到本地应用文件目录。
- 支持获取当前应用的存储空间大小、指定文件系统的剩余空间大小和指定文件系统的总空间大小。
- 支持应用分享文件给其它应用和使用其它应用分享的文件。
- 支持应用接入数据备份恢复，在接入后，应用可通过修改配置文件定制备份恢复框架的行为，包括是否允许备份恢复、备份哪些数据。
- 提供[用户文件访问框架](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/core-file-kit-intro#%E7%94%A8%E6%88%B7%E6%96%87%E4%BB%B6%E8%AE%BF%E9%97%AE%E6%A1%86%E6%9E%B6)，用于开发者访问和管理用户文件。例如选择与保存用户文件。
- 支持跨设备的文件访问和拷贝能力。

## 亮点/特征

- 沙箱隔离：
    
    访问和管理应用文件，对于每个应用，系统会在内部存储空间映射出一个专属的“[应用沙箱目录](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-sandbox-directory)”，它是“[应用文件目录](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-sandbox-directory#%E5%BA%94%E7%94%A8%E6%96%87%E4%BB%B6%E7%9B%AE%E5%BD%95%E4%B8%8E%E5%BA%94%E7%94%A8%E6%96%87%E4%BB%B6%E8%B7%AF%E5%BE%84)”与一部分系统文件（应用运行必需的少量系统文件）所在的目录组成的集合。有以下优点：
    
    - 隔离性：应用沙箱提供了一个完全隔离的环境，使用户可以安全地访问应用文件。
    - 安全性：应用沙箱限制了应用可见的数据的最小范围，保护了应用文件的安全。
    
- 应用分享：
    
    应用之间可以通过分享URI（Uniform Resource Identifier）或文件描述符FD（File Descriptor）的方式，进行文件共享。有以下优点：
    
    - 便携性：应用之间进行文件分享，省去了用户在多个应用间切换的麻烦，简化了操作步骤，提高了效率。
    - 高效性：应用间的文件分享能够更快地完成文件的传输，减少了因多次跳转和等待而浪费的时间。
    - 数据一致性：应用间的文件分享能够确保数据的完整性和一致性，避免数据在传输过程中出现损坏或丢失的情况。
    - 安全性：应用间的文件分享可以确保文件的安全性，避免文件被非法获取或篡改。同时，通过文件授权访问的方式，可以进一步增强文件的安全性。
    

## 框架原理

### 应用文件访问框架

应用文件访问框架是通过基础文件操作接口（[ohos.file.fs](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-file-fs)）实现。开发者无需了解内部实现，基础文件操作接口功能详情请参考[接口说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-file-access#%E6%8E%A5%E5%8F%A3%E8%AF%B4%E6%98%8E)。

### 用户文件访问框架

用户文件访问框架（File Access Framework）是一套提供给开发者访问和管理用户文件的基础框架。该框架依托于HarmonyOS的ExtensionAbility组件机制，提供了一套统一访问用户文件的方法和接口。

**图2** 用户文件访问框架示意图

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163818.54847361410404992859194216179195:50001231000000:2800:44EFAC8221E4AA865822D8BCCD829952521144EE6D60B8318265E5228CFC0B0A.png)

- 系统应用或三方应用（即图中的文件访问客户端）若需访问用户文件，如选择一张照片或保存多个文档等，可以通过拉起“文件选择器应用”来实现。
    
- FilePicker：系统预置应用，提供文件访问客户端选择和保存文件的能力，无需配置权限。FilePicker的使用指导请参见[选择用户文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/select-user-file)。
    
- FileManager：对于设备开发者，还可以按需开发自己的文件选择器或文件管理器应用。该功能不向三方应用开放。
    
- File Access Framework（用户文件访问框架）的主要功能模块如下：
    
    - File Access Helper：提供给文件管理器和文件选择器访问用户文件的API接口。
    - File Access ExtensionAbility：提供文件访问框架能力，由内卡文件管理服务UserFileManager和外卡文件管理服务ExternalFileManager组成，实现对应的文件访问功能。
        - UserFileManager：内卡文件管理服务，基于File Access ExtensionAbility框架实现，用于管理内置存储设备上的文件。
        - ExternalFileManager：外卡文件管理服务，基于File Access ExtensionAbility框架实现，用于管理外置存储设备上的文件。

## 与相关Kit的关系

Ability Kit：Core File Kit中用户文件访问框架依赖Ability Kit提供的Extension基础能力，并受Ability Kit服务调度管理。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/core-file-kit "Core File Kit（文件基础服务）")
# Core File Kit简介

更新时间: 2025-12-16 16:38

Core File Kit（文件基础服务）为开发者提供一套访问和管理应用文件和用户文件的能力。帮助用户更高效地管理、查找和备份各类文件，使用户能够轻松应对各种文件管理的需求。

## Core File Kit概述

在Core File Kit套件中，按文件所有者的不同，有如下文件分类模型，其示意图如下：

- [应用文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-file-overview)：文件所有者为应用，包括应用安装文件、应用资源文件、应用缓存文件等。
    
- [用户文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/user-file-overview)：文件所有者为登录到该终端设备的用户，包括用户私有的图片、视频、音频、文档等。
    
- 系统文件：与应用和用户无关的其它文件，包括公共库、设备文件、系统资源文件等。这类文件不需要开发者进行文件管理，本文不展开介绍。
    

按文件系统管理的文件存储位置（数据源位置）的不同，有如下文件系统分类模型：

- 本地文件系统：提供本地设备或外置存储设备（如U盘、移动硬盘）的文件访问能力。本地文件系统是最基本的文件系统，本文不展开介绍。
    
- [分布式文件系统](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/distributed-fs-overview)：提供跨设备的文件访问能力。所谓跨设备，指文件不一定存储在本地设备或外置存储设备，而是通过计算机网络与其它分布式设备相连。
    

**图1** 文件分类模型示意图

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163818.12343297878782675776484284853112:50001231000000:2800:AE73EAD40596ACF515996D91A46E492CF7CFDB38C913F324D1F71B14612773F1.png)

## Kit使用场景

Core File Kit常见的使用场景：

- 应用文件访问和文件分享。
- 应用数据备份恢复。
- 选择与保存用户文件。
- 跨设备的文件访问和分享能力。

## 能力范围

- 支持对应用文件进行查看、创建、读写、删除、移动、复制、获取属性等访问操作。
- 支持应用文件上传到网络服务器和网络服务器下载网络资源文件到本地应用文件目录。
- 支持获取当前应用的存储空间大小、指定文件系统的剩余空间大小和指定文件系统的总空间大小。
- 支持应用分享文件给其它应用和使用其它应用分享的文件。
- 支持应用接入数据备份恢复，在接入后，应用可通过修改配置文件定制备份恢复框架的行为，包括是否允许备份恢复、备份哪些数据。
- 提供[用户文件访问框架](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/core-file-kit-intro#%E7%94%A8%E6%88%B7%E6%96%87%E4%BB%B6%E8%AE%BF%E9%97%AE%E6%A1%86%E6%9E%B6)，用于开发者访问和管理用户文件。例如选择与保存用户文件。
- 支持跨设备的文件访问和拷贝能力。

## 亮点/特征

- 沙箱隔离：
    
    访问和管理应用文件，对于每个应用，系统会在内部存储空间映射出一个专属的“[应用沙箱目录](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-sandbox-directory)”，它是“[应用文件目录](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-sandbox-directory#%E5%BA%94%E7%94%A8%E6%96%87%E4%BB%B6%E7%9B%AE%E5%BD%95%E4%B8%8E%E5%BA%94%E7%94%A8%E6%96%87%E4%BB%B6%E8%B7%AF%E5%BE%84)”与一部分系统文件（应用运行必需的少量系统文件）所在的目录组成的集合。有以下优点：
    
    - 隔离性：应用沙箱提供了一个完全隔离的环境，使用户可以安全地访问应用文件。
    - 安全性：应用沙箱限制了应用可见的数据的最小范围，保护了应用文件的安全。
    
- 应用分享：
    
    应用之间可以通过分享URI（Uniform Resource Identifier）或文件描述符FD（File Descriptor）的方式，进行文件共享。有以下优点：
    
    - 便携性：应用之间进行文件分享，省去了用户在多个应用间切换的麻烦，简化了操作步骤，提高了效率。
    - 高效性：应用间的文件分享能够更快地完成文件的传输，减少了因多次跳转和等待而浪费的时间。
    - 数据一致性：应用间的文件分享能够确保数据的完整性和一致性，避免数据在传输过程中出现损坏或丢失的情况。
    - 安全性：应用间的文件分享可以确保文件的安全性，避免文件被非法获取或篡改。同时，通过文件授权访问的方式，可以进一步增强文件的安全性。
    

## 框架原理

### 应用文件访问框架

应用文件访问框架是通过基础文件操作接口（[ohos.file.fs](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-file-fs)）实现。开发者无需了解内部实现，基础文件操作接口功能详情请参考[接口说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-file-access#%E6%8E%A5%E5%8F%A3%E8%AF%B4%E6%98%8E)。

### 用户文件访问框架

用户文件访问框架（File Access Framework）是一套提供给开发者访问和管理用户文件的基础框架。该框架依托于HarmonyOS的ExtensionAbility组件机制，提供了一套统一访问用户文件的方法和接口。

**图2** 用户文件访问框架示意图

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163818.54847361410404992859194216179195:50001231000000:2800:44EFAC8221E4AA865822D8BCCD829952521144EE6D60B8318265E5228CFC0B0A.png)

- 系统应用或三方应用（即图中的文件访问客户端）若需访问用户文件，如选择一张照片或保存多个文档等，可以通过拉起“文件选择器应用”来实现。
    
- FilePicker：系统预置应用，提供文件访问客户端选择和保存文件的能力，无需配置权限。FilePicker的使用指导请参见[选择用户文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/select-user-file)。
    
- FileManager：对于设备开发者，还可以按需开发自己的文件选择器或文件管理器应用。该功能不向三方应用开放。
    
- File Access Framework（用户文件访问框架）的主要功能模块如下：
    
    - File Access Helper：提供给文件管理器和文件选择器访问用户文件的API接口。
    - File Access ExtensionAbility：提供文件访问框架能力，由内卡文件管理服务UserFileManager和外卡文件管理服务ExternalFileManager组成，实现对应的文件访问功能。
        - UserFileManager：内卡文件管理服务，基于File Access ExtensionAbility框架实现，用于管理内置存储设备上的文件。
        - ExternalFileManager：外卡文件管理服务，基于File Access ExtensionAbility框架实现，用于管理外置存储设备上的文件。

## 与相关Kit的关系

Ability Kit：Core File Kit中用户文件访问框架依赖Ability Kit提供的Extension基础能力，并受Ability Kit服务调度管理。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/core-file-kit "Core File Kit（文件基础服务）")
# 应用沙箱目录

更新时间: 2025-12-16 16:38

应用沙箱是一种以安全防护为目的的隔离机制，避免数据受到恶意路径穿越访问。在这种沙箱的保护机制下，应用可见的目录范围即为“应用沙箱目录”。

- 对于每个应用，系统会在内部存储空间映射出一个专属的“应用沙箱目录”，它是“[应用文件目录](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-sandbox-directory#%E5%BA%94%E7%94%A8%E6%96%87%E4%BB%B6%E7%9B%AE%E5%BD%95%E4%B8%8E%E5%BA%94%E7%94%A8%E6%96%87%E4%BB%B6%E8%B7%AF%E5%BE%84)”与一部分系统文件（应用运行必需的少量系统文件）所在的目录组成的集合。
    
- 应用沙箱限制了应用可见的数据范围。在“应用沙箱目录”中，应用默认仅能看到自己的应用文件以及少量的系统文件（应用运行必需的少量系统文件）。在全量挂载的设备平台上，文件管理应用可查看其他应用存放在el2/base下的数据。
    
- 应用可以在“应用文件目录”下保存和处理自己的应用文件；系统文件及其目录对于应用是只读的；应用若需要访问用户文件，请参考[用户文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/user-file-overview)使用指导。
    

下图展示了应用沙箱下，应用可访问的文件范围和方式。

**图1** 应用沙箱文件访问关系图

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163835.36355298796544001521497218886649:50001231000000:2800:7817BA202941B98EB284C58A0FA3BC537A4386845D3C84780D3AD771D8CE0FD1.png)

## 应用沙箱目录与应用沙箱路径

在应用沙箱保护机制下，应用无法获知除自身应用文件目录之外的其他应用或用户的数据目录位置及存在。同时，所有应用的目录可见范围均经过权限隔离与文件路径挂载隔离，形成了独立的路径视图，屏蔽了实际物理路径：

- 如下图所示，在普通应用（也称三方应用）视角下，不仅可见的目录与文件数量限制了范围，并且可见的目录与文件路径也与系统进程等其他进程看到的不同。我们将普通应用视角下看到的“应用沙箱目录”下某个文件或某个具体目录的路径，称为“应用沙箱路径”。
    
- 开发者在应用开发调试时，可能需要向应用沙箱下推送一些文件以期望在应用内访问或测试。可以通过DevEco Studio向应用安装路径中放入目标文件，详见[应用安装资源访问](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/resource-categories-and-access#%E8%B5%84%E6%BA%90%E8%AE%BF%E9%97%AE)。
    
- 实际物理路径与沙箱路径并非1:1的映射关系，沙箱路径总是少于系统进程视角可见的物理路径。部分调试进程视角下的物理路径在对应的应用沙箱目录下没有对应路径。
    

**图2** 应用沙箱路径（不同权限与角色的进程下可见的文件路径不同）

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163835.01403242970290659208674374020141:50001231000000:2800:AEFA75C4A4B0D1E75BC63AC9C104CE864B87BF3276B9B34ABA9F13875E9F675D.png)

## 应用文件目录与应用文件路径

如前文所述，“应用沙箱目录”内分为两类：应用文件目录和系统文件目录。

系统文件目录对应用的可见范围由HarmonyOS系统预置，开发者无需关注。

在此主要介绍应用文件目录，如下图所示。应用文件目录下的文件或目录路径称为应用文件路径。各文件路径具有不同的属性和特征。

**图3** 应用文件目录结构图

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163835.48200691378062793453489204698369:50001231000000:2800:5A475D29FB6CE37E095087B562FA88B03DD18E5B815D0AE5F23A03073CEAB604.png)

说明

- 禁止直接使用上图中四级目录之前的目录名组成的路径字符串，否则可能导致后续应用版本因应用文件路径变化导致不兼容问题。
- 应通过Context属性获取应用文件路径，包括但不限于上图中绿色背景的路径。 Context上下文获取及上述应用文件路径的获取，详见[应用上下文Context](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/application-context-stage)。

1. 一级目录data/：应用文件目录。
    
2. 二级目录storage/：应用持久化文件目录。
    
3. 三级目录el1/~el5/：不同文件加密类型。
    
    EL1(Encryption Level 1):
    
    - 保护设备上所有文件的基础安全能力。设备开机后，用户无需完成身份验证即可访问EL1保护的文件。除非有特殊需求，否则不建议使用此方法。
    - 如果直接窃取设备存储介质上的密文，攻击者无法脱机进行解密。
    
    EL2(Encryption Level 2):
    
    - 在EL1的基础上，增加首次认证后的文件保护能力。设备开机后，用户在通过首次认证后，通过EL2能力保护的文件才能被访问。此后只要设备没有关机，通过EL2能力保护的文件一直可被访问。推荐应用默认使用该方式。
    - 如果在关机后丢失手机，攻击者无法读取EL2保护的文件。
    
    EL3(Encryption Level 3):
    
    - 与EL4整体能力类似，但和EL4的区别是，在锁屏下可创建新的文件，但无法读取。如无特殊必要，无需使用该方式。
    
    EL4(Encryption Level 4):
    
    - 在EL2的基础上，增加设备锁屏时的文件保护能力。在用户锁屏时，通过EL4能力保护的数据将无法被访问。如无特殊必要，无需使用该方式。
    - 如果设备在锁屏状态下被盗，攻击者无法读取EL4保护的文件。
    
    EL5(Encryption Level 5):
    
    - 在EL2的基础上，增加设备锁屏时的文件保护能力。在用户锁屏后，满足一定条件时，通过EL5能力保护的数据将无法被访问，但可以继续创建和读写新的文件。如无特殊必要，无需使用该方式。
    - 默认情况下不会生成EL5的相关目录，应用若需要使用EL5目录，则需要配置访问E类加密数据库的权限。具体配置方法详见[E类加密数据库的使用](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/encrypted_estore_guidelines)。
    
    说明
    
    应用如无特殊需要，应将数据存放在el2加密目录下，以尽可能保证数据安全。但是对于某些场景，一些应用文件需要在用户首次认证前就可被访问，例如时钟、闹铃、壁纸等，此时应用需要将这些文件存放到设备级加密区（el1）。
    
    开发者可通过监听[COMMON_EVENT_USER_UNLOCKED](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/commoneventmanager-definitions#common_event_user_unlocked)事件感知当前用户首次认证完成。
    
    切换应用文件加密类型目录的方法请参见[获取和修改加密分区](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/application-context-stage#%E8%8E%B7%E5%8F%96%E5%92%8C%E4%BF%AE%E6%94%B9%E5%8A%A0%E5%AF%86%E5%88%86%E5%8C%BA)。
    
4. 四级、五级目录：
    
    通过ApplicationContext获取distributedfiles目录或base下的files、cache、preferences、temp等目录的路径，应用全局信息存放在这些目录下。
    
    通过UIAbilityContext、AbilityStageContext、ExtensionContext可以获取HAP级别应用文件路径。HAP信息可以存放在这些目录下，存放在此目录的文件会跟随HAP的卸载而删除，不会影响App级别目录下的文件。在开发态，一个应用包含一个或者多个HAP，详见[Stage模型应用程序包结构](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/application-package-structure-stage)。
    
    应用文件路径具体说明及生命周期如下表所示。
    
    **表1** 应用文件路径详细说明
    
    |目录名|Context属性名称|类型|说明|
    |:--|:--|:--|:--|
    |bundle|bundleCodeDir|安装文件路径|应用安装后的App的HAP资源包所在目录；随应用卸载而清理。<br><br>不能通过拼接路径访问资源文件，应使用[资源管理接口](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-resource-manager)访问资源。<br><br>可以用于存储应用的代码资源数据，主要包括应用安装的HAP资源包、可重复使用的库文件以及插件资源等。此路径下存储的代码资源数据可以被用于动态加载。|
    |base|NA|本设备文件路径|应用在本设备上存放持久化数据的目录（随应用卸载而清理），子目录包含files/、cache/、temp/和haps/。<br><br>不建议将cookie、密码和token等高风险信息明文存储在此目录下。|
    |database|databaseDir|数据库路径|应用在el2加密条件下存放通过分布式数据库服务操作的文件目录；随应用卸载而清理。<br><br>仅用于保存应用的私有数据库数据，主要包括数据库文件等。此路径下仅适用于存储分布式数据库相关文件数据。|
    |distributedfiles|distributedFilesDir|分布式文件路径|应用在el2加密条件下存放分布式文件的目录，应用将文件放入该目录可分布式跨设备直接访问；随应用卸载而清理。<br><br>可以用于保存应用分布式场景下的数据，主要包括应用多设备共享文件、应用多设备备份文件、应用多设备群组协助文件。此路径下存储这些数据，使得应用更加适合多设备使用场景。|
    |files|filesDir|应用通用文件路径|应用在本设备内部存储上通用的存放默认长期保存的文件路径；随应用卸载而清理。<br><br>可以用于保存应用的任何私有数据，主要包括用户持久性文件、图片、媒体文件以及日志文件等。此路径下存储这些数据，使得数据保持私有、安全且持久有效。|
    |cache|cacheDir|应用缓存文件路径|应用在本设备内部存储上用于缓存下载的文件或可重新生成的缓存文件的路径，应用cache目录大小超过配额或者系统空间达到一定条件，自动触发清理该目录下文件；用户通过系统空间管理类应用也可能触发清理该目录。应用需判断文件是否仍存在，决策是否需重新缓存该文件；随应用卸载而清理。<br><br>可以用于保存应用的缓存数据，主要包括离线数据、图片缓存、数据库备份以及临时文件等。此路径下存储的数据可能会被系统自动清理，因此不要存储重要数据。|
    |preferences|preferencesDir|应用首选项文件路径|应用在本设备内部存储上通过数据库API存储配置类或首选项的目录；随应用卸载而清理。详见[通过用户首选项实现数据持久化](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/data-persistence-by-preferences)。<br><br>可以用于保存应用的首选项数据，主要包括应用首选项文件以及配置文件等。此路径下仅适用于存储小量数据。|
    |temp|tempDir|应用临时文件路径|应用在本设备内部存储上仅在应用运行期间产生和需要的文件，应用退出后即清理。<br><br>可以用于保存应用的临时生成的数据，主要包括数据库缓存、图片缓存、临时日志文件、以及下载的应用安装包文件等。此路径下存储使用后即可删除的数据。|
    

## 应用沙箱路径和真实物理路径的对应关系

在应用沙箱路径下读写文件，经过映射转换，实际读写的是真实物理路径中的应用文件，应用沙箱路径与真实物理路径对应关系如下表所示。

其中<USERID>为当前用户ID，从100开始递增，<EXTENSIONPATH>为moduleName-extensionName。应用是否以Extension独立沙箱运行可参考[ExtensionAbility组件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/extensionability-overview)。

|应用沙箱路径|物理路径|
|:--|:--|
|/data/storage/el1/bundle|应用安装包目录：<br><br>/data/app/el1/bundle/public/<PACKAGENAME>|
|/data/storage/el1/base|应用el1级别加密数据目录：<br><br>- 非独立沙箱运行的应用：/data/app/el1/<USERID>/base/<PACKAGENAME><br><br>- 以独立沙箱运行的Extension应用： /data/app/el1/<USERID>/base/+extension-<EXTENSIONPATH>+<PACKAGENAME>|
|/data/storage/el2/base|应用el2级别加密数据目录：<br><br>- 非独立沙箱运行的应用：/data/app/el2/<USERID>/base/<PACKAGENAME><br><br>- 以独立沙箱运行的Extension应用： /data/app/el2/<USERID>/base/+extension-<EXTENSIONPATH>+<PACKAGENAME>|
|/data/storage/el1/database|应用el1级别加密数据库目录：<br><br>- 非独立沙箱运行的应用：/data/app/el1/<USERID>/database/<PACKAGENAME><br><br>- 以独立沙箱运行的Extension应用：/data/app/el1/<USERID>/database/+extension-<EXTENSIONPATH>+<PACKAGENAME>|
|/data/storage/el2/database|应用el2级别加密数据库目录：<br><br>- 非独立沙箱运行的应用：/data/app/el2/<USERID>/database/<PACKAGENAME><br><br>- 以独立沙箱运行的Extension应用：/data/app/el2/<USERID>/database/+extension-<EXTENSIONPATH>+<PACKAGENAME>|
|/data/storage/el2/distributedfiles|/mnt/hmdfs/<USERID>/account/merge_view/data/<PACKAGENAME>|

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-file-overview "应用文件概述")
# 应用文件分享

更新时间: 2025-12-16 16:38

应用文件分享是应用之间通过分享URI（Uniform Resource Identifier）进行文件共享的过程。

## 通过拉起文件处理类应用进行文件分享(startAbility)

基于[文件选择器(startAbility)](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/file-processing-apps-startup)的分享方式，应用可分享单个文件，通过[ohos.app.ability.wantConstant的wantConstant.Flags接口](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-app-ability-wantconstant#flags)以只读或读写权限授权给其他应用。被分享应用可通过[ohos.file.fs的fs.open](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-file-fs#fsopen)打开URI，并进行读写操作。

## 应用可分享目录

|沙箱路径|说明|
|:--|:--|
|/data/storage/el1/base|应用el1级别加密数据目录|
|/data/storage/el2/base|应用el2级别加密数据目录|
|/data/storage/el2/distributedfiles|应用el2加密级别有账号分布式数据融合目录|

## 文件URI规范

文件URI的格式：

格式为：file://<bundleName>/<path>

- file：文件URI的标志。
    
- bundleName：该文件资源的属主。
    
- path：文件资源在应用沙箱中的路径。
    

注意

1. 因URI处理涉及编解码，系统无法保证应用自行拼接的URI地址的可用性。
2. 推荐使用系统提供的接口获取URI，如[getUriFromPath接口](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-file-fileuri#fileurigeturifrompath)。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-fs-space-statistics "应用及文件系统空间统计")
# 选择用户文件

更新时间: 2025-12-16 16:39

用户需要分享文件、保存图片、视频等用户文件时，开发者可以通过系统预置的[文件选择器（FilePicker）](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-file-picker)，实现该能力。通过Picker访问相关文件，将拉起对应的应用，引导用户完成界面操作，接口本身无需申请权限。Picker获取的URI只具有临时权限，获取持久化权限需要通过[FilePicker设置永久授权](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/file-persistpermission#%E9%80%9A%E8%BF%87picker%E8%8E%B7%E5%8F%96%E4%B8%B4%E6%97%B6%E6%8E%88%E6%9D%83%E5%B9%B6%E8%BF%9B%E8%A1%8C%E6%8E%88%E6%9D%83%E6%8C%81%E4%B9%85%E5%8C%96)方式获取。

根据用户文件的常见类型，选择器（FilePicker）分别提供以下选项：

- [PhotoViewPicker](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-file-picker#photoviewpickerdeprecated)：适用于图片或视频类型文件的选择与保存（该接口在后续版本不再演进）。请使用[PhotoAccessHelper的PhotoViewPicker](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-photoaccesshelper-photoviewpicker)来选择图片文件。请使用[安全控件保存媒体库资源](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/photoaccesshelper-savebutton)。
    
- [DocumentViewPicker](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-file-picker#documentviewpicker)：适用于文件类型文件的选择与保存。DocumentViewPicker对接的选择资源来自于FilePicker，负责文件类型的资源管理，文件类型不区分后缀，比如浏览器下载的图片、文档等，都属于文件类型。
    
- [AudioViewPicker](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-file-picker#audioviewpicker)：适用于音频类型文件的选择与保存。AudioViewPicker目前对接的选择资源来自于AudioPicker。
    

## 选择图片或视频类文件

[PhotoViewPicker](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-file-picker#photoviewpickerdeprecated)在后续版本不再演进，请使用[PhotoAccessHelper的PhotoViewPicker](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-photoaccesshelper-photoviewpicker)来选择图片文件。

## 选择文档类文件

1. 导入选择器模块和基础文件API模块。
    
    1. import  { picker } from '@kit.CoreFileKit';
    2. import { fileIo as fs } from '@kit.CoreFileKit';
    3. import { common } from '@kit.AbilityKit';
    4. import { BusinessError } from '@kit.BasicServicesKit';
    
2. 创建文件类型、文件选择选项实例。
    
    1. const documentSelectOptions = new picker.DocumentSelectOptions();
    2. // 选择文档的最大数目（可选）。
    3. documentSelectOptions.maxSelectNumber = 5;
    4. // 指定选择的文件或者目录的URI（可选）。
    5. documentSelectOptions.defaultFilePathUri = "file://docs/storage/Users/currentUser/test";
    6. // 选择的文档类型，默认值是FILE(文件类型)。该参数在2in1设备中可正常使用，在其他设备中无效果。
    7. documentSelectOptions.selectMode = picker.DocumentSelectMode.FILE;
    8. // 选择文件的后缀类型['后缀类型描述|后缀类型']（可选，不传该参数，默认不过滤，即显示所有文件），若选择项存在多个后缀名，则每一个后缀名之间用英文逗号进行分隔（可选），后缀类型名不能超过100。此外2in1设备支持通配符方式['所有文件(*.*)|.*']（说明：从API version 17开始，手机支持该配置），表示为显示所有文件。
    9.  documentSelectOptions.fileSuffixFilters = ['图片(.png, .jpg)|.png,.jpg', '文档|.txt', '视频|.mp4', '.pdf'];
    10. //选择是否对指定文件或目录授权，true为授权，当为true时，defaultFilePathUri为必选参数，拉起文管授权界面；false为非授权(默认为false)，拉起常规文管界面（可选）。该参数在2in1设备中可正常使用，在其他设备中无效果。
    11. documentSelectOptions.authMode = false;
    12. //批量授权模式，默认为false（非批量授权模式）。当multiAuthMode为true时为批量授权模式。当multiAuthMode为true时，只有multiUriArray参数生效，其他参数不生效。该参数在Phone设备中可正常使用，在其他设备中无效果。
    13. documentSelectOptions.multiAuthMode = false;
    14. //需要传入批量授权的uri数组（仅支持文件，文件夹不生效）。配合multiAuthMode使用。当multiAuthMode为false时，配置该参数不生效。该参数在Phone设备中可正常使用，在其他设备中无效果。
    15. documentSelectOptions.multiUriArray = ["file://docs/storage/Users/currentUser/test", "file://docs/storage/Users/currentUser/2test"];
    16. //开启聚合视图模式，支持拉起文件管理应用的聚合视图。默认为DEFAULT，表示该参数不生效，非聚合视图。当该参数置为非DEFAULT时，其他参数不生效。该参数在Phone设备中可正常使用，在其他设备中无效果。
    17. documentSelectOptions.mergeMode = picker.MergeTypeMode.DEFAULT;
    18. //是否支持加密（仅支持文件，文件夹不生效），默认为false。该参数为true时，在Picker界面可以选择对文件进行加密。（说明：从API version 19开始支持该参数）。
    19. documentSelectOptions.isEncryptionSupported = false;
    
3. 创建[文件选择器DocumentViewPicker](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-file-picker#documentviewpicker)实例。调用[select()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-file-picker#select-3)接口拉起FilePicker应用界面进行文件选择。
    
    1. let uris: string[] = [];
    2. // 请在组件内获取context，确保this.getUIContext().getHostContext()返回结果为UIAbilityContext
    3. let context = this.getUIContext().getHostContext() as common.UIAbilityContext;
    4. // 创建文件选择器实例
    5. const documentViewPicker = new picker.DocumentViewPicker(context);
    6. documentViewPicker.select(documentSelectOptions).then((documentSelectResult: Array<string>) => {
    7.   //文件选择成功后，返回被选中文档的URI结果集。
    8.   uris = documentSelectResult;
    9.   console.info('documentViewPicker.select to file succeed and uris are:' + uris);
    10. }).catch((err: BusinessError) => {
    11.   console.error(`Invoke documentViewPicker.select failed, code is ${err.code}, message is ${err.message}`);
    12. })
    
    注意
    
    1. 使用Picker获取的[select()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-file-picker#select-3)返回的URI权限是临时只读权限，待退出应用后台后，获取的临时权限就会失效。
        
    2. 如果想要获取持久化权限，请参考[文件持久化授权访问](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/file-persistpermission#%E9%80%9A%E8%BF%87picker%E8%8E%B7%E5%8F%96%E4%B8%B4%E6%97%B6%E6%8E%88%E6%9D%83%E5%B9%B6%E8%BF%9B%E8%A1%8C%E6%8E%88%E6%9D%83%E6%8C%81%E4%B9%85%E5%8C%96)。
        
    3. 开发者可以根据结果集中URI做进一步的处理。建议定义一个全局变量保存URI。
        
    4. 如有获取元数据需求，可以通过[基础文件API](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-file-fs)和[文件URI](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-file-fileuri)根据URI获取部分文件属性信息，比如文件大小、访问时间、修改时间、文件名、文件路径等。
    
4. 待界面从FilePicker返回后，使用[基础文件API的fs.openSync](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-file-fs#fsopensync)接口通过URI打开这个文件得到文件描述符（fd）。
    
    1. if (uris.length > 0) {
    2.     let uri: string = uris[0];
    3.     //这里需要注意接口权限参数是fs.OpenMode.READ_ONLY。
    4.     let file = fs.openSync(uri, fs.OpenMode.READ_ONLY);
    5.     console.info('file fd: ' + file.fd);
    6.  }
    
5. 通过fd使用[fs.readSync](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-file-fs#readsync)接口读取这个文件内的数据。
    
    1. let buffer = new ArrayBuffer(4096);
    2. let readLen = fs.readSync(file.fd, buffer);
    3. console.info('readSync data to file succeed and buffer size is:' + readLen);
    4. //读取完成后关闭fd。
    5. fs.closeSync(file);
    

## 选择音频类文件

1. 导入选择器模块和基础文件API模块。
    
    1. import  { picker } from '@kit.CoreFileKit';
    2. import { fileIo as fs } from '@kit.CoreFileKit';
    3. import { BusinessError } from '@kit.BasicServicesKit';
    4. import { common } from '@kit.AbilityKit';
    
2. 创建音频类型文件选择选项实例。
    
    说明
    
    目前AudioSelectOptions不支持参数配置，默认可以选择所有类型的用户文件。
    
    1. const audioSelectOptions = new picker.AudioSelectOptions();
    
3. 创建[音频选择器AudioViewPicker](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-file-picker#audioviewpicker)实例。调用[select()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-file-picker#select-5)接口拉起AudioPicker应用界面进行文件选择。
    
    1. let uris: string[] = [];
    2. // 请在组件内获取context，确保this.getUIContext().getHostContext()返回结果为UIAbilityContext
    3. let context = this.getUIContext().getHostContext() as common.UIAbilityContext;
    4. const audioViewPicker = new picker.AudioViewPicker(context);
    5. audioViewPicker.select(audioSelectOptions).then((audioSelectResult: Array<string>) => {
    6.   //文件选择成功后，返回被选中音频的URI结果集。
    7.   uris = audioSelectResult;
    8.   console.info('audioViewPicker.select to file succeed and uri is:' + uris);
    9. }).catch((err: BusinessError) => {
    10.   console.error(`Invoke audioViewPicker.select failed, code is ${err.code}, message is ${err.message}`);
    11. })
    
    注意
    
    12. 使用Picker获取的[select()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-file-picker#select-3)返回的URI权限是临时只读权限，待退出应用后台后，获取的临时权限就会失效。
        
    13. 如果想要获取持久化权限，请参考[文件持久化授权访问](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/file-persistpermission#%E9%80%9A%E8%BF%87picker%E8%8E%B7%E5%8F%96%E4%B8%B4%E6%97%B6%E6%8E%88%E6%9D%83%E5%B9%B6%E8%BF%9B%E8%A1%8C%E6%8E%88%E6%9D%83%E6%8C%81%E4%B9%85%E5%8C%96)。
        
    14. 开发者可以根据结果集中的URI做读取文件数据操作。建议定义一个全局变量保存URI。例如通过[基础文件API](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-file-fs)根据URI拿到音频资源的文件描述符（fd），再配合媒体服务实现音频播放的开发，具体请参考[音频播放开发指导](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/audio-playback-overview)。
    
4. 待界面从AudioPicker返回后，可以使用[基础文件API的fs.openSync](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-file-fs#fsopensync)接口通过URI打开这个文件得到文件描述符（fd）。
    
    1. if (uris.length > 0) {
    2.     let uri: string = uris[0];
    3.     //这里需要注意接口权限参数是fs.OpenMode.READ_ONLY。
    4.        let file = fs.openSync(uri, fs.OpenMode.READ_ONLY);
    5.     console.info('file fd: ' + file.fd);
    6.  }
    
5. 通过fd可以使用[基础文件API的fs.readSync](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-file-fs#readsync)接口读取这个文件内的数据。
    
    1. let buffer = new ArrayBuffer(4096);
    2. let readLen = fs.readSync(file.fd, buffer);
    3. console.info('readSync data to file succeed and buffer size is:' + readLen);
    4. //读取完成后关闭fd。
    5. fs.closeSync(file);
    

## 示例代码

- [选择并查看文档与媒体文件](https://gitee.com/harmonyos_samples/picker)

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/select-save-user-file "选择与保存用户文件")
# 保存用户文件

更新时间: 2025-12-16 16:39

在从网络下载文件到本地或将已有用户文件另存为新的文件路径等场景下，需要使用FilePicker提供的保存用户文件的能力。需关注以下关键点：

**权限说明**

- 通过Picker获取的URI默认只具备**临时读写权限**，临时授权在应用退出后台自动失效。
- 获取持久化权限需要通过[FilePicker设置永久授权](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/file-persistpermission#%E9%80%9A%E8%BF%87picker%E8%8E%B7%E5%8F%96%E4%B8%B4%E6%97%B6%E6%8E%88%E6%9D%83%E5%B9%B6%E8%BF%9B%E8%A1%8C%E6%8E%88%E6%9D%83%E6%8C%81%E4%B9%85%E5%8C%96)方式获取。
- 使用Picker对音频、图片、视频、文档类文件的保存操作**无需申请权限**。

**系统隔离说明**

- 通过Picker保存的文件存储在用户指定的目录。此类文件与图库管理的资源隔离，无法在图库中看到。
- 若开发者需要保存图片、视频资源到图库，可使用用户无感的[安全控件进行保存](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/photoaccesshelper-savebutton#%E4%BD%BF%E7%94%A8%E5%AE%89%E5%85%A8%E6%8E%A7%E4%BB%B6%E4%BF%9D%E5%AD%98%E5%AA%92%E4%BD%93%E5%BA%93%E8%B5%84%E6%BA%90)。

## 保存图片或视频类文件

[PhotoViewPicker](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-file-picker#photoviewpickerdeprecated)在后续版本不再演进，建议使用[Media Library Kit（媒体文件管理服务）中能力来保存媒体库资源](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/photoaccesshelper-savebutton)。

如果开发场景无法调用安全控件进行图片、视频保存，可使用相册管理模块[PhotoAccessHelper.showAssetsCreationDialog](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-photoaccesshelper-photoaccesshelper#showassetscreationdialog12)接口进行保存操作。

## 保存文档类文件

1. 模块导入。
    
    1. import { picker } from '@kit.CoreFileKit';
    2. import { fileIo as fs } from '@kit.CoreFileKit';
    3. import { BusinessError } from '@kit.BasicServicesKit';
    4. import { common } from '@kit.AbilityKit';
    
2. 配置保存选项。
    
    1. // 创建文件管理器选项实例。
    2. const documentSaveOptions = new picker.DocumentSaveOptions();
    3. // 保存文件名（可选）。 默认为空。
    4. documentSaveOptions.newFileNames = ["DocumentViewPicker01.txt"];
    5. //指定保存的文件或者目录的URI（可选）。
    6. documentSaveOptions.defaultFilePathUri = "file://docs/storage/Users/currentUser/test";
    7. // 保存文件类型['后缀类型描述|后缀类型'],选择所有文件：'所有文件(*.*)|.*'（可选） ，如果选择项存在多个后缀（做大限制100个过滤后缀），默认选择第一个。如果不传该参数，默认无过滤后缀。
    8. documentSaveOptions.fileSuffixChoices = ['文档|.txt', '.pdf'];
    
3. 创建[文件选择器DocumentViewPicker](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-file-picker#constructor12)实例。调用[save()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-file-picker#save)接口拉起FilePicker界面进行文件保存。
    
    1. let uris: string[] = [];
    2. // 请在组件内获取context，确保this.getUIContext().getHostContext()返回结果为UIAbilityContext
    3. let context = this.getUIContext().getHostContext() as common.UIAbilityContext;
    4. const documentViewPicker = new picker.DocumentViewPicker(context);
    5. documentViewPicker.save(documentSaveOptions).then((documentSaveResult: Array<string>) => {
    6.   uris = documentSaveResult;
    7.   console.info('documentViewPicker.save to file succeed and uris are:' + uris);
    8. }).catch((err: BusinessError) => {
    9.   console.error(`Invoke documentViewPicker.save failed, code is ${err.code}, message is ${err.message}`);
    10. })
    
    注意
    
    1. URI存储建议：
        
        - 避免在Picker回调中直接操作URI。
        - 建议使用全局变量保存URI以供后续使用。
    2. 快捷保存：
        
        - 可以通过[DOWNLOAD模式](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/save-user-file#download%E6%A8%A1%E5%BC%8F%E4%BF%9D%E5%AD%98%E6%96%87%E4%BB%B6)直达下载目录。
    
4. 待界面从FilePicker返回后，使用[基础文件API的fs.openSync](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-file-fs#fsopensync)接口，通过URI打开这个文件得到文件描述符（fd）。
    
    1. if (uris.length > 0) {
    2.     let uri: string = uris[0];
    3.     //这里需要注意接口权限参数是fs.OpenMode.READ_WRITE。
    4.     let file = fs.openSync(uri, fs.OpenMode.READ_WRITE);
    5.     console.info('file fd: ' + file.fd);
    6.  }
    
5. 通过（fd）使用[基础文件API的fs.writeSync](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-file-fs#writesync)接口对这个文件进行编辑修改，编辑修改完成后关闭（fd）。
    
    1. let writeLen: number = fs.writeSync(file.fd, 'hello, world');
    2. console.info('write data to file succeed and size is:' + writeLen);
    3. fs.closeSync(file);
    

## 保存音频类文件

1. 模块导入。
    
    1. import { picker } from '@kit.CoreFileKit';
    2. import { fileIo as fs } from '@kit.CoreFileKit';
    3. import { BusinessError } from '@kit.BasicServicesKit';
    4. import { common } from '@kit.AbilityKit';
    
2. 配置保存选项。
    
    1. const audioSaveOptions = new picker.AudioSaveOptions();
    2. // 保存文件名（可选）
    3. audioSaveOptions.newFileNames = ['AudioViewPicker01.mp3'];
    
3. 创建[音频选择器AudioViewPicker](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-file-picker#audioviewpicker)实例。调用[save()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-file-picker#save-5)接口拉起FilePicker界面进行文件保存。
    
    1. let uris: string[] = [];
    2. // 请在组件内获取context，确保this.getUIContext().getHostContext()返回结果为UIAbilityContext
    3. let context = this.getUIContext().getHostContext() as common.UIAbilityContext;
    4. const audioViewPicker = new picker.AudioViewPicker(context);
    5. audioViewPicker.save(audioSaveOptions).then((audioSelectResult: Array<string>) => {
    6.   uris = audioSelectResult;
    7.   console.info('audioViewPicker.save to file succeed and uri is:' + uris);
    8. }).catch((err: BusinessError) => {
    9.   console.error(`Invoke audioViewPicker.save failed, code is ${err.code}, message is ${err.message}`);
    10. })
    
    注意
    
    1. URI存储建议：
        
        - 避免在Picker回调中直接操作URI。
        - 建议使用全局变量保存URI以供后续使用。
    2. 快捷保存：
        
        - 可以通过[DOWNLOAD模式](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/save-user-file#download%E6%A8%A1%E5%BC%8F%E4%BF%9D%E5%AD%98%E6%96%87%E4%BB%B6)直达下载目录。
    
4. 待界面从FilePicker返回后，可以使用[基础文件API的fs.openSync](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-file-fs#fsopensync)接口，通过URI打开这个文件得到文件描述符（fd）。
    
    1. if (uris.length > 0) {
    2.     let uri: string = uris[0];
    3.     //这里需要注意接口权限参数是fileIo.OpenMode.READ_WRITE。
    4.     let file = fs.openSync(uri, fs.OpenMode.READ_WRITE);
    5.     console.info('file fd: ' + file.fd);
    6.  }
    
5. 通过（fd）使用[基础文件API的fs.writeSync](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-file-fs#writesync)接口对这个文件进行编辑修改，编辑修改完成后关闭（fd）。
    
    1. let writeLen = fs.writeSync(file.fd, 'hello, world');
    2. console.info('write data to file succeed and size is:' + writeLen);
    3. fs.closeSync(file);
    

## DOWNLOAD模式保存文件

**模式特点**

- 自动创建在Download/包名/目录。
- 跳过文件选择界面直接保存。
- 返回的URI已具备持久化权限， 用户可在该URI下创建文件。

注意

DOWNLOAD模式创建的目录仅用于保存文件，目录之间无访问隔离，不建议保存应用敏感数据。

1. 模块导入。
    
    1. import { fileUri, picker } from '@kit.CoreFileKit';
    2. import { fileIo as fs } from '@kit.CoreFileKit';
    3. import { BusinessError } from '@kit.BasicServicesKit';
    4. import { common } from '@kit.AbilityKit';
    
2. 配置下载模式。
    
    1. const documentSaveOptions = new picker.DocumentSaveOptions();
    2. // 配置保存的模式为DOWNLOAD，若配置了DOWNLOAD模式，此时配置的其他documentSaveOptions参数将不会生效。
    3. documentSaveOptions.pickerMode = picker.DocumentPickerMode.DOWNLOAD;
    
3. 保存到下载目录。
    
    1. let uri: string = '';
    2. // 请在组件内获取context，确保this.getUIContext().getHostContext()返回结果为UIAbilityContext
    3. let context = this.getUIContext().getHostContext() as common.UIAbilityContext;
    4. const documentViewPicker = new picker.DocumentViewPicker(context);
    5. const documentSaveOptions = new picker.DocumentSaveOptions();
    6. documentSaveOptions.pickerMode = picker.DocumentPickerMode.DOWNLOAD;
    7. documentViewPicker.save(documentSaveOptions).then((documentSaveResult: Array<string>) => {
    8.   uri = documentSaveResult[0];
    9.   console.info('documentViewPicker.save succeed and uri is:' + uri);
    10.   const testFilePath = new fileUri.FileUri(uri + '/test.txt').path;
    11.   const file = fs.openSync(testFilePath, fs.OpenMode.CREATE | fs.OpenMode.READ_WRITE);
    12.   fs.writeSync(file.fd, 'Hello World!');
    13.   fs.closeSync(file.fd);
    14. }).catch((err: BusinessError) => {
    15.   console.error(`Invoke documentViewPicker.save failed, code is ${err.code}, message is ${err.message}`);
    16. })
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/select-user-file "选择用户文件")
# 授权持久化

更新时间: 2025-12-16 16:39

## 场景介绍

应用通过Picker获取临时授权，临时授权在应用退出后或者设备重启后会清除。如果应用重启或者设备重启后需要直接访问之前已访问过的文件，则对文件进行持久化授权。

## 通过Picker获取临时授权并进行授权持久化

通过Picker选择文件或文件夹进行临时授权，然后应用可以按需通过文件分享接口（[ohos.fileshare](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-fileshare)）进行持久化授权。

1.应用仅临时需要访问公共目录的数据，例如：通讯类应用需要发送用户的文件或者图片。应用调用Picker的([select](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-file-picker#select-3))接口选择需要发送的文件或者图片，此时应用获取到是该文件的临时访问权限，应用重启或者设备重启后，再次访问该文件则仍需使用Picker进行文件选择。

2.应用如果需要长期访问某个文件或目录时，可以通过Picker选择文件或文件夹进行临时授权，然后利用persistPermission接口（[ohos.fileshare.persistPermission](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-fileshare#filesharepersistpermission11)）对授权进行持久化（在授权方同意被持久化的情况下），例如：文档编辑类应用本次编辑完一个用户文件，期望在历史记录中可以直接选中打开，无需再拉起Picker进行选择授权。

可使用canIUse接口，确认设备是否具有以下系统能力：SystemCapability.FileManagement.AppFileService.FolderAuthorization。

1. if (!canIUse('SystemCapability.FileManagement.AppFileService.FolderAuthorization')) {
2.     console.error('this api is not supported on this device');
3.     return;
4. }

**需要权限**

ohos.permission.FILE_ACCESS_PERSIST，具体参考[访问控制-申请应用权限](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/determine-application-mode)。

**示例：**

1. import { BusinessError } from '@kit.BasicServicesKit';
2. import { picker } from '@kit.CoreFileKit';
3. import { fileShare } from '@kit.CoreFileKit';

4. async function persistPermissionExample() {
5.     try {
6.         let DocumentSelectOptions = new picker.DocumentSelectOptions();
7.         let documentPicker = new picker.DocumentViewPicker();
8.         let uris = await documentPicker.select(DocumentSelectOptions);
9.         let policyInfo: fileShare.PolicyInfo = {
10.             uri: uris[0],
11.             operationMode: fileShare.OperationMode.READ_MODE,
12.         };
13.         let policies: Array<fileShare.PolicyInfo> = [policyInfo];
14.         fileShare.persistPermission(policies).then(() => {
15.             console.info("persistPermission successfully");
16.         }).catch((err: BusinessError<Array<fileShare.PolicyErrorResult>>) => {
17.             console.error("persistPermission failed with error message: " + err.message + ", error code: " + err.code);
18.             if (err.code == 13900001 && err.data) {
19.                 for (let i = 0; i < err.data.length; i++) {
20.                     console.error("error code : " + JSON.stringify(err.data[i].code));
21.                     console.error("error uri : " + JSON.stringify(err.data[i].uri));
22.                     console.error("error reason : " + JSON.stringify(err.data[i].message));
23.                 }
24.             }
25.         });
26.     } catch (error) {
27.         let err: BusinessError = error as BusinessError;
28.         console.error(`persistPermission failed with err, Error code: ${err.code}, message: ${err.message}`);
29.     }
30. }

注意

1. 持久化授权文件信息建议应用在本地存储数据，供后续按需激活持久化文件。
2. 持久化授权的数据存储在系统的数据库中，应用或者设备重启后需要激活已持久化的授权才可以正常使用[激活持久化授权](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/file-persistpermission#%E6%BF%80%E6%B4%BB%E5%B7%B2%E7%BB%8F%E6%8C%81%E4%B9%85%E5%8C%96%E7%9A%84%E6%9D%83%E9%99%90%E8%AE%BF%E9%97%AE%E6%96%87%E4%BB%B6%E6%88%96%E7%9B%AE%E5%BD%95)。
3. 持久化权限接口(可以使用canIUse接口进行校验能力是否可用)，且需要申请对应的权限。
4. 应用在卸载时会将之前的授权数据全部清除，重新安装后需要重新授权。

**备注**：C/C++持久化授权接口说明及开发指南具体参考：[OH_FileShare_PersistPermission持久化授权接口](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/native-fileshare-guidelines)。

3.可以通过revokePermission接口（[ohos.fileshare.revokePermission](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-fileshare#filesharerevokepermission11)）对已持久化的文件取消授权，同时更新应用存储的数据以删除最近访问数据。

**需要权限**

ohos.permission.FILE_ACCESS_PERSIST，具体参考[访问控制-申请应用权限](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/determine-application-mode)。

**示例：**

1. import { BusinessError } from '@kit.BasicServicesKit';
2. import { picker } from '@kit.CoreFileKit';
3. import { fileShare } from '@kit.CoreFileKit';

4. async function revokePermissionExample() {
5.     try {
6.         let uri = "file://docs/storage/Users/username/tmp.txt";
7.         let policyInfo: fileShare.PolicyInfo = {
8.             uri: uri,
9.             operationMode: fileShare.OperationMode.READ_MODE,
10.         };
11.         let policies: Array<fileShare.PolicyInfo> = [policyInfo];
12.         fileShare.revokePermission(policies).then(() => {
13.             console.info("revokePermission successfully");
14.         }).catch((err: BusinessError<Array<fileShare.PolicyErrorResult>>) => {
15.             console.error("revokePermission failed with error message: " + err.message + ", error code: " + err.code);
16.             if (err.code == 13900001 && err.data) {
17.                 for (let i = 0; i < err.data.length; i++) {
18.                     console.error("error code : " + JSON.stringify(err.data[i].code));
19.                     console.error("error uri : " + JSON.stringify(err.data[i].uri));
20.                     console.error("error reason : " + JSON.stringify(err.data[i].message));
21.                 }
22.             }
23.         });
24.     } catch (error) {
25.         let err: BusinessError = error as BusinessError;
26.         console.error(`revokePermission failed with err, Error code: ${err.code}, message: ${err.message}`);
27.     }
28. }

注意

1. 示例中的URI来源自应用存储的持久化数据中。
2. 建议按照使用需求去激活对应的持久化权限，不要盲目的全量激活。
3. 持久化权限接口(可以使用canIUse接口进行校验能力是否可用)，且需要申请对应的权限。

**备注**：C/C++去持久化授权接口说明及开发指南具体参考：[OH_FileShare_RevokePermission去持久化授权接口](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/native-fileshare-guidelines)。

## 激活已经持久化的权限访问文件或目录

对于应用已经持久化的授权，应用每次启动时实际未加载到内存中，需要应用按需进行手动激活已持久化授权的权限，通过activatePermission接口（[ohos.fileshare.activatePermission](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-fileshare#fileshareactivatepermission11)）对已经持久化授权的权限进行使能操作，否则已经持久化授权的权限仍存在不能使用的情况。

**需要权限**

ohos.permission.FILE_ACCESS_PERSIST，具体参考[访问控制-申请应用权限](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/determine-application-mode)。

**示例：**

1. import { BusinessError } from '@kit.BasicServicesKit';
2. import { picker } from '@kit.CoreFileKit';
3. import { fileShare } from '@kit.CoreFileKit';

4. async function activatePermissionExample() {
5.     try {
6.         let uri = "file://docs/storage/Users/username/tmp.txt";
7.         let policyInfo: fileShare.PolicyInfo = {
8.             uri: uri,
9.             operationMode: fileShare.OperationMode.READ_MODE,
10.         };
11.         let policies: Array<fileShare.PolicyInfo> = [policyInfo];
12.         fileShare.activatePermission(policies).then(() => {
13.             console.info("activatePermission successfully");
14.         }).catch((err: BusinessError<Array<fileShare.PolicyErrorResult>>) => {
15.             console.error("activatePermission failed with error message: " + err.message + ", error code: " + err.code);
16.             if (err.code == 13900001 && err.data) {
17.                 for (let i = 0; i < err.data.length; i++) {
18.                     console.error("error code : " + JSON.stringify(err.data[i].code));
19.                     console.error("error uri : " + JSON.stringify(err.data[i].uri));
20.                     console.error("error reason : " + JSON.stringify(err.data[i].message));
21.                     if (err.data[i].code == fileShare.PolicyErrorCode.PERMISSION_NOT_PERSISTED) {
22.                         //可以选择进行持久化后再激活。
23.                     }
24.                 }
25.             }
26.         });
27.     } catch (error) {
28.         let err: BusinessError = error as BusinessError;
29.         console.error(`activatePermission failed with err, Error code: ${err.code}, message: ${err.message}`);
30.     }
31. }

注意

1. 示例中的URI来源自应用存储的持久化数据中。
2. 建议按照使用需求去激活对应的持久化权限，不要盲目的全量激活。
3. 如果激活失败显示未持久化的权限可以按照示例进行持久化。
4. 持久化权限接口可以使用canIUse接口进行校验能力是否可用，且需要申请对应的权限。

**备注**：C/C++持久化授权激活接口说明及开发指南具体参考：[OH_FileShare_ActivatePermission持久化授权激活接口](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/native-fileshare-guidelines)。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/save-user-file "保存用户文件")