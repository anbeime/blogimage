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
# 属性样式动画

更新时间: 2025-12-16 16:40

在关键帧（Keyframes）中动态设置父组件的width和height，实现组件变大缩小。子组件设置scale属性使父子组件同时缩放，再设置opacity实现父子组件的显示与隐藏。

1. <!-- xxx.hml -->
2. <div class="container">
3.   <div class="fade">
4.     <text>fading away</text>
5.   </div>
6.   <div class="bigger">
7.     <text>getting bigger</text>
8.   </div>
9. </div>

10. /* xxx.css */
11. .container {
12.   background-color:#F1F3F5;
13.   display: flex;
14.   justify-content: center;
15.   align-items: center;
16.   flex-direction: column;
17.   width: 100%;
18.   height: 100%;
19. }
20. .fade {
21.   width: 30%;
22.   height: 200px;
23.   left: 35%;
24.   top: 25%;
25.   position: absolute;
26.   animation: 2s change infinite friction;
27. }
28. .bigger {
29.   width: 20%;
30.   height: 100px;
31.   background-color: blue;
32.   animation: 2s change1 infinite linear-out-slow-in;
33. }
34. text {
35.   width: 100%;
36.   height: 100%;
37.   text-align: center;
38.   color: white;
39.   font-size: 35px;
40.   animation: 2s change2 infinite linear-out-slow-in;
41. }
42. /* 颜色变化 */
43. @keyframes change{
44.   from {
45.     background-color: #f76160;
46.     opacity: 1;
47.   }
48.   to {
49.     background-color: #09ba07;
50.     opacity: 0;
51.   }
52. }
53. /* 父组件大小变化 */
54. @keyframes change1 {
55.   0% {
56.     width: 20%;
57.     height: 100px;
58.   }
59.   100% {
60.     width: 80%;
61.     height: 200px;
62.   }
63. }
64. /* 子组件文字缩放 */
65. @keyframes change2 {
66.   0% {
67.     transform: scale(0);
68.   }
69.   100% {
70.     transform: scale(1.5);
71.   }
72. }

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216164017.38682061437818179726821012719433:50001231000000:2800:31099267538D8FA8426C1B517E18EC03EBBE1E0FC9FFBE768904F0CD5C41C1B8.gif)

说明

- animation取值不区分先后，duration （动画执行时间）/ delay （动画延迟执行时间）按照出现的先后顺序解析。
    
- 必须设置animation-duration样式，否则时长为0则不会有动画效果。当设置animation-fill-mode属性为forwards时，组件直接展示最后一帧的样式。
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-js-animation-css "CSS动画")
# transform样式动画

更新时间: 2025-12-16 16:40

设置transform属性对组件进行旋转、缩放、移动和倾斜。

## 设置静态动画

创建一个正方形并旋转90°变成菱形，并用下方的长方形把菱形下半部分遮盖形成屋顶，设置长方形translate属性值为(150px,-150px)确定坐标位置形成门，再使用position属性使横纵线跟随父组件（正方形）移动到指定坐标位置，接着设置scale属性使父子组件一起变大形成窗户大小，最后使用skewX属性使组件倾斜后设置坐标translate(200px,-710px)得到烟囱。

1. <!-- xxx.hml -->
2. <div class="container">
3.   <div class="top"></div>
4.   <div class="content"></div>
5.   <div class="door"></div>
6.   <!-- 窗户 -->
7.   <div class="window">
8.     <div class="horizontal"></div>
9.     <div class="vertical"></div>
10.   </div>
11.   <div class="chimney"></div>
12. </div>

13. /* xxx.css */
14. .container {
15.   width:100%;
16.   height:100%;
17.   background-color:#F1F3F5;
18.   align-items: center;
19.   flex-direction: column;
20. }
21. .top{
22.   z-index: -1;
23.   position: absolute;
24.   width: 428px;
25.   height: 428px;
26.   background-color: #860303;
27.   transform: rotate(45deg);
28.   margin-top: 284px;
29.   margin-left: 148px;
30. }
31. .content{
32.   margin-top: 500px;
33.   width: 600px;
34.   height: 400px;
35.   background-color: white;
36.   border:  1px solid black;
37. }
38. .door{
39.   width: 100px;
40.   height: 135px;
41.   background-color: #1033d9;
42.   transform: translate(150px,-137px);
43. }
44. .window{
45.   z-index: 1;
46.   position: relative;
47.   width: 100px;
48.   height: 100px;
49.   background-color: white;
50.   border: 1px solid black;
51.   transform: translate(-150px,-400px) scale(1.5);
52. }
53. /* 窗户的横轴 */
54. .horizontal{
55.   position: absolute;
56.   top: 50%;
57.   width: 100px;
58.   height: 5px;
59.   background-color: black;
60. }
61. /* 窗户的纵轴 */
62. .vertical{
63.   position: absolute;
64.   left: 50%;
65.   width: 5px;
66.   height: 100px;
67.   background-color: black;
68. }
69. .chimney{
70.   z-index: -2;
71.   width: 40px;
72.   height: 100px;
73.   border-radius: 15px;
74.   background-color: #9a7404;
75.   transform: translate(200px,-710px) skewX(-5deg);
76. }

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216164030.95294099872391676080216063364431:50001231000000:2800:7F742C6BABEAE1768819F5D8D49D95F6CC5DFD9BBD4A1B54F254B865A9FBC5AE.png)

## 设置平移动画

小球下降动画，改变小球的Y轴坐标实现小球下落，在下一段时间内减小Y轴坐标实现小球回弹，让每次回弹的高度逐次减小直至回弹高度为0，就模拟出了小球下降的动画。

1. <!-- xxx.hml -->
2. <div class="container">
3.   <div class="circle"></div>
4.   <div class="flower"></div>
5. </div>

6. /* xxx.css */
7. .container {
8.   width:100%;
9.   height:100%;
10.   background-color:#F1F3F5;
11.   display: flex;
12.   justify-content: center;
13. }
14. .circle{
15.   width: 100px;
16.   height: 100px;
17.   border-radius: 50px;
18.   background-color: red;
19.   /* forwards停在动画的最后一帧 */
20.   animation: down 3s fast-out-linear-in forwards;
21. }
22. .flower{
23.   position: fixed;
24.   width: 80%;
25.   margin-left: 10%;
26.   height: 5px;
27.   background-color: black;
28.   top: 1000px;
29. }
30. @keyframes down {
31.   0%{
32.     transform: translate(0px,0px);
33.   }
34.   /* 下落 */
35.   15%{
36.     transform: translate(10px,900px);
37.   }
38.   /* 开始回弹 */
39.   25%{
40.     transform: translate(20px,500px);
41.   }
42.   /* 下落 */
43.   35%{
44.     transform: translate(30px,900px);
45.   }
46.   /* 回弹 */
47.   45%{
48.     transform: translate(40px,700px);
49.   }
50.   55%{
51.     transform: translate(50px,900px);
52.   }
53.   65%{
54.     transform: translate(60px,800px);
55.   }
56.   80%{
57.     transform: translate(70px,900px);
58.   }
59.   90%{
60.     transform: translate(80px,850px);
61.   }
62.   /* 停止 */
63.   100%{
64.     transform: translate(90px,900px);
65.   }
66. }

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216164030.88357307432888156772262184011135:50001231000000:2800:25A5CC0FA8709B668AA4963D654A28D1F24379E8114B3B1AA6445AC811E9D2CD.gif)

## 设置旋转动画

设置不同的原点位置（transform-origin）改变元素所围绕的旋转中心。rotate3d属性前三个参数值分别为X轴、Y轴、Z轴的旋转向量，第四个值为旋转角度，旋转角度可为负值，负值则代表旋转方向为逆时针方向。

