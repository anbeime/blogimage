# Core Speech Kit简介

更新时间: 2025-12-16 16:27

Core Speech Kit（基础语音服务）集成了语音类基础AI能力，包括文本转语音（TextToSpeech）及语音识别（SpeechRecognizer）能力，便于用户与设备进行互动，实现将实时输入的语音与文本之间相互转换。

## 场景介绍

- 文本转语音：将一段不超过10000字数的文本合成为语音并进行播报。
- 语音识别：将一段音频信息（短语音模式不超过60s，长语音模式不超过8h）转换为文本，可以将pcm音频文件或者实时语音转换为文字。

## 约束与限制

### 支持的设备

Phone、Tablet、PC/2in1。

### 支持的国家/地区

仅适用于中国境内（不包含中国香港、中国澳门、中国台湾）。

### 能力限制

|AI能力|约束|
|:--|:--|
|文本转语音（中国境内版本）|- 支持的语种类型：中文、英文。（简体中文、繁体中文、中文语境下的英文）<br>- 支持的音色类型：聆小珊女声音色、英语（美国）劳拉女声音色、凌飞哲男声音色。<br>- 文本长度：不超过10000字数。|
|语音识别|- 支持的语种类型：中文普通话。<br>- 支持的模型类型：离线。<br>- 语音时长：短语音模式不超过60s，长语音模式不超过8h。|

## 模拟器支持情况

本Kit能力从6.0.0(20)版本开始支持模拟器。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/core-speech-kit-guide "Core Speech Kit（基础语音服务）")
# 文本转语音

更新时间: 2025-12-16 16:27

Core Speech Kit支持将一篇不超过10000字数的中英文文本（简体中文、繁体中文、数字、英文）合成为语音，并以选定音色进行播报。

开发者可对播报的策略进行设置，包括单词播报、数字播报、静音停顿、汉字发音策略。

## 场景介绍

手机/平板等设备在无网状态下，系统应用无障碍（屏幕朗读）接入文本转语音能力，为视障人士或不方便阅读场景提供播报能力。

## 约束与限制

|AI能力|约束|
|:--|:--|
|文本转语音（中国境内版本）|- 支持的语种类型：中文、英文。（简体中文、繁体中文、中文语境下的英文）<br>- 支持的音色类型：聆小珊女声音色、英语（美国）劳拉女声音色、凌飞哲男声音色。<br>- 文本长度：不超过10000字数。|

## 开发步骤

1. 在使用文本转语音时，将实现文本转语音相关的类添加至工程。
    
    1. import { textToSpeech } from '@kit.CoreSpeechKit';
    2. import { BusinessError } from '@kit.BasicServicesKit';
    
