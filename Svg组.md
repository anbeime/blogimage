# 基础知识

更新时间: 2025-12-16 16:40

Svg组件主要作为svg画布的根节点使用，也可以在svg中嵌套使用。具体用法请参考[Svg](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-components-svg)。

说明

svg父组件或者svg组件需要定义宽高值，否则不进行绘制。

## 创建Svg组件

在pages/index目录下的hml文件中创建一个Svg组件。

1. <!-- xxx.hml -->
2. <div class="container">
3.   <svg width="400" height="400">  </svg>
4. </div>

5. /* xxx.css */
6. .container{
7.   width: 100%;
8.   height: 100%;
9.   flex-direction: column;
10.   align-items: center;
11.   justify-content: center;
12.   background-color: #F1F3F5;
13. }
14. svg{
15.   background-color: blue;
16. }

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216164017.43773120464241168588532894810374:50001231000000:2800:A72AE6D2D445E96FB742F98C0093EBA5F9816E1C77D534D3F2FEBE70EB0D8AC3.png)

## 设置属性

通过设置width、height、x、y和viewBox属性为Svg设置宽度、高度、x轴坐标、y轴坐标和Svg视口。

1. <!-- xxx.hml -->
2. <div class="container">
3.   <svg width="400" height="400" viewBox="0 0 100 100">    
4.     <svg class="rect" width="100" height="100" x="20" y="10">    
5.     </svg>  
6.   </svg>
7. </div>

8. /* xxx.css */
9. .container{
10.   width: 100%;
11.   height: 100%;
12.   flex-direction: column;
13.   align-items: center;
14.   justify-content: center;
15.   background-color: #F1F3F5;
16. }
17. svg{
18.   background-color: yellow;
19. }
20. .rect{
21.   background-color: red;
22. }

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216164017.78444484290148976361398622495190:50001231000000:2800:809C9799F3B314D29D773E64F6E4DADA30E384B56C35BEAD190D7BD89C3863FD.png)

说明

- x和y设置的是当前Svg的x轴和y轴坐标，如果当前Svg为根节点，x轴和y轴属性无效。
    
- viewBox的宽高和svg的宽高不一致，会以中心对齐进行缩放。
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-js-svg "Svg开发指导")
# 绘制图形

更新时间: 2025-12-16 16:40

Svg组件可以用来绘制常见图形和线段，如矩形（<rect>）、圆形（<circle>）、线条(<line>）等，具体支持图形样式还请参考[Svg](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-components-svg)组件。

在本场景中，绘制各种图形拼接成一个小房子。

1. <!-- xxx.hml -->
2. <div class="container">
3.   <svg width="1000" height="1000">
4.     <polygon points="100,400 300,200 500,400" fill="red"></polygon>     //屋顶
5.     <polygon points="375,275 375,225 425,225 425,325" fill="orange"></polygon>   //烟囱
6.     <rect width="300" height="300" x="150" y="400" fill="orange">      //房子
7.     </rect>
8.     <rect width="100" height="100" x="180" y="450" fill="white">    //窗户
9.     </rect>
10.     <line x1="180" x2="280" y1="500" y2="500" stroke-width="4" fill="white" stroke="black"></line>     //窗框
11.     <line x1="230" x2="230" y1="450" y2="550" stroke-width="4" fill="white" stroke="black"></line>     //窗框
12.     <polygon points="325,700 325,550 400,550 400,700" fill="red"></polygon>     //门
13.     <circle cx="380" cy="625" r="20" fill="black"></circle>      //门把手
14.   </svg>
15. </div>

16. /* xxx.css */
17. .container {
18.   width: 100%;
19.   height: 100%;
20.   flex-direction: column;
21.   justify-content: center;
22.   align-items: center;
23.   background-color: #F1F3F5;
24. }

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216164029.55389886033273897209778785439154:50001231000000:2800:D2DF32C9EABDC747797B7765503D95DEABA723973608AC1515AAC058A66AF4F8.png)

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-js-components-svg-overview "基础知识")
# 绘制路径

更新时间: 2025-12-16 16:40

[Svg](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-components-svg)组件绘制路径时，通过Path中的M（起点）、H（水平线）、a（绘制弧形到指定位置）路径控制指令，并填充颜色实现饼状图效果。

1. <!-- xxx.hml -->
2. <div class="container">
3.   <svg fill="#00FF00" x="100" y="400">
4.     <path d="M300,200 h-150 a150 150 0 1 0 150 -150 z" fill="red" stroke="blue" stroke-width="5" >    
5.     </path> 
6.     <path d="M275,175 v-150 a150 150 0 0 0 -150 150 z" fill="yellow" stroke="blue" stroke-width="5">    
7.     </path>
8.   </svg>
9. </div>