1. <!-- xxx.hml -->
2. <div class="container">
3.   <div class="rotate">
4.     <div class="rect rect1"></div>
5.     <div class="rect rect2"></div>
6.     <div class="rect rect3"></div>
7.   </div>
8.   <!-- 3d属性 -->
9.   <div class="rotate3d">
10.     <div class="content">
11.         <div class="rect4"></div>
12.         <div class="rect5"> </div>
13.     </div>
14.     <div class="mouse"></div>
15.   </div>
16. </div>

17. /* xxx.css */
18. .container {
19.     flex-direction: column;
20.     background-color:#F1F3F5;
21.     display: flex;
22.     align-items: center;
23.     justify-content: center;
24.     width: 100%;
25.     height: 100%;
26. }
27. .rect {
28.     width: 100px;
29.     height: 100px;
30.     animation: rotate 3s infinite;
31.     margin-left: 30px;
32. }
33. .rect1 {
34.     background-color: #f76160;
35. }
36. .rect2 {
37.     background-color: #60f76f;
38. /* 改变原点位置*/
39.     transform-origin: 10% 10px;
40. }
41. .rect3 {
42.     background-color: #6081f7;
43. /*  改变原点位置*/
44.     transform-origin: right bottom;
45. }
46. @keyframes rotate {
47.     from {
48.         transform: rotate(0deg)
49.     }
50.     to {
51.         transform: rotate(360deg);
52.     }
53. }
54. /* 3d示例样式 */
55. .rotate3d {
56.     margin-top: 150px;
57.     flex-direction: column;
58.     background-color:#F1F3F5;
59.     display: flex;
60.     align-items: center;
61.     width: 80%;
62.     height: 600px;
63.     border-radius: 300px;
64.     border: 1px solid #ec0808;
65. }
66. .content {
67.     padding-top: 150px;
68.     display: flex;
69.     align-items: center;
70.     justify-content: center;
71. }
72. /* rect4 rect5 翻转形成眼睛 */
73. .rect4 {
74.     width: 100px;
75.     height: 100px;
76.     animation: rotate3d1 1000ms infinite;
77.     background-color: darkmagenta;
78. }
79. .rect5 {
80.     width: 100px;
81.     height: 100px;
82.     animation: rotate3d1 1000ms infinite;
83.     margin-left: 100px;
84.     background-color: darkmagenta;
85. }
86. .mouse {
87.     margin-top: 150px;
88.     width: 200px;
89.     height: 100px;
90.     border-radius: 50px;
91.     border: 1px solid #e70303;
92.     animation: rotate3d2 1000ms infinite;
93. }
94. /* 眼睛的动效 */
95. @keyframes rotate3d1 {
96.     0% {
97.         transform:rotate3d(0,0,0,0deg)
98.     }
99.     50% {
100.         transform:rotate3d(20,20,20,360deg);
101.     }
102.     100% {
103.         transform:rotate3d(0,0,0,0deg);
104.     }
105. }
106. /* 嘴的动效 */
107. @keyframes rotate3d2 {
108.     0% {
109.         transform:rotate3d(0,0,0,0deg)
110.     }
111.     33% {
112.         transform:rotate3d(0,0,10,30deg);
113.     }
114.     66% {
115.         transform:rotate3d(0,0,10,-30deg);
116.     }
117.     100% {
118.         transform:rotate3d(0,0,0,0deg);
119.     }
120. }

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216164030.57941332452692958067760026045882:50001231000000:2800:08E75EEE359C8D53D0E30B3413B6CE01DE4EF9DB56AB68E9A7F320B3B5364A90.gif)

说明

transform-origin变换对象的原点位置，如果仅设置一个值，另一个值为50%，若设置两个值第一个值表示X轴的位置，第二个值表示Y轴的位置。

## 设置缩放动画

设置scale样式属性实现涟漪动画，先使用定位确定元素的位置，确定坐标后创建多个组件实现重合效果，再设置opacity属性改变组件不透明度实现组件隐藏与显示，同时设置scale值使组件可以一边放大一边隐藏，最后设置两个组件不同的动画执行时间，实现扩散的效果。

设置scale3d中X轴、Y轴、Z轴的缩放参数实现动画。

1. <!-- xxx.hml -->
2. <div class="container">
3.   <div class="circle">
4.     <text>ripple</text>
5.   </div>
6.   <div class="ripple"></div>
7.   <div class="ripple ripple2"></div>
8.   <!-- 3d -->
9.   <div class="content">
10.     <text>spring</text>
11.   </div>
12. </div>

13. /* xxx.css */
14. .container {
15.     flex-direction: column;
16.     background-color:#F1F3F5;
17.     width: 100%;
18.     position: relative;
19. }
20. .circle{
21.     margin-top: 400px;
22.     margin-left: 40%;
23.     width: 100px;
24.     height: 100px;
25.     border-radius: 50px;
26.     background-color: mediumpurple;
27.     z-index: 1;  position: absolute;
28. }
29. .ripple{
30.     margin-top: 400px;
31.     margin-left: 40%;
32.     position: absolute; z-index: 0;
33.     width: 100px;
34.     height: 100px;
35.     border-radius: 50px;
36.     background-color: blueviolet;
37.     animation: ripple 5s infinite;
38. }
39. /* 设置不同的动画时间 */
40. .ripple2{
41.     animation-duration: 2.5s;
42. }
43. @keyframes ripple{
44.     0%{
45.         transform: scale(1);
46.         opacity: 0.5;
47.     }
48.     50%{
49.         transform: scale(3);
50.         opacity: 0;
51.     }
52.     100%{
53.         transform: scale(1);
54.         opacity: 0.5;
55.     }
56. }
57. text{
58.     color: white;
59.     text-align: center;
60.     height: 100%;
61.     width: 100%;
62. }
63. .content {
64.     margin-top: 700px;
65.     margin-left: 33%;
66.     width: 200px;
67.     height: 100px;
68.     animation:rubberBand 1s infinite;
69.     background-color: darkmagenta;
70.     position: absolute;
71. }
72. @keyframes rubberBand {
73.     0% {
74.         transform: scale3d(1, 1, 1);
75.     }
76.     30% {
77.         transform: scale3d(1.25, 0.75, 1.1);
78.     }
79.     40% {
80.         transform: scale3d(0.75, 1.25, 1.2);
81.     }
82.     50% {
83.         transform: scale3d(1.15, 0.85, 1.3);
84.     }
85.     65% {
86.         transform: scale3d(.95, 1.05, 1.2);
87.     }
88.     75% {
89.         transform: scale3d(1.05, .95, 1.1);
90.     }
91.     100%{
92.         transform: scale3d(1, 1, 1);
93.     }
94. }

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216164030.67314812843609376606634165142049:50001231000000:2800:932A28D6E610F7E9D16D73D982959CC096B0CFA1C37D646E319E0268891A83B3.gif)

说明

设置transform属性值后，子元素会跟着父元素一起改变，若只改变父元素其他属性值时（如：height，width），子元素不会改变。

## 设置matrix属性

matrix是一个入参为六个值的矩阵，6个值分别代表：scaleX, skewY, skewX, scaleY, translateX, translateY。下面示例中设置了matrix属性为matrix(1,0,0,1,0,200)使组件移动和倾斜。

1. <!-- xxx.hml -->
2. <div class="container">
3.   <div class="rect"> </div>
4. </div>