2. 调用createEngine接口，创建[TextToSpeechEngine](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/hms-ai-texttospeech#section185526396124)实例。
    
    createEngine接口提供了两种调用形式，当前以其中一种作为示例，其他方式可参考[API参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/hms-ai-texttospeech)。
    
    1. let ttsEngine: textToSpeech.TextToSpeechEngine;
    
    2. // 设置创建引擎参数
    3. let extraParam: Record<string, Object> = {"style": 'interaction-broadcast', "locate": 'CN', "name": 'EngineName'};
    4. let initParamsInfo: textToSpeech.CreateEngineParams = {
    5.   language: 'zh-CN',
    6.   person: 0,
    7.   online: 1,
    8.   extraParams: extraParam
    9. };
    
    10. // 调用createEngine方法
    11. textToSpeech.createEngine(initParamsInfo, (err: BusinessError, textToSpeechEngine: textToSpeech.TextToSpeechEngine) => {
    12.   if (!err) {
    13.     console.info('Succeeded in creating engine');
    14.     // 接收创建引擎的实例
    15.     ttsEngine = textToSpeechEngine;
    16.   } else {
    17.     console.error(`Failed to create engine. Code: ${err.code}, message: ${err.message}.`);
    18.   }
    19. });
    
3. 得到[TextToSpeechEngine](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/hms-ai-texttospeech#section185526396124)实例对象后，实例化[SpeakParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/hms-ai-texttospeech#section7843122735210)对象、[SpeakListener](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/hms-ai-texttospeech#section115395631614)对象，并传入待合成及播报的文本originalText，调用[speak](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/hms-ai-texttospeech#section140216144119)接口进行播报。
    
    1. // 设置speak的回调信息
    2. let speakListener: textToSpeech.SpeakListener = {
    3.   // 开始播报回调
    4.   onStart(requestId: string, response: textToSpeech.StartResponse) {
    5.     console.info(`onStart, requestId: ${requestId} response: ${JSON.stringify(response)}`);
    6.   },
    7.   // 合成完成及播报完成回调
    8.   onComplete(requestId: string, response: textToSpeech.CompleteResponse) {
    9.     console.info(`onComplete, requestId: ${requestId} response: ${JSON.stringify(response)}`);
    10.   },
    11.   // 停止播报回调
    12.   onStop(requestId: string, response: textToSpeech.StopResponse) {
    13.     console.info(`onStop, requestId: ${requestId} response: ${JSON.stringify(response)}`);
    14.   },
    15.   // 返回音频流
    16.   onData(requestId: string, audio: ArrayBuffer, response: textToSpeech.SynthesisResponse) {
    17.     console.info(`onData, requestId: ${requestId} sequence: ${JSON.stringify(response)} audio: ${JSON.stringify(audio)}`);
    18.   },
    19.   // 错误回调
    20.   onError(requestId: string, errorCode: number, errorMessage: string) {
    21.     console.error(`onError, requestId: ${requestId} errorCode: ${errorCode} errorMessage: ${errorMessage}`);
    22.   }
    23. };
    24. // 设置回调
    25. ttsEngine.setListener(speakListener);
    26. let originalText: string = 'Hello HarmonyOS';
    27. // 设置播报相关参数
    28. let extraParam: Record<string, Object> = {"queueMode": 0, "speed": 1, "volume": 2, "pitch": 1, "languageContext": 'zh-CN',  
    29. "audioType": "pcm", "soundChannel": 3, "playType": 1 };
    30. let speakParams: textToSpeech.SpeakParams = {
    31.   requestId: '123456', // requestId在同一实例内仅能用一次，请勿重复设置
    32.   extraParams: extraParam
    33. };
    34. // 调用播报方法
    35. // 开发者可以通过修改speakParams主动[设置播报策略](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/texttospeech-guide#section137481719163910)
    36. ttsEngine.speak(originalText, speakParams);
    
4. （可选）当需要停止合成及播报时，可调用[stop](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/hms-ai-texttospeech#section14433919171116)接口。
    
    1. ttsEngine.stop();
    
5. （可选）当需要查询文本转语音服务是否处于忙碌状态时，可调用[isBusy](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/hms-ai-texttospeech#section35361720111113)接口。
    
    1. ttsEngine.isBusy();
    
6. （可选）当需要查询支持的语种音色信息时，可调用[listVoices](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/hms-ai-texttospeech#section813761871119)接口。
    
    listVoices接口提供了两种调用形式，当前以其中一种作为示例，其他方式可参考[API参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/hms-ai-texttospeech)。
    
    1. // 在组件中声明并初始化字符串voiceInfo
    2. @State voiceInfo: string = "";
    
    3. // 设置查询相关参数
    4. let voicesQuery: textToSpeech.VoiceQuery = {
    5.   requestId: '12345678', // requestId在同一实例内仅能用一次，请勿重复设置
    6.   online: 1
    7. };
    8. // 调用listVoices方法，以callback返回
    9. ttsEngine.listVoices(voicesQuery, (err: BusinessError, voiceInfo: textToSpeech.VoiceInfo[]) => {
    10.   if (!err) {
    11.     // 接收目前支持的语种音色等信息
    12.     this.voiceInfo = JSON.stringify(voiceInfo);
    13.     console.info(`Succeeded in listing voices, voiceInfo is ${this.voiceInfo}`);
    14.   } else {
    15.     console.error(`Failed to list voices. Code: ${err.code}, message: ${err.message}`);
    16.   }
    17. });
    

## 设置播报策略

由于不同场景下，模型自动判断所选择的播报策略可能与实际需求不同，此章节提供对于播报策略进行主动设置的方法。

说明

以下取值说明均为有效取值，若所使用的数值在有效取值之外则播报结果可能与预期不符，并产生错误的播报结果。

### 设置单词播报方式

文本格式：[hN] (N=0/1/2)

N取值说明：

|取值|说明|
|:--|:--|
|0|智能判断单词播放方式。默认值为0。|
|1|逐个字母进行播报。|
|2|以单词方式进行播报。|

文本示例：

1. "hello[h1] world"

hello使用单词发音，world及后续单词将会逐个字母进行发音。

### 设置数字播报策略

格式：[nN] (N=0/1/2)

N取值说明：

|取值|说明|
|:--|:--|
|0|智能判断数字处理策略。默认值为0。|
|1|作为号码逐个数字播报。|
|2|作为数值播报。超过18位数字不支持，自动按逐个数字进行播报。|

文本示例：

1. "[n2]123[n1]456[n0]"

其中，123将会按照数值播报，456则会按照号码播报，而后的文本中的数字，均会自动判断。

### 插入静音停顿

格式：[pN]

描述：N为无符号整数，单位为ms。

文本示例：

1. "你好[p500]小艺"

该句播报时，将会在“你好”后插入500ms的静音停顿。

### 指定汉字发音

汉字的声调，通过在拼音后接一位数字1~5分别表示阴平、阳平、上声、去声和轻声5个声调。

格式：[=MN]

描述：M表示拼音，N表示声调。

N取值说明：

|取值|说明|
|:--|:--|
|1|阴平|
|2|阳平|
|3|上声|
|4|去声|
|5|轻声|

文本示例：

1. "着[=zhuo2]手"

“着”字将读作“zhuó”。

## 开发实例

点击按钮，播报一段文本。

### Index.ets

1. import { textToSpeech } from '@kit.CoreSpeechKit';
2. import { BusinessError } from '@kit.BasicServicesKit';
3. import { PromptAction } from '@kit.ArkUI';
4. import { UIContext } from '@kit.ArkUI';
5. import { TreeMap } from '@kit.ArkTS';
6. import { fileIo as fs } from '@kit.CoreFileKit';
7. import PcmPlayer from './PcmPlayer';
8. import { audio } from '@kit.AudioKit';
9. import { Context } from '@kit.AbilityKit';

10. const TAG: string = 'TtsDemo';
11. let ttsEngine: textToSpeech.TextToSpeechEngine;
12. let bufferLength: number = 0;
13. let engineCreated: boolean = false;

14. // 定义一个函数来拼接ArrayBuffer
15. function concatenateArrayBuffers(buffers: ArrayBuffer[]): ArrayBuffer {
16.   const totalLength = buffers.reduce((sum, buffer) => sum + buffer.byteLength, 0);
17.   const concatenatedBuffer = new ArrayBuffer(totalLength);
18.   let offset = 0;
19.   for (const buffer of buffers) {
20.     const uint8Array = new Uint8Array(buffer);
21.     new Uint8Array(concatenatedBuffer, offset, uint8Array.length).set(uint8Array);
22.     offset += uint8Array.length;
23.   }
24.   return concatenatedBuffer;
25. }

26. @Entry
27. @Component
28. struct Index {
29.   @State createCount: number = 0;
30.   @State originalText: string = "\n\t\t古人学问无遗力，少壮工夫老始成；\n\t\t" + "纸上得来终觉浅，绝知此事要躬行。\n\t\t";
31.   @State uiContext: UIContext = this.getUIContext()
32.   @State promptAction: PromptAction = this.uiContext.getPromptAction();
33.   private pcmData: TreeMap<number, Uint8Array> = new TreeMap();
34.   private pcmPlayer: PcmPlayer = new PcmPlayer();

35.   build() {
36.     Column() {
37.       Scroll() {
38.         Column() {
39.           TextArea({ placeholder: 'Please enter tts original text', text: `${this.originalText}` })
40.             .margin(20)
41.             .focusable(false)
42.             .border({ width: 5, color: 0x317AE7, radius: 10, style: BorderStyle.Dotted })
43.             .onChange((value: string) => {
44.               this.originalText = value;
45.               console.info(TAG, "original text: " + this.originalText);
46.             })

47.           Button() {
48.             Text("CreateEngine")
49.               .fontColor(Color.White)
50.               .fontSize(20)
51.           }
52.           .type(ButtonType.Capsule)
53.           .backgroundColor("#0x317AE7")
54.           .width("80%")
55.           .height(50)
56.           .margin(10)
57.           .onClick(() => {
58.             engineCreated = true
59.             this.createCount++;
60.             console.info(`createByCallback：createCount:${this.createCount}`);
61.             this.createByCallback();
62.             this.promptAction.showToast({
63.               message: 'CreateEngine success!',
64.               duration: 2000
65.             });
66.           })

67.           Button() {
68.             Text("speak")
69.               .fontColor(Color.White)
70.               .fontSize(20)
71.           }
72.           .type(ButtonType.Capsule)
73.           .backgroundColor("#0x317AE7")
74.           .width("80%")
75.           .height(50)
76.           .margin(10)
77.           .onClick(() => {
78.             if (engineCreated) {
79.               try {
80.                 this.speak();
81.                 this.promptAction.showToast({
82.                   message: 'start speaking',
83.                   duration: 2000
84.                 });
85.               } catch (err)  {
86.                   this.promptAction.showToast({
87.                     message: 'start speaking failed',
88.                     duration: 2000
89.                   });
90.                 }
91.             } else {
92.               this.promptAction.showToast({
93.                 message: 'The engine has not been created',
94.                 duration: 2000
95.               });
96.             }
97.           })

98.           Button() {
99.             Text("speakOnData")
100.               .fontColor(Color.White)
101.               .fontSize(20)
102.           }
103.           .type(ButtonType.Capsule)
104.           .backgroundColor("#0x317AE7")
105.           .width("80%")
106.           .height(50)
107.           .margin(10)
108.           .onClick(() => {
109.             if (engineCreated) {
110.               try {
111.                 this.speakOnData();
112.                 this.promptAction.showToast({
113.                   message: 'start speakOnData',
114.                   duration: 2000
115.                 });
116.               } catch (err) {
117.                 this.promptAction.showToast({
118.                   message: 'start speakOnData failed',
119.                   duration: 2000
120.                 });
121.               }
122.             } else {
123.               this.promptAction.showToast({
124.                 message: 'The engine has not been created',
125.                 duration: 2000
126.               });
127.             }
128.           })

129.           Button() {
130.             Text("stop")
131.               .fontColor(Color.White)
132.               .fontSize(20)
133.           }
134.           .type(ButtonType.Capsule)
135.           .backgroundColor("#0x317AE7")
136.           .width("80%")
137.           .height(50)
138.           .margin(10)
139.           .onClick(() => {
140.             try {
141.               let isBusy: boolean = ttsEngine.isBusy();
142.               let isPlaying: boolean = this.pcmPlayer.isPlaying();
143.               if (isBusy) {
144.                 ttsEngine.stop();
145.               }
146.               if (isPlaying) {
147.                 this.pcmPlayer.stop()
148.               }
149.               this.promptAction.showToast({
150.                 message: 'stop!',
151.                 duration: 2000
152.               });
153.             } catch (err) {
154.               this.promptAction.showToast({
155.                 message: 'stop failed',
156.                 duration: 2000
157.               });
158.             }
159.           })

160.           Button() {
161.             Text("isBusy")
162.               .fontColor(Color.White)
163.               .fontSize(20)
164.           }
165.           .type(ButtonType.Capsule)
166.           .backgroundColor("#0x317AE7")
167.           .width("80%")
168.           .height(50)
169.           .margin(10)
170.           .onClick(() => {
171.             try {
172.               let isBusy: boolean = ttsEngine.isBusy();
173.               let isPlaying: boolean = this.pcmPlayer.isPlaying();
174.               console.info('isBusy :' + isBusy);
175.               console.info('isPlaying :' + isPlaying);
176.               this.promptAction.showToast({
177.                 message: 'speak isBusy :' + isBusy + '\nspeakOnData isBusy :' + isPlaying,
178.                 duration: 2000
179.               });
180.             } catch (err) {
181.               this.promptAction.showToast({
182.                 message: 'isBusy failed',
183.                 duration: 2000
184.               });
185.             }
186.           })

187.           Button() {
188.             Text("shutdown")
189.               .fontColor(Color.White)
190.               .fontSize(20)
191.           }
192.           .type(ButtonType.Capsule)
193.           .backgroundColor("#0x317AA7")
194.           .width("80%")
195.           .height(50)
196.           .margin(10)
197.           .onClick(() => {
198.             try {
199.               this.pcmPlayer.release()
200.               ttsEngine.shutdown();
201.               engineCreated = false
202.               this.promptAction.showToast({
203.                 message: 'shutdown success!',
204.                 duration: 2000
205.               });
206.             } catch (err) {
207.               this.promptAction.showToast({
208.                 message: 'shutdown failed',
209.                 duration: 2000
210.               });
211.             }
212.           })

213.         }
214.         .layoutWeight(1)
215.       }
216.       .width('100%')
217.       .height('100%')

218.     }
219.   }

220.   // 创建引擎，通过callback形式返回
221.   // 当引擎不存在、引擎资源不存在、初始化超时，返回错误码1002300005，引擎创建失败
222.   private createByCallback() {
223.     // 设置创建引擎参数
224.     let extraParam: Record<string, Object> = { "style": 'interaction-broadcast', "locate": 'CN', "name": 'EngineName' }
225.     let initParamsInfo: textToSpeech.CreateEngineParams = {
226.       language: 'zh-CN',
227.       person: 0,
228.       online: 1,
229.       extraParams: extraParam
230.     };
231.     try {
232.       // 调用createEngine方法
233.       textToSpeech.createEngine(initParamsInfo, (err: BusinessError, textToSpeechEngine: textToSpeech.TextToSpeechEngine) => {
234.         if (!err) {
235.           console.info('createEngine is success');
236.           // 接收创建引擎的实例
237.           ttsEngine = textToSpeechEngine;
238.         } else {
239.           console.error(`error code: ${err.code}, message: ${err.message}.`)
240.         }
241.       });
242.     } catch (error) {
243.       let message = (error as BusinessError).message;
244.       let code = (error as BusinessError).code;
245.       console.error(`createEngine failed, error code: ${code}, message: ${message}.`)
246.     }
247.   }

248.   // 调用speak播报方法
249.   private speak() {
250.     let speakListener: textToSpeech.SpeakListener = {
251.       // 开始播报回调
252.       onStart(requestId: string, response: textToSpeech.StartResponse) {
253.         console.info(`onStart, requestId: ${requestId} response: ${JSON.stringify(response)}`);
254.       },
255.       // 完成播报回调
256.       onComplete(requestId: string, response: textToSpeech.CompleteResponse) {
257.         console.info(`onComplete, requestId: ${requestId} response: ${JSON.stringify(response)}`);
258.       },
259.       // 停止播报完成回调，调用stop方法并完成时会触发此回调
260.       onStop(requestId: string, response: textToSpeech.StopResponse) {
261.         console.info(`onStop, requestId: ${requestId} response: ${JSON.stringify(response)}`);
262.       },
263.       // 返回音频流
264.       onData(requestId: string, audio: ArrayBuffer, response: textToSpeech.SynthesisResponse) {
265.         console.info(`onData, requestId: ${requestId} sequence: ${JSON.stringify(response)} audio: ${JSON.stringify(audio)}`);
266.       },
267.       // 错误回调，播报过程发生错误时触发此回调
268.       onError(requestId: string, errorCode: number, errorMessage: string) {
269.         if (errorCode === 1002300007) {
270.           engineCreated = false
271.         }
272.         console.error(`onError, requestId: ${requestId} errorCode: ${errorCode} errorMessage: ${errorMessage}`);
273.       }
274.     };
275.     // 设置回调
276.     ttsEngine.setListener(speakListener);
277.     // 设置播报相关参数
278.     let extraParam: Record<string, Object> = {"queueMode": 0, "speed": 1, "volume": 2, "pitch": 1, "languageContext": 'zh-CN', "audioType": "pcm", "soundChannel": 3, "playType":1}
279.     let speakParams: textToSpeech.SpeakParams = {
280.       requestId: '123456' + Date.now(), // requestId在同一实例内仅能用一次，请勿重复设置
281.       extraParams: extraParam
282.     };
283.     // 调用speak播报方法
284.     ttsEngine.speak(this.originalText, speakParams);
285.   };

286.   private onStart = async (utteranceId: string, response: textToSpeech.StartResponse) => {
287.     bufferLength = 0;
288.     // 初始化音频数据映射
289.     console.info(TAG, `onStart | utteranceId: ${ utteranceId }, response: ${JSON.stringify(response)}`);
290.   }

291.   private onData = async (utteranceId: string, audio: ArrayBuffer, response: textToSpeech.SynthesisResponse) => {
292.     // 将ArrayBuffer转换为Uint8Array
293.     let uint8Array: Uint8Array = new Uint8Array(audio);
294.     this.pcmData.set(response.sequence, uint8Array)
295.     bufferLength += 1
296.     let str = ""
297.     // 或者使用循环打印每个元素
298.     for (let i = 0; i < uint8Array.length; i++) {
299.       str = str + (","+uint8Array[i]);
300.     }
301.     console.info(TAG, `onData | utteranceId: ${utteranceId}, sequence: ${JSON.stringify(response.sequence)}, length: ${uint8Array.length}, audio: ${JSON.stringify(str)}`);
302.   }

303.   private onComplete = async (utteranceId: string, response: textToSpeech.CompleteResponse) => {
304.     let buffers: ArrayBuffer[] = new Array();

305.     console.info(TAG, `pcmData len: ${this.pcmData.length}`)
306.     // 遍历Map，将ArrayBuffer添加到数组中
307.     this.pcmData.forEach((value: Uint8Array, key: number) => {
308.       buffers.push(value.buffer.slice(0))
309.     })
310.     console.info(TAG, `buffers len: ${buffers.length}`)

311.     // 按照顺序拼接所有的ArrayBuffer
312.     let audioData = concatenateArrayBuffers(buffers);
313.     console.info(TAG, `audioData len: ${audioData.byteLength}`)

314.     let context = this.uiContext.getHostContext() as Context
315.     let path = context.filesDir
316.     let filePath: string = `${path}/my.pcm`
317.     let os = await fs.createStream(filePath, "w+")
318.     await os.write(audioData)
319.     this.pcmPlayer.file = fs.openSync(filePath, fs.OpenMode.READ_ONLY);
320.     // 播放音频流
321.     console.info(TAG, `playAudio start`)
322.     await this.pcmPlayer.prepare(audio.AudioSamplingRate.SAMPLE_RATE_16000)
323.     await this.pcmPlayer.play(audioData)
324.     console.info(TAG, `playAudio end`)

325.     console.info(TAG, `onComplete | utteranceId: ${utteranceId}, response: ${JSON.stringify(response)}`);
326.   }

327.   // 调用speakOnData播报方法
328.   // 未初始化引擎时调用speak方法，返回错误码1002300007，合成及播报失败
329.   private async speakOnData() {
330.     // 设置播报相关参数
331.     let extraParam: Record<string, Object> = {"queueMode": 0, "speed": 1.2, "volume": 2, "pitch": 1, "languageContext": 'zh-CN', "audioType": "pcm", "soundChannel": 1, "playType":0}
332.     let speakParams: textToSpeech.SpeakParams = {
333.       requestId: '1234567' + Date.now(),
334.       extraParams: extraParam
335.     }

336.     try{
337.       // 创建回调对象
338.       let speakListener: textToSpeech.SpeakListener = {
339.         // 开始识别成功回调
340.         onStart: this.onStart,
341.         // 识别完成回调
342.         onComplete: this.onComplete,
343.         // 停止播报回调
344.         onStop(utteranceId: string, response: textToSpeech.StopResponse) {
345.           console.info('speakListener onStop: ' + ' utteranceId: ' + utteranceId + ' response: ' + JSON.stringify(response));
346.         },
347.         // 返回音频流
348.         onData: this.onData,
349.         // 错误回调
350.         onError(utteranceId: string, errorCode: number, errorMessage: string) {
351.           if (errorCode === 1002300007) {
352.             engineCreated = false
353.           }
354.           console.error('speakListener onError: ' + ' utteranceId: ' + utteranceId + ' errorCode: ' + errorCode + ' errorMessage: ' + errorMessage);
355.         }
356.       };
357.       // 设置回调
358.       ttsEngine.setListener(speakListener);
359.       try{
360.         console.info(`speakListener before speak`)
361.         // 调用speak播报方法
362.         for (let i = 0; i < 1; i++) {
363.           ttsEngine?.speak(this.originalText, speakParams);
364.         }
365.         console.info(`speakListener after speak`)
366.       }catch (error) {
367.         let message = (error as BusinessError).message;
368.         let code = (error as BusinessError).code;
369.         console.error(`speakListener speak failed, error code: ${code}, message: ${message}.`)
370.       }
371.     }catch (error) {
372.       let message = (error as BusinessError).message;
373.       let code = (error as BusinessError).code;
374.       console.error(`speakListener setListener failed, error code: ${code}, message: ${message}.`)
375.     }
376.   }
377. }

### PcmPlayer.ets

1. import { audio } from '@kit.AudioKit';
2. import { fileIo as fs } from '@kit.CoreFileKit';

3. const TAG = 'PCM_audio';

4. class Options {
5.   offset?: number;
6.   length?: number;
7. }

8. export default class PcmPlayer {

9.   public file: fs.File | undefined;
10.   private writeDataCallback = (buffer: ArrayBuffer) => {
11.     let options: Options = {
12.       offset: this.bufferSize,
13.       length: buffer.byteLength
14.     };

15.     try {
16.       fs.readSync(this.file?.fd, buffer, options);
17.       this.bufferSize += buffer.byteLength;
18.       if (this.audioDataSize < this.bufferSize) {
19.         this.renderModel?.off('writeData');
20.         this.stop()
21.       }
22.       console.info(TAG, 'reading file success');
23.       // 系统会判定buffer有效，正常播放。
24.       return audio.AudioDataCallbackResult.VALID;
25.     } catch (error) {
26.       console.error(TAG, `Reading file failed, error code: ${error.code}, message: ${error.message}.`)
27.       // 系统会判定buffer无效，不播放。
28.       return audio.AudioDataCallbackResult.INVALID;
29.     }
30.   };
31.   /**
32.    * 缓存大小
33.    */
34.   private bufferSize: number = 0;
35.   /**
36.    * 音频总大小
37.    */
38.   private audioDataSize: number = 0;
39.   /**
40.    * 播放器
41.    */
42.   private renderModel: audio.AudioRenderer | null = null;
43.   /**
44.    * 播放状态
45.    */
46.   private audioStreamInfo: audio.AudioStreamInfo = {
47.     samplingRate: audio.AudioSamplingRate.SAMPLE_RATE_16000, // 采样率
48.     channels: audio.AudioChannel.CHANNEL_1, // 通道
49.     sampleFormat: audio.AudioSampleFormat.SAMPLE_FORMAT_S16LE, // 采样格式
50.     encodingType: audio.AudioEncodingType.ENCODING_TYPE_RAW // 编码格式
51.   }
52.   private audioRendererInfo: audio.AudioRendererInfo = {
53.     usage: audio.StreamUsage.STREAM_USAGE_ACCESSIBILITY, // 音频流使用类型
54.     rendererFlags: 0 // 音频渲染器标志
55.   }
56.   private audioRendererOptions: audio.AudioRendererOptions = {
57.     streamInfo: this.audioStreamInfo,
58.     rendererInfo: this.audioRendererInfo
59.   }

60.   public async prepare(sampleRate: number) {
61.     this.audioRendererOptions.streamInfo.samplingRate = sampleRate;
62.     this.audioRendererOptions.rendererInfo.usage = audio.StreamUsage.STREAM_USAGE_MUSIC;
63.     if (this.renderModel != null) {
64.       await this.renderModel.release();
65.     }
66.     let renderModel = await audio.createAudioRenderer(this.audioRendererOptions);
67.     if (!renderModel) {
68.       console.error(TAG, `failed to create audio renderer`);
69.     }
70.     console.info(TAG, "creating AudioRenderer success");
71.     this.renderModel = renderModel;
72.     this.bufferSize = await this.renderModel.getBufferSize();
73.   }

74.   public async play(data: ArrayBuffer): Promise<number> {
75.     this.audioDataSize = data.byteLength
76.     if (this.renderModel != null) {
77.       this.renderModel.on('writeData', this.writeDataCallback);
78.       // 启动渲染
79.       await this.renderModel.start();
80.       console.info(TAG, "start AudioRenderer success");
81.     }
82.     return -1;
83.   }

84.   public async stop() {
85.     console.info(TAG, 'Renderer begin stop');
86.     if (this.renderModel == null) {
87.       return;
88.     }

89.     // 只有渲染器状态为running或paused的时候才可以停止
90.     if (this.renderModel.state !== audio.AudioState.STATE_RUNNING
91.       && this.renderModel.state !== audio.AudioState.STATE_PAUSED) {
92.       console.error(TAG, 'Renderer is not running or paused');
93.       return;
94.     }
95.     await this.renderModel.stop(); // 停止渲染
96.     console.info(TAG, 'Renderer stopped');
97.   }

98.   public async release() {
99.     // 渲染器状态不是released状态，才能release
100.     if (this.renderModel != null) {
101.       if (this.renderModel.state === audio.AudioState.STATE_RELEASED) {
102.         console.error(TAG, 'Renderer already released');
103.         return;
104.       }
105.       await this.renderModel.release(); // 释放资源
106.       this.renderModel = null;
107.       console.info(TAG, 'Renderer released');
108.     }
109.   }

110.   /**
111.    * 判断当前渲染状态
112.    *
113.    * @returns running返回true，否则返回false
114.    */
115.   public isPlaying() {
116.     if (this.renderModel != null) {
117.       console.info(TAG, "player.state:" + this.renderModel.state);
118.       return this.renderModel.state == audio.AudioState.STATE_RUNNING;
119.     } else {
120.       return false;
121.     }
122.   }

123.   /**
124.    * 获取当前渲染状态
125.    *
126.    * @returns running返回true，否则返回false
127.    */
128.   public getRenderState(): number {
129.     if (this.renderModel != null) {
130.       console.info(TAG, "player.state:" + this.renderModel.state);
131.       return this.renderModel.state;
132.     } else {
133.       return audio.AudioState.STATE_INVALID;
134.     }
135.   }

136.   /**
137.    * 获取音频渲染器的最小缓冲区大小
138.    */
139.   public getBufferSize(): number {
140.     return this.bufferSize;
141.   }
142. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/core-speech-introduction "Core Speech Kit简介")
# 语音识别

更新时间: 2025-12-16 16:27

将一段中文音频信息（中文、中文语境下的英文；短语音模式不超过60s，长语音模式不超过8h）转换为文本，音频信息可以为PCM音频文件或者实时语音。

## 场景介绍

手机/平板等设备在无网状态下，为听障人士或不方便收听音频场景提供音频转文本能力。

## 约束与限制

|AI能力|约束|
|:--|:--|
|语音识别|- 支持的语种类型：中文普通话。<br>- 支持的模型类型：离线。<br>- 语音时长：短语音模式不超过60s，长语音模式不超过8h。|

## 开发步骤

1. 在使用语音识别时，将实现语音识别相关的类添加至工程。
    
    1. import { speechRecognizer } from '@kit.CoreSpeechKit';
    2. import { BusinessError } from '@kit.BasicServicesKit';
    
2. 调用[createEngine](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/hms-ai-speechrecognizer#section53411946183318)方法，对引擎进行初始化，并创建[SpeechRecognitionEngine](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/hms-ai-speechrecognizer#section153101728203110)实例。
    
    createEngine方法提供了两种调用形式，当前以其中一种作为示例，其他方式可参考[API参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/hms-ai-speechrecognizer)。
    
    1. let asrEngine: speechRecognizer.SpeechRecognitionEngine;
    2. let sessionId: string = '123456';
    3. // 创建引擎，通过callback形式返回
    4. // 设置创建引擎参数
    5. let extraParam: Record<string, Object> = {"locate": "CN", "recognizerMode": "short"};
    6. let initParamsInfo: speechRecognizer.CreateEngineParams = {
    7.   language: 'zh-CN',
    8.   online: 1,
    9.   extraParams: extraParam
    10. };
    11. // 调用createEngine方法
    12. speechRecognizer.createEngine(initParamsInfo, (err: BusinessError, speechRecognitionEngine: speechRecognizer.SpeechRecognitionEngine) => {
    13.   if (!err) {
    14.     console.info('Succeeded in creating engine.');
    15.     // 接收创建引擎的实例
    16.     asrEngine = speechRecognitionEngine;
    17.   } else {
    18.     console.error(`Failed to create engine. Code: ${err.code}, message: ${err.message}.`);
    19.   }
    20. });
    
3. 得到[SpeechRecognitionEngine](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/hms-ai-speechrecognizer#section153101728203110)实例对象后，实例化[RecognitionListener](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/hms-ai-speechrecognizer#section845815011389)对象，调用[setListener](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/hms-ai-speechrecognizer#section1745872517348)方法设置回调，用来接收语音识别相关的回调信息。
    
    1. // 创建回调对象
    2. let setListener: speechRecognizer.RecognitionListener = {
    3.   // 开始识别成功回调
    4.   onStart(sessionId: string, eventMessage: string) {
    5.     console.info(`onStart, sessionId: ${sessionId} eventMessage: ${eventMessage}`);
    6.   },
    7.   // 事件回调
    8.   onEvent(sessionId: string, eventCode: number, eventMessage: string) {
    9.     console.info(`onEvent, sessionId: ${sessionId} eventCode: ${eventCode} eventMessage: ${eventMessage}`);
    10.   },
    11.   // 识别结果回调，包括中间结果和最终结果
    12.   onResult(sessionId: string, result: speechRecognizer.SpeechRecognitionResult) {
    13.     console.info(`onResult, sessionId: ${sessionId} result: ${JSON.stringify(result)}`);
    14.   },
    15.   // 识别完成回调
    16.   onComplete(sessionId: string, eventMessage: string) {
    17.     console.info(`onComplete, sessionId: ${sessionId} eventMessage: ${eventMessage}`);
    18.   },
    19.   // 错误回调，错误码通过本方法返回
    20.   // 返回错误码1002200002，开始识别失败，重复启动startListening方法时触发
    21.   // 更多错误码请参考[错误码参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/errorcode-corespeech)
    22.   onError(sessionId: string, errorCode: number, errorMessage: string) {
    23.     console.error(`onError, sessionId: ${sessionId} errorCode: ${errorCode} errorMessage: ${errorMessage}`);
    24.   },
    25. }
    26. // 设置回调
    27. asrEngine.setListener(setListener);
    
4. 分别为音频文件转文字和麦克风转文字功能设置开始识别的相关参数，调用[startListening](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/hms-ai-speechrecognizer#section140216144119)方法，开始识别。
    
    1. private startListeningForRecording() {
    2.   let audioParam: speechRecognizer.AudioInfo = { audioType: 'pcm', sampleRate: 16000, soundChannel: 1, sampleBit: 16 }// audioInfo参数配置请参考[AudioInfo](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/hms-ai-speechrecognizer#section85771521101910)
    3.   let extraParam: Record<string, Object> = {
    4.     "recognitionMode": 0,
    5.     "vadBegin": 2000,
    6.     "vadEnd": 3000,
    7.     "maxAudioDuration": 20000
    8.   }
    9.   let recognizerParams: speechRecognizer.StartParams = {
    10.     sessionId: this.sessionId,
    11.     audioInfo: audioParam,
    12.     extraParams: extraParam
    13.   }
    14.   console.info('startListening start');
    15.   asrEngine.startListening(recognizerParams);
    16. };
    
5. 传入音频流，调用[writeAudio](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/hms-ai-speechrecognizer#section72131731149)方法，开始写入音频流。读取音频文件时，开发者需预先准备一个pcm格式音频文件。
    
    1. let uint8Array: Uint8Array = new Uint8Array();
    2. // 可以通过如下方式获取音频流：1、通过录音获取音频流；2、从音频文件中读取音频流
    3. // 两种方式示例均已实现:[demo参考](https://developer.huawei.com/consumer/cn/doc/#section56481271497)
    4. // 写入音频流，音频流长度仅支持640或1280
    5. asrEngine.writeAudio(sessionId, uint8Array);
    
    注意
    
    6. 如需通过录音获取音频流，请打开麦克风权限，参考[步骤10](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/speechrecognizer-guide#li1723555443715)配置相关权限。
    
    7. 如需从音频文件中读取音频流，请在项目中的main\resources\resfile路径下存放pcm文件。
    
6. （可选）当需要查询语音识别服务支持的语种信息，可调用[listLanguages](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/hms-ai-speechrecognizer#section813761871119)方法。
    
    listLanguages方法提供了两种调用形式，当前以其中一种作为示例，其他方式可参考[API参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/hms-ai-speechrecognizer)。
    
    1. // 设置查询相关的参数
    2. let languageQuery: speechRecognizer.LanguageQuery = {
    3.   sessionId: sessionId
    4. };
    5. // 调用listLanguages方法
    6. asrEngine.listLanguages(languageQuery).then((res: Array<string>) => {
    7.   console.info(`Succeeded in listing languages.`);
    8. }).catch((err: BusinessError) => {
    9.   console.error(`Failed to list languages. Code: ${err.code}, message: ${err.message}.`);
    10. });
    
7. （可选）当需要结束识别时，可调用[finish](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/hms-ai-speechrecognizer#section14433919171116)方法。
    
    1. // 结束识别
    2. asrEngine.finish(sessionId);
    
8. （可选）当需要取消识别时，可调用[cancel](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/hms-ai-speechrecognizer#section3235541759)方法。
    
    1. // 取消识别
    2. asrEngine.cancel(sessionId);
    
9. （可选）当需要释放语音识别引擎资源时，可调用[shutdown](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/hms-ai-speechrecognizer#section444415855615)方法。
    
    1. // 释放识别引擎资源
    2. asrEngine.shutdown();
    
10. 需要在[module.json5配置文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file)中添加ohos.permission.MICROPHONE权限，确保麦克风使用正常。详细步骤可查看[声明权限](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/declare-permissions)章节。
    
    1. // ...
    2. "requestPermissions": [
    3.   {
    4.     "name" : "ohos.permission.MICROPHONE",
    5.     "reason": "$string:reason",
    6.     "usedScene": {
    7.       "abilities": [
    8.         "EntryAbility"
    9.       ],
    10.       "when":"inuse"
    11.     }
    12.   }
    13. ],
    14. // ...
    

## 开发实例

点击按钮，将一段音频信息转换为文本。

### Index.ets

1. import { speechRecognizer } from '@kit.CoreSpeechKit';
2. import { BusinessError } from '@kit.BasicServicesKit';
3. import { fileIo } from '@kit.CoreFileKit';
4. import { PromptAction } from '@kit.ArkUI';
5. import FileCapturer from './FileCapturer';

6. const TAG = 'AsrDemo';

7. let asrEngine: speechRecognizer.SpeechRecognitionEngine;

8. @Entry
9. @Component
10. struct Index {
11.   @State createCount: number = 0;
12.   @State result: boolean = false;
13.   @State voiceInfo: string = "";
14.   @State sessionId: string = "123456";
15.   @State sessionId2: string = "1234567";
16.   @State generatedText: string = "Default Text";
17.   @State uiContext: UIContext = this.getUIContext()
18.   @State promptAction: PromptAction = this.uiContext.getPromptAction();

19.   private mFileCapturer: FileCapturer = new FileCapturer();

20.   build() {
21.     Column() {
22.       Scroll() {
23.         Column() {
24.           Row() {
25.             Column() {
26.               Text(this.generatedText)
27.                 .fontColor($r('sys.color.ohos_id_color_text_secondary'))
28.             }
29.             .width('100%')
30.             .constraintSize({ minHeight: 100 })
31.             .border({ width: 1, radius: 5 })
32.             .backgroundColor('#d3d3d3')
33.             .padding(20)
34.             .alignItems(HorizontalAlign.Start)
35.           }
36.           .width('100%')
37.           .padding({ left: 20, right: 20, top: 20, bottom: 20 })

38.           Button() {
39.             Text("CreateEngineByCallback")
40.               .fontColor(Color.White)
41.               .fontSize(20)
42.           }
43.           .type(ButtonType.Capsule)
44.           .backgroundColor("#0x317AE7")
45.           .width("80%")
46.           .height(50)
47.           .margin(10)
48.           .onClick(async () => {
49.             this.createByCallback();
50.             this.createCount++;
51.             console.info(TAG, `CreateAsrEngine：createCount:${this.createCount}`);
52.             await this.sleep(500);
53.             this.setListener();
54.             this.promptAction.showToast({
55.               message: 'CreateEngine succeeded!',
56.               duration: 2000
57.             });
58.           })

59.           Button() {
60.             Text("startRecording")
61.               .fontColor(Color.White)
62.               .fontSize(20)
63.           }
64.           .type(ButtonType.Capsule)
65.           .backgroundColor("#0x317AE7")
66.           .width("80%")
67.           .height(50)
68.           .margin(10)
69.           .onClick(() => {
70.             this.startRecording();
71.             this.promptAction.showToast({
72.               message: 'start Recording',
73.               duration: 2000
74.             });
75.           })

76.           Button() {
77.             Text("audioToText")
78.               .fontColor(Color.White)
79.               .fontSize(20)
80.           }
81.           .type(ButtonType.Capsule)
82.           .backgroundColor("#0x317AE7")
83.           .width("80%")
84.           .height(50)
85.           .margin(10)
86.           .onClick(() => {
87.             this.audioToText();
88.             this.promptAction.showToast({
89.               message: 'start audioToText',
90.               duration: 2000
91.             });
92.           })

93.           Button() {
94.             Text("queryLanguagesCallback")
95.               .fontColor(Color.White)
96.               .fontSize(20)
97.           }
98.           .type(ButtonType.Capsule)
99.           .backgroundColor("#0x317AE7")
100.           .width("80%")
101.           .height(50)
102.           .margin(10)
103.           .onClick(() => {
104.             try{
105.               this.queryLanguagesCallback();
106.               this.promptAction.showToast({
107.                 message: 'queryLanguages succeeded!',
108.                 duration: 2000
109.               });
110.             } catch (err) {
111.               this.generatedText = `Failed to query language information. message: ${err.message}.`
112.               this.promptAction.showToast({
113.                 message: 'queryLanguages failed!',
114.                 duration: 2000
115.               });
116.             }
117.           })

118.           Button() {
119.             Text("shutdown")
120.               .fontColor(Color.White)
121.               .fontSize(20)
122.           }
123.           .type(ButtonType.Capsule)
124.           .backgroundColor("#0x317AA7")
125.           .width("80%")
126.           .height(50)
127.           .margin(10)
128.           .onClick(() => {
129.             // 释放引擎
130.             try{
131.               asrEngine.shutdown();
132.               this.generatedText = `The engine has been released.`
133.               this.promptAction.showToast({
134.                 message: 'shutdown succeeded!',
135.                 duration: 2000
136.               });
137.             } catch (err) {
138.               this.generatedText = `Failed to release engine. message: ${err.message}.`
139.               this.promptAction.showToast({
140.                 message: 'shutdown failed!',
141.                 duration: 2000
142.               });
143.             }
144.           })
145.         }
146.         .layoutWeight(1)
147.       }
148.       .width('100%')
149.       .height('100%')

150.     }
151.   }

152.   // 创建引擎，通过callback形式返回
153.   private createByCallback() {
154.     // 设置创建引擎参数
155.     let extraParam: Record<string, Object> = {"locate": "CN", "recognizerMode": "short"};
156.     let initParamsInfo: speechRecognizer.CreateEngineParams = {
157.       language: 'zh-CN',
158.       online: 1,
159.       extraParams: extraParam
160.     };

161.     // 调用createEngine方法
162.     speechRecognizer.createEngine(initParamsInfo, (err: BusinessError, speechRecognitionEngine:
163.       speechRecognizer.SpeechRecognitionEngine) => {
164.       if (!err) {
165.         console.info(TAG, 'succeeded in creating engine.');
166.         // 接收创建引擎的实例
167.         asrEngine = speechRecognitionEngine;
168.       } else {
169.         // 无法创建引擎时返回错误码1002200001，原因：语种不支持、模式不支持、初始化超时、资源不存在等导致创建引擎失败
170.         // 无法创建引擎时返回错误码1002200006，原因：引擎正在忙碌中，一般多个应用同时调用语音识别引擎时触发
171.         // 无法创建引擎时返回错误码1002200008，原因：引擎已被销毁
172.         console.error(TAG, `Failed to create engine. Message: ${err.message}.`);
173.       }
174.     });
175.   }

176.   // 查询语种信息，以callback形式返回
177.   private queryLanguagesCallback() {
178.     // 设置查询相关参数
179.     let languageQuery: speechRecognizer.LanguageQuery = {
180.       sessionId: this.sessionId
181.     };
182.     // 调用listLanguages方法
183.     asrEngine.listLanguages(languageQuery, (err: BusinessError, languages: Array<string>) => {
184.       if (!err) {
185.         // 接收目前支持的语种信息
186.         console.info(TAG, `succeeded in listing languages, result: ${JSON.stringify(languages)}`);
187.         this.generatedText = `languages result: ${JSON.stringify(languages)}`
188.       } else {
189.         console.error(TAG, `Failed to create engine. Message: ${err.message}.`);
190.         this.generatedText = `Failed to create engine. Message: ${err.message}.`
191.       }
192.     });
193.   };

194.   private startListeningForRecording() {
195.     let audioParam: speechRecognizer.AudioInfo = { audioType: 'pcm', sampleRate: 16000, soundChannel: 1, sampleBit: 16 } // audioInfo参数配置请参考[AudioInfo](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/hms-ai-speechrecognizer#section85771521101910)
196.     let extraParam: Record<string, Object> = {
197.       "recognitionMode": 0,
198.       "vadBegin": 2000,
199.       "vadEnd": 3000,
200.       "maxAudioDuration": 20000
201.     }
202.     let recognizerParams: speechRecognizer.StartParams = {
203.       sessionId: this.sessionId,
204.       audioInfo: audioParam,
205.       extraParams: extraParam
206.     }
207.     console.info(TAG, 'startListening start');
208.     asrEngine.startListening(recognizerParams);
209.   };

210.   // 写音频流
211.   private async audioToText() {
212.     try {
213.       this.setListener();
214.       // Set the parameters related to the start of identification.
215.       let audioParam: speechRecognizer.AudioInfo = { audioType: 'pcm', sampleRate: 16000, soundChannel: 1, sampleBit: 16 }
216.       let recognizerParams: speechRecognizer.StartParams = {
217.         sessionId: this.sessionId2,
218.         audioInfo: audioParam
219.       }
220.       // Invoke the start recognition method.
221.       asrEngine.startListening(recognizerParams);

222.       // Get Audio from File
223.       let data: ArrayBuffer;
224.       let ctx = this.getUIContext().getHostContext() as Context;
225.       let filenames: string[] = fileIo.listFileSync(ctx.resourceDir);
226.       if (filenames.length <= 0) {
227.         console.error('length is null');
228.         return;
229.       }
230.       let filePath: string = ctx.resourceDir + '/' + filenames[0];
231.       (this.mFileCapturer as FileCapturer).setFilePath(filePath);
232.       this.mFileCapturer.init((dataBuffer: ArrayBuffer) => {
233.         data = dataBuffer
234.         let uint8Array: Uint8Array = new Uint8Array(data);
235.         asrEngine.writeAudio(this.sessionId2, uint8Array);
236.       });
237.       await this.mFileCapturer.start();
238.       asrEngine?.finish(this.sessionId);
239.       this.mFileCapturer.release();
240.     } catch (err) {
241.       this.generatedText = `Message: ${err.message}.`
242.     }
243.   }

244.   // 麦克风语音转文本
245.   private async startRecording() {
246.     try {
247.       this.startListeningForRecording();
248.     } catch (err) {
249.       this.generatedText = `Message: ${err.message}.`;
250.     }
251.   };

252.   // 睡眠
253.   private sleep(ms: number):Promise<void> {
254.     return new Promise(resolve => setTimeout(resolve, ms));
255.   }

256.   // 设置回调
257.   private setListener() {
258.     // 创建回调对象
259.     let setListener: speechRecognizer.RecognitionListener = {
260.       // 开始识别成功回调
261.       onStart: (sessionId: string, eventMessage: string) => {
262.         this.generatedText = '';
263.         console.info(TAG, `onStart, sessionId: ${sessionId} eventMessage: ${eventMessage}`);
264.       },
265.       // 事件回调
266.       onEvent(sessionId: string, eventCode: number, eventMessage: string) {
267.         console.info(TAG, `onEvent, sessionId: ${sessionId} eventCode: ${eventCode} eventMessage: ${eventMessage}`);
268.       },
269.       // 识别结果回调，包括中间结果和最终结果
270.       onResult: (sessionId: string, result: speechRecognizer.SpeechRecognitionResult) => {
271.         console.info(TAG, `onResult, sessionId: ${sessionId} result: ${JSON.stringify(result)}`);
272.         this.generatedText = result.result;
273.       },
274.       // 识别完成回调
275.       onComplete(sessionId: string, eventMessage: string) {
276.         console.info(TAG, `onComplete, sessionId: ${sessionId} eventMessage: ${eventMessage}`);
277.       },
278.       // 错误回调，错误码通过本方法返回
279.       // 返回错误码1002200002，开始识别失败，重复启动startListening方法时触发
280.       // 更多错误码请参考[错误码参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/errorcode-corespeech)
281.       onError(sessionId: string, errorCode: number, errorMessage: string) {
282.         console.error(TAG, `onError, sessionId: ${sessionId} errorCode: ${errorCode} errorMessage: ${errorMessage}`);
283.       },
284.     }
285.     // 设置回调
286.     asrEngine.setListener(setListener);
287.   };
288. }

### FileCapturer.ets

添加FileCapturer.ets文件用于pcm文件音频流。

1. import { fileIo } from '@kit.CoreFileKit';

2. const TAG = 'FileCapturer';
3. const SEND_SIZE: number = 1280;

4. /**
5.  * File collector tool
6.  */
7. export default class FileCapturer {
8.   /**
9.    * Whether the audio is being written
10.    */
11.   private mIsWriting: boolean = false;

12.   /**
13.    * File Path
14.    */
15.   private mFilePath: string = '';

16.   /**
17.    * Open File Object
18.    */
19.   private mFile: fileIo.File | null = null;

20.   /**
21.    * Indicates whether the file can be read.
22.    */
23.   private mIsReadFile: boolean = true;

24.   /**
25.    * Audio Data Callback Method
26.    */
27.   private mDataCallBack: ((data: ArrayBuffer) => void ) | null = null;

28.   /**
29.    * Setting the File Path
30.    * @param filePath
31.    */
32.   public setFilePath(filePath: string) {
33.     this.mFilePath = filePath;
34.   }

35.   async init(dataCallBack: (data: ArrayBuffer) => void): Promise<void> {
36.     if (null != this.mDataCallBack) {
37.       return;
38.     }
39.     this.mDataCallBack = dataCallBack;
40.     if (!fileIo.accessSync(this.mFilePath)) {
41.       return
42.     }
43.     console.error(TAG, "init start ");
44.   }

45.   async start(): Promise<void> {
46.     try {
47.       if (this.mIsWriting || null == this.mDataCallBack) {
48.         return;
49.       }
50.       this.mIsWriting = true;
51.       this.mIsReadFile = true;
52.       this.mFile = fileIo.openSync(this.mFilePath, fileIo.OpenMode.READ_ONLY);
53.       let buf: ArrayBuffer = new ArrayBuffer(SEND_SIZE);
54.       let offset: number = 0;
55.       let count = 0;
56.       while (SEND_SIZE == fileIo.readSync(this.mFile.fd, buf, {
57.         offset: offset
58.       }) && this.mIsReadFile) {
59.         this.mDataCallBack(buf);
60.         ++count;
61.         await sleep(40);
62.         offset = offset + SEND_SIZE;
63.       }
64.     } catch (e) {
65.       console.error(TAG, "read file error " + e);
66.     } finally {
67.       if (null != this.mFile) {
68.         fileIo.closeSync(this.mFile);
69.       }
70.       this.mIsWriting = false;
71.     }
72.   }

73.   stop() {
74.     if (null == this.mDataCallBack) {
75.       return;
76.     }
77.     try {
78.       this.mIsReadFile = false;
79.     } catch (e) {
80.       console.error(TAG, "read file error " + e);
81.     }
82.   }

83.   release() {
84.     if (null == this.mDataCallBack) {
85.       return;
86.     }
87.     try {
88.       this.mDataCallBack = null;
89.       this.mIsReadFile = false;
90.     } catch (e) {
91.       console.error(TAG, "read file error " + e);
92.     }
93.   }
94. }

95. function sleep(ms: number): Promise<void> {
96.   return new Promise<void>(resolve => setTimeout(resolve, ms));
97. }

### EntryAbility.ets

在EntryAbility.ets文件中添加麦克风权限。

1. import { abilityAccessCtrl, AbilityConstant, UIAbility, Want } from '@kit.AbilityKit';
2. import { hilog } from '@kit.PerformanceAnalysisKit';
3. import { window } from '@kit.ArkUI';
4. import { BusinessError } from '@kit.BasicServicesKit';

5. export default class EntryAbility extends UIAbility {
6.   onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void {
7.     hilog.info(0x0000, 'testTag', '%{public}s', 'Ability onCreate');
8.   }

9.   onDestroy(): void {
10.     hilog.info(0x0000, 'testTag', '%{public}s', 'Ability onDestroy');
11.   }

12.   onWindowStageCreate(windowStage: window.WindowStage): void {
13.     // Main window is created, set main page for this ability
14.     hilog.info(0x0000, 'testTag', '%{public}s', 'Ability onWindowStageCreate');

15.     let atManager = abilityAccessCtrl.createAtManager();
16.     atManager.requestPermissionsFromUser(this.context, ['ohos.permission.MICROPHONE']).then((data) => {
17.       hilog.info(0x0000, 'testTag', 'data:' + JSON.stringify(data));
18.       hilog.info(0x0000, 'testTag', 'data permissions:' + data.permissions);
19.       hilog.info(0x0000, 'testTag', 'data authResults:' + data.authResults);
20.     }).catch((err: BusinessError) => {
21.       hilog.error(0x0000, 'testTag', 'errCode: ' + err.code + 'errMessage: ' + err.message);
22.     });

23.     windowStage.loadContent('pages/Index', (err, data) => {
24.       if (err.code) {
25.         hilog.error(0x0000, 'testTag', 'Failed to load the content. Cause: %{public}s', JSON.stringify(err) ?? '');
26.         return;
27.       }
28.       hilog.info(0x0000, 'testTag', 'Succeeded in loading the content. Data: %{public}s', JSON.stringify(data) ?? '');
29.     });
30.   }

31.   onWindowStageDestroy(): void {
32.     // Main window is destroyed, release UI related resources
33.     hilog.info(0x0000, 'testTag', '%{public}s', 'Ability onWindowStageDestroy');
34.   }

35.   onForeground(): void {
36.     // Ability has brought to foreground
37.     hilog.info(0x0000, 'testTag', '%{public}s', 'Ability onForeground');
38.   }

39.   onBackground(): void {
40.     // Ability has back to background
41.     hilog.info(0x0000, 'testTag', '%{public}s', 'Ability onBackground');
42.   }
43. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/texttospeech-guide "文本转语音")