10. /* xxx.css */
11. .container {
12.   flex-direction: row;
13.   justify-content: flex-start;
14.   align-items: flex-start;
15.   height: 1200px;
16.   width: 600px;
17.   background-color: #F1F3F5;
18. }

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216164042.58910930953993230153234020756355:50001231000000:2800:E22F7FCBC1071667EAC9F317A240232FD0C4B3BC9C334B73C115B85577C48CF6.png)

说明

- M/m = moveto 参数x和y表示需要移动到点的x轴和y轴的坐标。在使用M命令移动画笔后，只会移动画笔，但不会在两点之间画线。所以M命令经常出现在路径的开始处，用来指明从何处开始画。
    
- L/l = lineto 参数x和y表示一个点的x轴和y轴坐标，L命令将会在当前位置和新位置（L前面画笔所在的点）之间画一条线段。
    
- H/h = horizontal lineto 绘制平行线。
    
- V/v = vertical lineto 绘制垂直线。
    
- C/c = curveto 三次贝塞尔曲线 设置三组坐标参数： x1 y1, x2 y2, x y。
    
- S/s = smooth curveto 三次贝塞尔曲线命令 设置两组坐标参数： x2 y2, x y。
    
- Q/q = quadratic Belzier curve 二次贝塞尔曲线 设置两组坐标参数： x1 y1, x y。
    
- T/t = smooth quadratic Belzier curveto 二次贝塞尔曲线命令 设置参数： x y。
    
- A/a = elliptical Arc 弧形命令 设置参数： rx ry x-axis-rotation（旋转角度）large-arc-flag（角度大小） sweep-flag（弧线方向） x y。large-arc-flag决定弧线是大于还是小于180度，0表示小角度弧，1表示大角度弧。sweep-flag表示弧线的方向，0表示从起点到终点沿逆时针画弧，1表示从起点到终点沿顺时针画弧。
    
- Z/z = closepath 从当前点画一条直线到路径的起点。
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-js-components-svg-graphics "绘制图形")
# 绘制文本

更新时间: 2025-12-16 16:40

Svg组件还可以绘制文本。

## 文本

说明

- 文本的展示内容需要写在元素标签text内，可嵌套tspan子元素标签分段。
    
- 只支持被父元素标签svg嵌套。
    
- 只支持默认字体sans-serif。
    

通过设置x（x轴坐标）、y（y轴坐标）、dx（文本x轴偏移）、dy（文本y轴偏移）、fill（字体填充颜色）、stroke（文本边框颜色）、stroke-width（文本边框宽度）等属性实现文本的不同展示样式。

1. <!-- xxx.hml -->
2. <div class="container">
3.   <svg>
4.     <text x="200" y="300" font-size="80px" fill="blue" >Hello World</text>    <text x="200" y="300" dx="20" dy="80" font-size="80px" fill="blue" fill-opacity="0.5" stroke="red" stroke-width="2">Hello World</text>
5.     <text x="20" y="550" fill="#D2691E">
6.       <tspan dx="40" fill="red" font-size="80" fill-opacity="0.4">Hello World </tspan>
7.     </text>
8.   </svg>
9. </div>

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216164049.99609974250677896839100774143690:50001231000000:2800:5A3BBE712C57000FBCBD46B4FDA2ADD01093C9F23F30FCE54B468C824C4FA45F.png)

## 沿路径绘制文本

textpath文本内容沿着属性path中的路径绘制文本。

1. <!-- xxx.hml -->
2. <div class="container">
3.   <svg fill="#00FF00" x="100" y="400">
4.     <path d="M40,360 Q360,360 360,180 Q360,20 200,20 Q40,40 40,160 Q40,280 180,180 Q180,180 200,100" stroke="red" fill="none"></path>
5.       <text>
6.         <textpath fill="blue" startOffset="20%" path="M40,360 Q360,360 360,180 Q360,20 200,20 Q40,40 40,160 Q40,280 180,180 Q180,180 200,100" font-size="30px">
7.           This is textpath test.
8.         </textpath>
9.       </text>
10.   </svg>
11. </div>

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216164050.48968329843273891752619343704619:50001231000000:2800:3765670FB702A357056020551F382698DEA26ADDC20523E8EA2FD4BC0BB7BF1A.png)

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-js-components-svg-path "绘制路径")