5. /* xxx.css */
6. .container{
7.   background-color:#F1F3F5;
8.   display: flex;
9.   justify-content: center;
10.   width: 100%;
11.   height: 100%;
12. }
13. .rect{
14.   width: 100px;
15.   height: 100px;
16.   background-color: red;
17.   animation: down 3s infinite forwards;
18. }
19. @keyframes down{
20.   0%{
21.     transform: matrix(1,0,0,1,0,0);
22.   }
23.   10%{
24.     transform: matrix(1,0,0,1,0,200);
25.   }
26.   60%{
27.     transform: matrix(2,1.5,1.5,2,0,700);
28.   }
29.   100%{
30.     transform: matrix(1,0,0,1,0,0);
31.   }
32. }

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216164030.25014797515925241741202220393691:50001231000000:2800:088A61360B8FEC8922D7DE73885EC497B224DB389BA91DBBD8C4ED9505A8100E.gif)

## 整合transform属性

transform可以设置多个值并且多个值可同时设置，下面案例中展示同时设置缩放（scale），平移（translate），旋转（rotate）属性时的动画效果。

1. <!-- xxx.hml -->
2. <div class="container">
3.   <div class="rect1"></div>
4.   <div class="rect2"></div>
5.   <div class="rect3"></div>
6.   <div class="rect4"></div>
7.   <div class="rect5"></div>
8. </div>

9. /* xxx.css */
10. .container{
11.     width: 100%;
12.     height: 100%;
13.     flex-direction:column;
14.     background-color:#F1F3F5;
15.     padding:50px;
16. }
17. .rect1{
18.     width: 100px;
19.     height: 100px;
20.     background-color: red;
21.     animation: change1 3s infinite forwards;
22. }
23. .rect2{
24.     margin-top: 50px;
25.     width: 100px;
26.     height: 100px;
27.     background-color: darkblue;
28.     animation: change2 3s infinite forwards;
29. }
30. .rect3{
31.     margin-top: 50px;
32.     width: 100px;
33.     height: 100px;
34.     background-color: darkblue;
35.     animation: change3 3s infinite;
36. }
37. .rect4{
38.     align-self: center;
39.     margin-left: 50px;
40.     margin-top: 200px;
41.     width: 100px;
42.     height: 100px;
43.     background-color: darkmagenta;
44.     animation: change4 3s infinite;
45. }
46. .rect5{
47.     margin-top: 300px;
48.     width: 100px;
49.     height: 100px;
50.    background-color: cadetblue;
51.     animation: change5 3s infinite;
52. }
53. /* change1 change2 对比 */
54. @keyframes change1{
55.     0%{
56.         transform: translate(0,0);    transform: rotate(0deg)
57.     }
58.     100%{
59.         transform: translate(0,500px);
60.         transform: rotate(360deg)
61.     }
62. }
63. /* change2 change3 对比属性顺序不同的动画效果 */
64. @keyframes change2{
65.     0%{
66.         transform:translate(0,0) rotate(0deg) ;
67.     }
68.     100%{
69.         transform: translate(300px,0) rotate(360deg);
70.     }
71. }
72. @keyframes change3{
73.     0%{
74.         transform:rotate(0deg) translate(0,0);
75.     }
76.     100%{
77.         transform:rotate(360deg)  translate(300px,0);
78.     }
79. }
80. /* 属性值不对应的情况 */
81. @keyframes change4{
82.     0%{
83.         transform: scale(0.5);
84.     }
85.     100%{
86.         transform:scale(2) rotate(45deg);
87.     }
88. }
89. /* 多属性的写法 */
90. @keyframes change5{
91.     0%{
92.         transform:scale(0) translate(0,0) rotate(0);
93.     }
94.     100%{
95.         transform: scale(1.5) rotate(360deg) translate(200px,0);
96.     }
97. }

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216164030.56027069556034139868122413891822:50001231000000:2800:D4BC9A22A5D8E69B488D41E81F642B63EDFDEAE3DD30D3EA767559E81BE949B9.gif)

说明

- 当设置多个transform时，后续的transform值会把前面的覆盖掉。若想同时使用多个动画样式可用复合写法，例：transform: scale(1) rotate(0) translate(0,0)。
    
- transform进行复合写法时，变化样式内多个样式值顺序的不同会呈现不一样的动画效果。
    
- transform属性设置的样式值要一一对应，若前后不对应，则该动画不生效。若设置多个样式值则只会呈现出已对应值的动画效果。
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-js-animate-attribute-style "属性样式动画")
# background-position样式动画

更新时间: 2025-12-16 16:40

通过改变background-position属性（第一个值为X轴的位置，第二个值为Y轴的位置）移动背景图片位置，若背景图位置超出组件则超出部分的背景图不显示。

1. <!-- xxx.hml -->
2. <div class="container">
3.   <div class="content"></div>
4.   <div class="content1"></div>
5. </div>

6. /* xxx.css */
7. .container {
8.   height: 100%;
9.   background-color:#F1F3F5;
10.   display: flex;
11.   flex-direction: column;
12.   justify-content: center;
13.   align-items: center;
14.   width: 100%;
15. }
16. .content{
17.   width: 400px;
18.   height: 400px;
19.   /* 不建议图片长宽比为1:1 */
20.   background-image: url('common/images/bg-tv.jpg');
21.   background-size: 100%;
22.   background-repeat: no-repeat;
23.   animation: change 3s infinite;
24.   border: 1px solid black;
25. }
26. .content1{
27.   margin-top:50px;
28.   width: 400px;
29.   height: 400px;
30.   background-image: url('common/images/bg-tv.jpg');
31.   background-size: 50%;
32.   background-repeat: no-repeat;
33.   animation: change1 5s infinite;
34.   border: 1px solid black;
35. }
36. /* 背景图片移动出组件 */
37. @keyframes change{
38.   0%{
39.     background-position:0px top;
40.   }
41.   25%{
42.     background-position:400px top;
43.   }
44.   50%{
45.     background-position:0px top;
46.   }
47.   75%{
48.     background-position:0px bottom;
49.   }
50.   100%{
51.     background-position:0px top;
52.   }
53. }
54. /* 背景图片在组件内移动 */
55. @keyframes change1{
56.   0%{
57.     background-position:left top;
58.   }
59.   25%{
60.     background-position:50% 50%;
61.   }
62.   50%{
63.     background-position:right bottom;
64.   }
65.   100%{
66.     background-position:left top;
67.   }
68. }

说明

background-position仅支持背景图片的移动，不支持背景颜色（background-color）。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216164042.79575244963770496177893082739453:50001231000000:2800:308BE67A5B23F7C02925DC02EB6A3DB32C30A7F04238A31751EDDAA124923551.gif)

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-js-animate-transform "transform样式动画")
# svg动画

更新时间: 2025-12-16 16:40

为svg组件添加动画效果。

## 属性样式动画

在svg的子组件[animate](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-components-svg-animate)中，通过attributeName设置需要进行动效的属性，from设置开始值，to设置结束值。

1. <!-- xxx.hml -->
2. <div class="container">
3.   <svg>
4.     <text x="300" y="300" fill="blue">
5.       Hello
6.       <animate attributeName="font-size" from="30" to="60" dur="3s" repeatCount="indefinite">
7.       </animate>
8.       <animate attributeName="fill" from="red" to="blue" dur="3s" repeatCount="indefinite">
9.       </animate>
10.       <animate attributeName="opacity" from="1" to="0.3" dur="3s" repeatCount="indefinite">
11.       </animate>
12.     </text>
13.     <text x="300" y="600" fill="blue">
14.       World
15.       <animate attributeName="font-size" from="30" to="60" values="30;80" dur="3s" repeatCount="indefinite">
16.       </animate>
17.       <animate attributeName="fill" from="red" to="blue"  dur="3s" repeatCount="indefinite">
18.       </animate>
19.       <animate attributeName="opacity" from="0.3" to="1" dur="3s" repeatCount="indefinite">
20.       </animate>
21.     </text>
22.   </svg>
23. </div>

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216164050.12626481279268028276390131326316:50001231000000:2800:6752FCE812F211C9F962EE1B192285FB98C191E9EA73B6C137AF09892D92C3C5.gif)

说明

在设置动画变化值时，如果已经设置了values属性，则from和to都失效。

## 路径动画

在svg的子组件[animateMotion](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-components-svg-animatemotion)中，通过path设置动画变化的路径。

1. <!-- xxx.hml -->
2. <div class="container">
3.   <svg fill="white" width="800" height="900">
4.     <path d="M300,200 h-150 a150 150 0 1 0 150 -150 z" fill="white" stroke="blue" stroke-width="5" >
5.     </path>
6.     <path fill="red" d="M-5,-5 L10,0 L-5,5 L0,0 Z"  >
7.       <animateMotion dur="2000" repeatCount="indefinite" rotate="auto-reverse"path="M300,200 h-150 a150 150 0 1 0 150 -150 z">
8.       </animateMotion>
9.     </path>
10.   </svg>
11. </div>

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216164050.55666303170129210827621742879975:50001231000000:2800:206A3E4B0BC4E9ADF59C35B88540E6FC9CAC81F003DBBDAF0424D9191EFEA492.gif)

## animateTransform动画

在svg的子组件[animateTransform](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-components-svg-animatetransform)中，通过attributeName绑定transform属性，type设置动画类型，from设置开始值，to设置结束值。

1. <!-- xxx.hml -->
2. <div class="container" style="">
3.   <svg>
4.     <line x1="90" y1="300" x2="90" y2="730" stroke-width="10" stroke="black" stroke-linecap="round">
5.       <animateTransform attributeName="transform" attributeType="XML" type="translate"  dur="3s" values="0;30;10;30;20;30;25;30" keyTimes="0;0.3;0.5;0.7;0.8;0.9;1.0;1.1"
6.       fill="freeze">
7.       </animateTransform>
8.     </line>
9.     <circle cx="500" cy="500" r="50" stroke-width="15" fill="red" stroke="#e70d0d">
10.       <animateTransform attributeName="transform" attributeType="XML" type="rotate"  dur="3s" values="0;30;10;30;20;30;25;30" keyTimes="0;0.3;0.5;0.7;0.8;0.9;1.0;1.1" fill="freeze">
11.       </animateTransform>
12.       <animateTransform attributeName="transform" attributeType="XML" type="scale"  dur="6s" values="1;1;1.3" keyTimes="0;0.5;1" fill="freeze"></animateTransform>
13.       <animateTransform attributeName="transform" attributeType="XML" type="translate"  dur="9s" values="0;0;300 7" keyTimes="0;0.6;0.9" fill="freeze"></animateTransform>
14.     </circle>
15.     <rect width="500" height="200" x="90" y="840">
16.       <animateTransform attributeName="transform" attributeType="XML" type="skewY"  dur="6s" values="0;0;30" keyTimes="0;0.5;1" fill="freeze"></animateTransform>
17.     </rect>
18.     <line x1="650" y1="300" x2="650" y2="600" stroke-width="20" stroke="blue" stroke-linecap="round">
19.       <animateTransform attributeName="transform" attributeType="XML" type="translate"  dur="9s" values="0;0;0 800" keyTimes="0;0.6;1" fill="freeze"></animateTransform>
20.     </line>
21.   </svg>
22. </div>

23. /* xxx.css */
24. .container {
25.   flex-direction: column;
26.   align-items: center;
27.   width: 100%;
28.   height: 100%;
29.   background-color: #F1F3F5;
30. }

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216164050.14051380145716846494966027025582:50001231000000:2800:22CC3AC14A6B3DB39CE262211E0809A3327E15219DAE077E850C14A8FE1FA118.gif)

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-js-animate-background-position-style "background-position样式动画")
# 组件动画

更新时间: 2025-12-16 16:40

在组件上创建和运行动画的快捷方式。具体用法请参考[通用方法](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-components-common-methods)。

## 获取动画对象

通过调用animate方法获得animation对象，animation对象支持动画属性、动画方法和动画事件。

1. <!-- xxx.hml -->
2. <div class="container">
3.   <div id="content" class="box" onclick="Show"></div>
4. </div>

5. /* xxx.css */
6. .container {
7.   flex-direction: column;
8.   justify-content: center;
9.   align-items: center;
10.   width: 100%;
11. }
12. .box{
13.   width: 200px;
14.   height: 200px;
15.   background-color: #ff0000;
16.   margin-top: 30px;
17. }

18. /* xxx.js */
19. export default {
20.     data: {
21.         animation: '',
22.         options: {},
23.         frames: {}
24.     },
25.     onInit() {
26.         this.options = {
27.             duration: 1500,
28.         };
29.         this.frames = [
30.             {
31.                 width: 200, height: 200,
32.             },
33.             {
34.                 width: 300, height: 300,
35.             }
36.         ];
37.     },
38.     Show() {
39.         this.animation = this.$element('content').animate(this.frames, this.options); //获取动画对象
40.         this.animation.play();
41.     }
42. }

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216164017.16807682729339196326572677251477:50001231000000:2800:9777EDFF64A35B932798033BE7806CFA42AA4861A066BBFC6C9AB72F7F34C4F8.gif)

说明

- 使用animate方法时必须传入Keyframes和Options参数。
- 多次调用animate方法时，采用replace策略，即最后一次调用时传入的参数生效。

## 设置动画参数

在获取动画对象后，通过设置参数Keyframes设置动画在组件上的样式。

1. <!-- xxx.hml -->
2. <div class="container">
3.    <div id="content" class="box" onclick="Show"></div>
4. </div>

5. /* xxx.css */
6. .container {
7.   flex-direction: column;
8.   justify-content: center;
9.   align-items: center;
10.   width: 100%;
11.   height: 100%;
12. }
13. .box{
14.   width: 200px;
15.   height: 200px;
16.   background-color: #ff0000;
17.   margin-top: 30px;
18. }

19. /* xxx.js */
20. export default {
21.   data: {
22.     animation: '',
23.     keyframes:{},
24.     options:{}
25.   },
26.   onInit() {
27.     this.options = {
28.       duration: 4000,
29.     }
30.     this.keyframes = [
31.     {
32.       transform: {
33.         translate: '-120px -0px',
34.         scale: 1,
35.         rotate: 0
36.         },
37.         transformOrigin: '100px 100px',
38.         offset: 0.0,
39.         width: 200,
40.         height: 200
41.       },
42.       {
43.         transform: {
44.           translate: '120px 0px',
45.           scale: 1.5,
46.           rotate: 90
47.           },
48.           transformOrigin: '100px 100px',
49.           offset: 1.0,
50.           width: 300,
51.           height: 300
52.       }
53.     ]
54.   },
55.   Show() {
56.     this.animation = this.$element('content').animate(this.keyframes, this.options)
57.     this.animation.play()
58.   }
59. }

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216164017.31348630466825361732327993293850:50001231000000:2800:2CC8FCB1E9A9CBB52741670841BBF360D45B97BCDA9E2D0AD1B5E062AE027B65.gif)

说明

- translate、scale和rotate的先后顺序会影响动画效果。
    
- transformOrigin只对scale和rotate起作用。
    

在获取动画对象后，通过设置参数Options来设置动画的属性。

1. <!-- xxx.hml -->
2. <div class="container">
3.    <div id="content" class="box" onclick="Show"></div>
4. </div>

5. /* xxx.css */
6. .container {
7.   flex-direction: column;
8.   justify-content: center;
9.   align-items: center;
10.   width: 100%;
11. }
12. .box{
13.   width: 200px;
14.   height: 200px;
15.   background-color: #ff0000;
16.   margin-top: 30px;
17. }

18. /* xxx.js */
19. export default {
20.     data: {
21.         animation: '',
22.         options: {},
23.         frames: {}
24.     },
25.     onInit() {
26.         this.options = {
27.             duration: 1500,
28.             easing: 'ease-in',
29.             delay: 5,
30.             iterations: 2,
31.             direction: 'normal',
32.         };
33.         this.frames = [
34.             {
35.                 transform: {
36.                     translate: '-150px -0px'
37.                 }
38.             },
39.             {
40.                 transform: {
41.                     translate: '150px 0px'
42.                 }
43.             }
44.         ];
45.     },
46.     Show() {
47.         this.animation = this.$element('content').animate(this.frames, this.options);
48.         this.animation.play();
49.     }
50. }

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216164017.60719559727058532387578364227244:50001231000000:2800:3058488552E7A32D3894B9B566A02B34B875A47B8F11A41FE7B0CF022FAC3775.gif)

说明

direction：指定动画的播放模式。

normal： 动画正向循环播放。

reverse： 动画反向循环播放。

alternate：动画交替循环播放，奇数次正向播放，偶数次反向播放。

alternate-reverse：动画反向交替循环播放，奇数次反向播放，偶数次正向播放。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-js-animation-js "JS动画")
# 动画动效

更新时间: 2025-12-16 16:41

通过设置插值器来实现动画效果。

## 创建动画对象

通过createAnimator创建一个动画对象，通过设置参数options来设置动画的属性。

1. <!-- xxx.hml -->
2. <div class="container">
3.   <div style="width: 300px;height: 300px;margin-top: 100px;background: linear-gradient(pink, purple);transform: translate({{translateVal}});">
4.   </div>
5.   <div class="row">
6.     <button type="capsule" value="play" onclick="playAnimation"></button>
7.   </div>
8. </div>

9. /* xxx.css */
10. .container {
11.   width:100%;
12.   height:100%;
13.   flex-direction: column;
14.   align-items: center;
15.   justify-content: center;
16. }
17. button{
18.   width: 200px;
19. }
20. .row{
21.   width: 65%;
22.   height: 100px;
23.   align-items: center;
24.   justify-content: space-between;
25.   margin-top: 50px;
26.   margin-left: 260px;
27. }

28. // xxx.js
29. export default {
30.   data: {
31.     translateVal: 0,
32.     animation: null
33.   },
34.   onInit() {},
35.   onShow(){
36.     var options = {
37.       duration: 3000,
38.       easing:"friction",
39.       delay:"1000",
40.       fill: 'forwards',
41.       direction:'alternate',
42.       iterations: 2,
43.       begin: 0,
44.       end: 180
45.     };//设置参数
46.     this.animation = this.getUIContext().createAnimator(options);//创建动画
47.   },
48.   playAnimation() {
49.     var _this = this;
50.     this.animation.onframe = function(value) {
51.       _this.translateVal= value;
52.     };
53.     this.animation.play();
54.   }
55. }

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216164107.33799364690520679378276853697877:50001231000000:2800:4E049585949768F04D401A10814669EF45D150ACAE6A4E65712E5774997C5FF6.gif)

说明

- 使用createAnimator创建动画对象时必须传入options参数。
    
- begin插值起点，不设置时默认为0。
    
- end插值终点，不设置时默认为1。
    

## 添加动画事件和调用接口

animator支持事件和接口，可以通过添加frame、cancel、repeat、finish事件和调用update、play、pause、cancel、reverse、finish接口自定义动画效果。animator支持的事件和接口具体见动画中的[createAnimator](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-uicontext-uicontext#createanimator)。

1. <!-- xxx.hml -->
2. <div style="flex-direction: column;align-items: center;width: 100%;height: 100%;">
3.   <div style="width:200px;height: 200px;margin-top: 100px;background: linear-gradient(#b30d29, #dcac1b);
4.   transform: scale({{scaleVal}});"></div>
5.   <div style="width: {{DivWidth}};height: {{DivHeight}};margin-top: 200px;
6.   background: linear-gradient(pink, purple);margin-top: 200px;transform:translateY({{translateVal}});">
7.   </div>
8.   <div class="row">
9.     <button type="capsule" value="play" onclick="playAnimation"></button>
10.     <button type="capsule" value="update" onclick="updateAnimation"></button>
11.   </div>
12.   <div class="row1">
13.     <button type="capsule" value="pause" onclick="pauseAnimation"></button>
14.     <button type="capsule" value="finish" onclick="finishAnimation"></button>
15.   </div>
16.   <div class="row2">
17.     <button type="capsule" value="cancel" onclick="cancelAnimation"></button>
18.     <button type="capsule" value="reverse" onclick="reverseAnimation"></button>
19.   </div>
20. </div>

21. /* xxx.css */
22. button{
23.   width: 200px;
24. }
25. .row{
26.   width: 65%;
27.   height: 100px;
28.   align-items: center;
29.   justify-content: space-between;
30.   margin-top: 150px;
31.   position: fixed;
32.   top: 52%;
33.   left: 120px;
34. }
35. .row1{
36.   width: 65%;
37.   height: 100px;
38.   align-items: center;
39.   justify-content: space-between;
40.   margin-top: 120px;
41.   position: fixed;
42.   top: 65%;
43.   left: 120px;
44. }
45. .row2{
46.   width: 65%;
47.   height: 100px;
48.   align-items: center;
49.   justify-content: space-between;
50.   margin-top: 100px;
51.   position: fixed;
52.   top: 75%;
53.   left: 120px;
54. }

55. // xxx.js
56. export default {
57.   data: {
58.     scaleVal:1,
59.     DivWidth:200,
60.     DivHeight:200,
61.     translateVal:0,
62.     animation: null
63.   },
64.   onInit() {},
65.   onShow() {
66.     var options = {
67.       duration: 3000,
68.       fill: 'forwards',
69.       begin: 200,
70.       end: 270
71.     };
72.     this.animation = this.getUIContext().createAnimator(options);
73.     var _this= this;
74.     //添加动画重放事件
75.     this.animation.onrepeat = function() {
76.       this.getUIContext().getPromptAction().showToast({
77.         message: 'repeat'
78.       });
79.       var repeatOptions = {
80.         duration: 2000,
81.         iterations: 1,
82.          direction: 'alternate',
83.          begin: 180,
84.          end: 240
85.        };
86.         _this.animation?.update(repeatOptions);
87.         _this.animation?.play();
88.       };
89.   },
90.   playAnimation() {
91.     var _this= this;
92.     //添加动画逐帧插值回调事件
93.     this.animation.onframe = function(value) {
94.       _this.scaleVal= value/150,
95.       _this.DivWidth = value,
96.       _this.DivHeight = value,
97.       _this.translateVal = value-180
98.     };
99.     this.animation.play();
100.   },
101.   updateAnimation() {
102.     var newoptions = {
103.       duration: 5000,
104.       iterations: 2,
105.       begin: 120,
106.       end: 180
107.     };
108.     this.animation.update(newoptions);
109.     this.animation.play();//调用动画播放接口
110.   },
111.   pauseAnimation() {
112.     this.animation.pause();//调用动画暂停接口
113.   },
114.   finishAnimation() {
115.     var _this= this;
116.    //添加动画完成事件
117.     this.animation.onfinish = function() {
118.       this.getUIContext().getPromptAction().showToast({
119.         message: 'finish'
120.       });
121.     };
122.     this.animation.finish(); //调用动画完成接口
123.   },
124.   cancelAnimation() {
125.     this.animation.cancel(); //调用动画取消接口
126.   },
127.   reverseAnimation() {
128.     this.animation.reverse(); //调用动画倒放接口
129.   }
130. }

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216164107.07039814739987850272785781217898:50001231000000:2800:D218BE49C81FD6718F98AC9A3AB90469CDF2231CFE8E4920325EC75E0EC229D6.gif)

说明

在调用[reset](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-animator#reset9)接口的过程中可以使用这个接口更新动画参数，入参与[createAnimator](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-uicontext-uicontext#createanimator)一致。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-js-interpolator-animation "插值器动画")
# 自定义组件

更新时间: 2025-12-16 16:38

使用兼容JS的类Web开发范式的方舟开发框架支持自定义组件，用户可根据业务需求将已有的组件进行扩展，增加自定义的私有属性和事件，封装成新的组件，方便在工程中多次调用，提高页面布局代码的可读性。具体的封装方法示例如下：

- 构建自定义组件
    
    1. <!-- comp.hml -->
    2.  <div class="item"> 
    3.    <text class="title-style">{{title}}</text>
    4.    <text class="text-style" onclick="childClicked" focusable="true">点击这里查看隐藏文本</text>
    5.    <text class="text-style" if="{{showObj}}">hello world</text>
    6.  </div>
    
    7. /* comp.css */
    8.  .item {
    9.    width: 700px;
    10.    flex-direction: column;
    11.    height: 300px;
    12.    align-items: center;
    13.    margin-top: 100px;
    14.  }
    15.  .text-style {
    16.    width: 100%;
    17.    text-align: center;
    18.    font-weight: 500;
    19.    font-family: Courier;
    20.    font-size: 36px;
    21.  }
    22.  .title-style {
    23.    font-weight: 500;
    24.    font-family: Courier;
    25.    font-size: 50px;
    26.    color: #483d8b;
    27.  }
    
    28. // comp.js
    29.  export default {
    30.    props: {
    31.      title: {
    32.        default: 'title',
    33.      },
    34.      showObject: {},
    35.    },
    36.    data() {
    37.      return {
    38.        showObj: this.showObject,
    39.      };
    40.    },
    41.    childClicked () {
    42.      this.$emit('eventType1', {text: '收到子组件参数'});
    43.      this.showObj = !this.showObj;
    44.    },
    45.  }
    
- 引入自定义组件
    
    1. <!-- xxx.hml -->
    2.  <element name='comp' src='../../common/component/comp.hml'></element> 
    3.  <div class="container"> 
    4.    <text>父组件：{{text}}</text>
    5.    <comp title="自定义组件" show-object="{{isShow}}" @event-type1="textClicked"></comp>
    6.  </div>
    
    7. /* xxx.css */
    8.  .container {
    9.    background-color: #f8f8ff;
    10.    flex: 1;
    11.    flex-direction: column;
    12.    align-content: center;
    13.  }
    
    14. // xxx.js
    15.  export default {
    16.    data: {
    17.      text: '开始',
    18.      isShow: false,
    19.    },
    20.    textClicked (e) {
    21.      this.text = e.detail.text;
    22.    },
    23.  }
    

本示例中父组件通过添加自定义属性向子组件传递了名称为title的参数，子组件在props中接收。同时子组件也通过事件绑定向上传递了参数text，接收时通过e.detail获取。要绑定子组件事件，父组件事件命名必须遵循事件绑定规则，详见[自定义组件的基本用法](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-components-custom-basic-usage)。自定义组件效果如下图所示：

**图1** 自定义组件的效果

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163848.83842596872580396310031256975343:50001231000000:2800:4097A6C3A15BE890C34CB5DE870338A628AB3C4C4CA6FB4A11E7EC6EE5486619.png)

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-js-animate-frame "动画帧")
# 自定义组件

更新时间: 2025-12-16 16:38

使用兼容JS的类Web开发范式的方舟开发框架支持自定义组件，用户可根据业务需求将已有的组件进行扩展，增加自定义的私有属性和事件，封装成新的组件，方便在工程中多次调用，提高页面布局代码的可读性。具体的封装方法示例如下：

- 构建自定义组件
    
    1. <!-- comp.hml -->
    2.  <div class="item"> 
    3.    <text class="title-style">{{title}}</text>
    4.    <text class="text-style" onclick="childClicked" focusable="true">点击这里查看隐藏文本</text>
    5.    <text class="text-style" if="{{showObj}}">hello world</text>
    6.  </div>
    
    7. /* comp.css */
    8.  .item {
    9.    width: 700px;
    10.    flex-direction: column;
    11.    height: 300px;
    12.    align-items: center;
    13.    margin-top: 100px;
    14.  }
    15.  .text-style {
    16.    width: 100%;
    17.    text-align: center;
    18.    font-weight: 500;
    19.    font-family: Courier;
    20.    font-size: 36px;
    21.  }
    22.  .title-style {
    23.    font-weight: 500;
    24.    font-family: Courier;
    25.    font-size: 50px;
    26.    color: #483d8b;
    27.  }
    
    28. // comp.js
    29.  export default {
    30.    props: {
    31.      title: {
    32.        default: 'title',
    33.      },
    34.      showObject: {},
    35.    },
    36.    data() {
    37.      return {
    38.        showObj: this.showObject,
    39.      };
    40.    },
    41.    childClicked () {
    42.      this.$emit('eventType1', {text: '收到子组件参数'});
    43.      this.showObj = !this.showObj;
    44.    },
    45.  }
    
- 引入自定义组件
    
    1. <!-- xxx.hml -->
    2.  <element name='comp' src='../../common/component/comp.hml'></element> 
    3.  <div class="container"> 
    4.    <text>父组件：{{text}}</text>
    5.    <comp title="自定义组件" show-object="{{isShow}}" @event-type1="textClicked"></comp>
    6.  </div>
    
    7. /* xxx.css */
    8.  .container {
    9.    background-color: #f8f8ff;
    10.    flex: 1;
    11.    flex-direction: column;
    12.    align-content: center;
    13.  }
    
    14. // xxx.js
    15.  export default {
    16.    data: {
    17.      text: '开始',
    18.      isShow: false,
    19.    },
    20.    textClicked (e) {
    21.      this.text = e.detail.text;
    22.    },
    23.  }
    

本示例中父组件通过添加自定义属性向子组件传递了名称为title的参数，子组件在props中接收。同时子组件也通过事件绑定向上传递了参数text，接收时通过e.detail获取。要绑定子组件事件，父组件事件命名必须遵循事件绑定规则，详见[自定义组件的基本用法](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-components-custom-basic-usage)。自定义组件效果如下图所示：

**图1** 自定义组件的效果

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163848.83842596872580396310031256975343:50001231000000:2800:4097A6C3A15BE890C34CB5DE870338A628AB3C4C4CA6FB4A11E7EC6EE5486619.png)

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-js-animate-frame "动画帧")
# 使用WebGL绘制图形

更新时间: 2025-12-16 16:39

## 场景介绍

WebGL的全称为Web Graphics Library（网页图形库），主要用于交互式渲染2D图形。目前HarmonyOS中使用的WebGL是基于OpenGL裁剪的OpenGL ES，可以在HTML5的Canvas元素对象中使用，无需使用插件，支持跨平台。WebGL程序是由JavaScript代码组成的，其中使用的API可以利用用户设备提供的GPU硬件完成图形渲染和加速。更多信息请参考[WebGL™标准](https://www.khronos.org/registry/webgl/specs/latest/1.0/)。

说明

目前该功能仅支持使用兼容JS的类Web开发范式开发。

## 基本概念

### 着色器程序

将缓冲区中的数据推送到着色器中还需涉及“着色器程序”，一个负责关联着色器和缓冲区的JavaScript对象。一个WebGLProgram对象由两个编译过后的WebGLShader组成，即顶点着色器和片元着色器（均由GLSL语言所写）。

### 着色器

着色器可以理解为运行在显卡中的指令和数据。在WebGL中，着色器是用OpenGL ES着色语言（GLSL）编写的。

完整的着色器包括顶点着色器和片元着色器。顶点着色器和片元着色器的交互则涉及到图片光栅化。

- 顶点着色器：最基本的任务是接收三维空间中点的坐标，将其处理为二维空间中的坐标并输出。
    
- 片元着色器：最基本的任务是对需要处理的屏幕上的每个像素输出一个颜色值。
    

### 图片光栅化

将顶点着色器输出的二维空间中的点坐标，转化为需要处理的像素并传递给片元着色器的过程。

### 帧缓冲区对象

帧缓冲区对象为绘图缓冲区提供替代呈现目标。它们是颜色、深度和模板缓冲区的集合，通常用于渲染图像。

### 纹理

纹理是一种图像，可以应用到3D模型的表面上。WebGL中的纹理有许多属性，包括宽度、高度、格式和类型。在使用纹理时，需要将其加载到WebGL中，并将其绑定到一个纹理单元上。

## 变量与接口说明

### 变量类型

|类型|对应Web IDL类型|描述|
|:--|:--|:--|
|GLenum|unsigned long|用于枚举。|
|GLboolean|boolean|true或者false。|
|GLbitfield|unsigned long|无符号整数，可以包含多个位标志。每个位标志都代表一个特定的选项。|
|GLbyte|byte|纹理八位（一个字节），2的补码表示的有符号整数。|
|GLshort|short|16位2的补码表示的有符号整数。|
|GLint|long|32位2的补码表示的有符号整数。|
|GLsizei|long|用来描述尺寸（例如：绘画缓冲drawing buffer 的宽和高）。|
|GLintptr|long long|用来表示指针的特殊类型，通常用于指定缓冲区对象的偏移量。|
|GLsizeiptr|long long|用来表示指针的特殊类型，通常用于指定缓冲区对象的大小。|
|GLubyte|octet|八位（一个字节）2的补码表示的无符号整数。|
|GLushort|unsigned short|16位2的补码表示的无符号整数。|
|GLuint|unsigned long|32位2的补码表示的无符号整数。|
|GLfloat|unrestricted float|32位的IEEE标准的浮点数。|
|GLclampf|unrestricted float|限值32位IEEE浮点数。|

### 接口说明

|接口名|描述|
|:--|:--|
|canvas.getContext|获取canvas对象上下文。|
|webgl.createBuffer(): WebGLBuffer \| null|创建与初始化WebGL数据缓冲区。|
|webgl.bindBuffer(target: GLenum, buffer: WebGLBuffer \| null): void|将WebGL数据缓冲区与目标进行绑定。|
|webgl.bufferData(target: GLenum, srcData: ArrayBufferView, usage: GLenum, srcOffset: GLuint, length?: GLuint): void|创建并初始化WebGL的数据存储区。|
|webgl.getAttribLocation(program: WebGLProgram, name: string): GLint|从给定WebGL着色程序中获取着色器中attribute变量的地址。|
|webgl.vertexAttribPointer(index GLuint, size: GLint, type: GLenum, normalized: GLboolean, stride: GLsizei, offset: GLintptr): void|将缓冲区对象分配给变量。|
|webgl.enableVertexAttribArray(index: GLuint): void|连接变量与分配给它的缓冲区对象。|
|webgl.clearColor(red: GLclampf, green: GLclampf, blue: GLclampf, alpha: GLclampf): void|清空<canvas>指定的颜色。|
|webgl.clear(mask: GLbitfield): void|清空<canvas>。|
|webgl.drawArrays(mode: GLenum, first: GLint, count: GLsizei): void|执行数据绘制。|
|webgl.flush(): void|刷新数据至GPU，清空缓冲区。|
|webgl.createProgram(): WebGLProgram \| null|创建着色器程序对象。|

## 开发步骤

如下以实现一个彩色正方形为例，来演示使用WebGL绘制2D图形的过程。

1. 使用WebGL进行3D渲染前，首先需要一个Canvas元素。以下示例创建了一个Canvas元素并设置一个onclick事件处理程序来初始化WebGL上下文。
    
    1.  <div class="container">
    2.      <canvas ref="canvas1" style="width : 400px; height : 400px; background-color : lightyellow;"></canvas>
    3.      <button class="btn-button" onclick="BtnColorTriangle">BtnColorTriangle</button>
    4.  </div>
    
2. 设置WebGL的上下文。
    
    - JavaScript 代码中的 main() 函数将会在文档加载完成之后被调用。它的任务是设置WebGL上下文并开始渲染内容。
        
    - 当获取到canvas之后，会调用getContext函数并向它传递 "webgl" 参数，来尝试获取WebGLRenderingContext。如果浏览器不支持WebGL，getContext将会返回null，如果WebGL上下文成功初始化，变量'gl'会用来引用该上下文。
        
    
    1. function main() {
    2.   const canvas = document.querySelector("#glcanvas");
    3.   // 初始化WebGL上下文
    4.   const gl = canvas.getContext("webgl");
    
    5.   // 确认WebGL支持性
    6.   if (!gl) {
    7.     alert("你的浏览器、操作系统或硬件等可能不支持WebGL。");
    8.     return;
    9.   }
    10.   // 使用完全不透明的黑色清除所有图像
    11.   gl.clearColor(0.0, 0.0, 0.0, 1.0);
    12.   // 用上面指定的颜色清除缓冲区
    13.   gl.clear(gl.COLOR_BUFFER_BIT);
    14. }
    
3. 定义顶点着色器。
    
    顶点着色器需要对顶点坐标进行必要的转换，在每个顶点基础上进行其他调整或计算，然后通过将其保存在由GLSL提供的特殊变量中来返回变换后的顶点。
    
    在矩阵计算之前需要先引入gl-matrix开源工具库，可以从[gl-matrix官网](https://glmatrix.net/)下载，也可以使用npm命令下载：
    
    npm install gl-matrix
    
    1. // 引入mat4
    2. import { mat4 } from 'gl-matrix'
    3. const vsSource = `
    4.     attribute vec4 aVertexPosition;
    5.     uniform mat4 uModelViewMatrix;
    6.     uniform mat4 uProjectionMatrix;
    7.     void main() {
    8.       gl_Position = uProjectionMatrix * uModelViewMatrix * aVertexPosition;
    9.     }
    10.   `;
    
4. 定义片段着色器。
    
    片段着色器在顶点着色器处理完图形的顶点后，会被要绘制的每个图形的每个像素点调用一次。
    
    1. const fsSource = `
    2.     void main() {
    3.       gl_FragColor = vec4(1.0, 1.0, 1.0, 1.0);
    4.     }
    5.  `;
    
5. 将着色器传递给WebGL。
    
    定义顶点着色器与片段着色器之后，需要将它们传递给WebGL，并将其编译连接在一起。
    
    如下代码通过调用 loadShader()，为着色器传递类型和来源。创建了两个着色器。然后创建一个附加着色器的程序，将它们连接在一起。如果编译或链接失败，代码将弹出alert。
    
    1. // 初始化着色器程序，让WebGL知道如何绘制数据
    2. function initShaderProgram(gl, vsSource, fsSource) {
    3.   const vertexShader = loadShader(gl, gl.VERTEX_SHADER, vsSource);
    4.   const fragmentShader = loadShader(gl, gl.FRAGMENT_SHADER, fsSource);
    5.   // 创建着色器程序
    6.   const shaderProgram = gl.createProgram();
    7.   gl.attachShader(shaderProgram, vertexShader);
    8.   gl.attachShader(shaderProgram, fragmentShader);
    9.   gl.linkProgram(shaderProgram);
    10.   // 如果创建失败，将会弹出alert
    11.   if (!gl.getProgramParameter(shaderProgram, gl.LINK_STATUS)) {
    12.     alert(
    13.       "无法初始化着色器程序: " +
    14.      gl.getProgramInfoLog(shaderProgram),
    15.     );
    16.     return null;
    17.   }
    18.   return shaderProgram;
    19. }
    20. // 创建指定类型的着色器，上传source源码并编译
    21. function loadShader(gl, type, source) {
    22.   const shader = gl.createShader(type);
    23.   // 将资源发送到着色器对象
    24.   gl.shaderSource(shader, source);
    25.   // 编译着色器程序
    26.   gl.compileShader(shader);
    27.   // 查看是否编译成功
    28.   if (!gl.getShaderParameter(shader, gl.COMPILE_STATUS)) {
    29.     alert(
    30.    "编译着色器时出错：" + gl.getShaderInfoLog(shader),
    31.     );
    32.     gl.deleteShader(shader);
    33.     return null;
    34.   }
    35.   return shader;
    36. }
    
6. 查找WebGL返回分配的输入位置。
    
    - 在创建着色器程序之后，需要查找WebGL返回分配的输入位置。上述有一个属性和两个Uniform。
        
    - 属性从缓冲区接收值。顶点着色器的每次迭代都从分配给该属性的缓冲区接收下一个值。
        
    - Uniform类似于JavaScript全局变量。它们在着色器的所有迭代中保持相同的值。由于属性的位置是特定于单个着色器程序的，因此将它们存储在一起以易于传递。
        
    
    1. const programInfo = {
    2.   program: shaderProgram,
    3.   attribLocations: {
    4.     vertexPosition: gl.getAttribLocation(shaderProgram, "aVertexPosition"),
    5.   },
    6.   uniformLocations: {
    7.     projectionMatrix: gl.getUniformLocation(shaderProgram, "uProjectionMatrix"),
    8.     modelViewMatrix: gl.getUniformLocation(shaderProgram, "uModelViewMatrix"),
    9.   },
    10. };
    
7. 创建缓冲器对象。
    
    - 在画正方形前，需要创建一个缓冲器来存储它的顶点。
        
    - 首先调用gl的成员函数createBuffer()得到缓冲对象并存储在顶点缓冲器。然后调用 bindBuffer() 函数绑定上下文。
        
    - 创建一个Javascript数组去记录每一个正方体的每一个顶点。然后将其转化为WebGL浮点型类型的数组，并将其传到gl对象的bufferData()方法来建立对象的顶点。
        
    
    1. function initBuffers(gl) {
    2.   const positionBuffer = initPositionBuffer(gl);
    3.   return {
    4.     position: positionBuffer,
    5.   };
    6. }
    7. function initPositionBuffer(gl) {
    8.   // 为正方形的位置创建一个缓冲区。
    9.   const positionBuffer = gl.createBuffer();
    10.   // 选择positionBuffer作为应用缓冲区的位置。
    11.   gl.bindBuffer(gl.ARRAY_BUFFER, positionBuffer);
    12.   // 创建一个正方形的位置数组。
    13.   const positions = [1.0, 1.0, -1.0, 1.0, 1.0, -1.0, -1.0, -1.0];
    14.   //将位置列表传递给WebGL以构建形状。
    15.   gl.bufferData(gl.ARRAY_BUFFER, new Float32Array(positions), gl.STATIC_DRAW);
    16.   return positionBuffer;
    17. }
    18. export { initBuffers };
    
8. 渲染场景。
    
    - 用背景色擦除画布，然后建立摄像机透视矩阵。设置45度的视图角度，并且设置一个适合实际图像的宽高比。指定在摄像机距离0.1到100单位长度的范围内的物体可见。
        
    - 加载特定位置，并把正方形放在距离摄像机6个单位的位置。然后，绑定正方形的顶点缓冲到上下文，并配置好，再通过调用drawArrays()方法来画出对象。
        
    
    1. function drawScene(gl, programInfo, buffers) {
    2.   gl.clearColor(0.0, 0.0, 0.0, 1.0);
    3.   gl.clearDepth(1.0); // 清除所有内容。
    4.   gl.depthFunc(gl.LEQUAL);
    5.   // 清除画布。
    6.    gl.clear(gl.COLOR_BUFFER_BIT | gl.DEPTH_BUFFER_BIT);
    7.   //创建透视矩阵用于模拟相机中的透视变形。
    8.   const fieldOfView = (45 * Math.PI) / 180;
    9.   const aspect = gl.canvas.clientWidth / gl.canvas.clientHeight;
    10.   const zNear = 0.1;
    11.   const zFar = 100.0;
    12.   const projectionMatrix = mat4.create();
    13.   mat4.perspective(projectionMatrix, fieldOfView, aspect, zNear, zFar);
    14.   // 将绘制位置设置为标识点，即场景的中心。
    15.   const modelViewMatrix = mat4.create();
    16.   // 开始绘制正方形。
    17.   mat4.translate(
    18.     modelViewMatrix, // 目标矩阵
    19.     modelViewMatrix, // 要转换的矩阵
    20.     [-0.0, 0.0, -6.0],
    21.   );
    22.   {
    23.     const numComponents = 2;
    24.     const type = gl.FLOAT;
    25.     const normalize = false;
    26.     const stride = 0; // 从一组值到下一组值需要多少字节
    27.     const offset = 0;
    28.     gl.bindBuffer(gl.ARRAY_BUFFER, buffers.position);
    29.     gl.vertexAttribPointer(
    30.       programInfo.attribLocations.vertexPosition,
    31.       numComponents,
    32.       type,
    33.       normalize,
    34.       stride,
    35.       offset,
    36.     );
    37.     gl.enableVertexAttribArray(programInfo.attribLocations.vertexPosition);
    38.   }
    39.   gl.useProgram(programInfo.program);
    40.   gl.uniformMatrix4fv(
    41.     programInfo.uniformLocations.projectionMatrix,
    42.     false,
    43.     projectionMatrix,
    44.   );
    45.   gl.uniformMatrix4fv(
    46.     programInfo.uniformLocations.modelViewMatrix,
    47.     false,
    48.     modelViewMatrix,
    49.   );
    50.   {
    51.     const offset = 0;
    52.     const vertexCount = 4;
    53.     gl.drawArrays(gl.TRIANGLE_STRIP, offset, vertexCount);
    54.   }
    55. }
    56. // 告诉WebGL如何从位置中拉出位置缓冲到vertexPosition属性中。
    57. function setPositionAttribute(gl, buffers, programInfo) {
    58.   const numComponents = 2;
    59.   const type = gl.FLOAT;
    60.   const normalize = false;
    61.   const stride = 0; // 从一组值到下一组值需要多少字节
    62.   const offset = 0;
    63.   gl.bindBuffer(gl.ARRAY_BUFFER, buffers.position);
    64.   gl.vertexAttribPointer(
    65.     programInfo.attribLocations.vertexPosition,
    66.     numComponents,
    67.     type,
    68.     normalize,
    69.     stride,
    70.     offset,
    71.   );
    72.   gl.enableVertexAttribArray(programInfo.attribLocations.vertexPosition);
    73. }
    74. export { drawScene };
    

最终实现效果示意如下：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163902.21943217636700730332696292325897:50001231000000:2800:F570B0C59E2273254B7B7113BD00CBA17E2D7E48716F215408810A4E849C68F0.png)

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-js-webgl "WebGL")
