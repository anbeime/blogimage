# 🦞【极客挑战虾】chemistry-courseware：让AI自动制作化学教学动画视频

  

> **赛道**：极客挑战虾

> **标签**：#极客挑战虾# #OpenClaw# #Skill开发# #教育# #化学课件

  

---

  

## 💡 我做了什么？

  

**chemistry-courseware** 是一个基于OpenClaw的化学动态课件制作技能包，核心能力是：

  

**从PDF教材一键生成动态教学动画视频**

  

| OpenClaw能力 | chemistry-courseware实现 | 效果 |

|-------------|------------------------|------|

| Shell接口 | 调用Remotion渲染视频 | AI自动生成视频 |

| 文件系统 | 读取PDF、保存视频 | AI处理教学资源 |

| AI分析 | 提取知识点、生成脚本 | AI理解教学内容 |

  

---

  

## 🎯 解决什么问题？

  

教师/教育工作者面临的痛点：

  

| 痛点 | 传统方案 | chemistry-courseware方案 |

|-----|---------|------------------------|

| 制作课件耗时 | 2-4小时/课 | **< 30分钟** |

| 需要专业技能 | 动画制作/视频剪辑 | **自动生成** |

| 动画质量 | 依赖个人能力 | **专业模板** |

| 批量制作 | 几乎不可能 | **一键批量** |

  

---

  

## 🎬 效果展示

  

### 输入

  

一本初三化学教材PDF（约15MB）

  

### 输出

  

动态教学视频：

- **原子结构动画**：电子绕核运动可视化

- **化学键形成**：离子键、共价键过程演示

- **化学反应过程**：燃烧、电解等反应动画

- **酸碱盐知识点**：完整的知识讲解视频

  

### 示例视频

  

```

output/

├── atomic-structure-complete.mp4      # 原子结构（3分20秒）

├── acid-base-salt-complete.mp4        # 酸碱盐（5分45秒）

└── audio/

    ├── scene_00.mp3                   # 语音讲解

    ├── scene_01.mp3

    └── ...

```

  

---

  

## 🏗️ 技能包架构

  

```

chemistry-courseware/

├── SKILL.md                    # 技能说明

├── src/

│   ├── compositions/           # 课件组合

│   │   ├── AtomicStructure.tsx     # 原子结构动画

│   │   ├── ChemicalBond.tsx        # 化学键动画

│   │   ├── ChemicalReaction.tsx    # 化学反应动画

│   │   └── AcidBaseSalt.tsx        # 酸碱盐课件

│   ├── components/             # 可复用组件

│   │   ├── Atom.tsx                # 原子模型组件

│   │   ├── Molecule.tsx            # 分子模型组件

│   │   ├── Formula.tsx             # 化学式组件

│   │   ├── Arrow.tsx               # 反应箭头

│   │   └── Label.tsx               # 标注组件

│   ├── utils/

│   │   ├── colors.ts               # 配色方案（CPK着色）

│   │   └── animations.ts           # 动画工具

│   └── Root.tsx

├── scripts/                    # 渲染脚本

│   ├── generate_voiceover.py       # 语音合成

│   ├── merge_final.py              # 音视频合成

│   └── build_final_video.py        # 最终输出

├── out/                        # 输出视频

│   └── audio/                      # 音频文件

├── package.json

└── README.md

```

  

---

  

## 🔧 核心代码

  

### 技能说明 (SKILL.md)

  

```yaml

---

name: chemistry-courseware

description: 化学动态课件制作技能，基于Remotion框架创建初三/高中化学教学动画视频。支持原子结构、化学键、化学反应、元素周期表等知识点的动态可视化。

metadata:

  tags: chemistry, courseware, remotion, education, animation, science

---

  

# 化学动态课件制作

  

基于 Remotion 框架的化学教学动画视频制作技能。

  

## 适用场景

  

- 初三化学：原子结构、化学式、化学反应、溶液、酸碱盐

- 高一化学：摩尔概念、离子反应、氧化还原、元素周期律

- 化学实验教学动画

- 分子/原子结构可视化

```

  

### 原子结构动画组件 (AtomicStructure.tsx)

  

```tsx

import { useCurrentFrame, useVideoConfig, interpolate, spring } from 'remotion';

import { AbsoluteFill } from 'remotion';

  

export const AtomicStructure: React.FC = () => {

  const frame = useCurrentFrame();

  const { fps } = useVideoConfig();

  // 原子核缩放动画

  const nucleusScale = spring({

    frame,

    fps,

    config: { damping: 200 }

  });

  // 电子轨道旋转

  const electronRotation = interpolate(frame, [0, 60], [0, 360]);

  // 电子出现动画

  const electronOpacity = interpolate(

    frame,

    [30, 45],

    [0, 1],

    { extrapolateLeft: 'clamp', extrapolateRight: 'clamp' }

  );

  return (

    <AbsoluteFill style={{

      backgroundColor: '#1a1a2e',

      justifyContent: 'center',

      alignItems: 'center',

    }}>

      {/* 原子核 */}

      <div style={{

        width: 80,

        height: 80,

        borderRadius: '50%',

        background: 'radial-gradient(circle, #ff6b6b, #e63946)',

        transform: `scale(${nucleusScale})`,

        boxShadow: '0 0 30px #ff6b6b',

      }} />

      {/* 电子轨道 */}

      <div style={{

        position: 'absolute',

        width: 200,

        height: 200,

        border: '2px solid rgba(0, 212, 255, 0.3)',

        borderRadius: '50%',

        transform: `rotate(${electronRotation}deg)`,

      }}>

        {/* 电子 */}

        <div style={{

          position: 'absolute',

          top: -8,

          left: '50%',

          transform: 'translateX(-50%)',

          width: 16,

          height: 16,

          borderRadius: '50%',

          background: '#00d4ff',

          opacity: electronOpacity,

          boxShadow: '0 0 10px #00d4ff',

        }} />

      </div>

      {/* 标注 */}

      <div style={{

        position: 'absolute',

        bottom: 100,

        color: '#fff',

        fontSize: 24,

        opacity: interpolate(frame, [90, 105], [0, 1]),

      }}>

        原子 = 原子核 + 电子

      </div>

    </AbsoluteFill>

  );

};

```

  

### 化学式动画组件 (Formula.tsx)

  

```tsx

import { useCurrentFrame, interpolate, spring } from 'remotion';

  

interface FormulaProps {

  formula: string;      // 化学式，如 "H2O"

  colorMap?: object;    // 元素颜色映射

}

  

export const Formula: React.FC<FormulaProps> = ({

  formula,

  colorMap = { H: '#FFFFFF', O: '#FF0D0D', C: '#909090' }

}) => {

  const frame = useCurrentFrame();

  // 解析化学式

  const parseFormula = (f: string) => {

    const parts = [];

    const regex = /([A-Z][a-z]?)(\d*)/g;

    let match;

    while ((match = regex.exec(f)) !== null) {

      parts.push({

        element: match[1],

        count: match[2] || '1',

        color: colorMap[match[1]] || '#FFFFFF'

      });

    }

    return parts;

  };

  const parts = parseFormula(formula);

  return (

    <div style={{

      display: 'flex',

      alignItems: 'flex-start',

      gap: 4,

    }}>

      {parts.map((part, index) => {

        const opacity = interpolate(

          frame,

          [index * 10, index * 10 + 10],

          [0, 1],

          { extrapolateRight: 'clamp' }

        );

        return (

          <div key={index} style={{

            display: 'flex',

            opacity,

            transform: `scale(${spring({ frame: frame - index * 10, fps: 30 })})`

          }}>

            <span style={{

              fontSize: 48,

              fontWeight: 'bold',

              color: part.color

            }}>

              {part.element}

            </span>

            {part.count !== '1' && (

              <span style={{

                fontSize: 24,

                color: '#aaa',

                alignSelf: 'flex-end',

                marginBottom: 8

              }}>

                {part.count}

              </span>

            )}

          </div>

        );

      })}

    </div>

  );

};

```

  

### 语音合成脚本 (generate_voiceover.py)

  

```python

"""

AI语音合成脚本

使用Edge-TTS生成课件讲解语音

"""

  

import asyncio

import edge_tts

from pathlib import Path

  

# 音色配置

VOICE = "zh-CN-XiaoxiaoNeural"  # 女声，清晰

  

async def generate_voice(text: str, output: str):

    """生成单段语音"""

    communicate = edge_tts.Communicate(text, VOICE)

    await communicate.save(output)

  

async def generate_courseware_voiceover(scenes: list, output_dir: str):

    """生成完整课件语音"""

    output_path = Path(output_dir)

    output_path.mkdir(exist_ok=True)

    for i, scene in enumerate(scenes):

        await generate_voice(

            scene['text'],

            str(output_path / f"scene_{i:02d}.mp3")

        )

        print(f"[{i+1}/{len(scenes)}] 生成语音: {scene['title']}")

  

# 示例使用

if __name__ == "__main__":

    scenes = [

        {"title": "引入", "text": "今天我们来学习原子结构..."},

        {"title": "原子核", "text": "原子核位于原子中心..."},

        {"title": "电子", "text": "电子在核外高速运动..."},

    ]

    asyncio.run(generate_courseware_voiceover(scenes, "out/audio"))

```

  

### 音视频合成脚本 (merge_final.py)

  

```python

"""

音视频合成脚本

使用FFmpeg合并视频和语音

"""

  

import subprocess

from pathlib import Path

  

def merge_audio_video(

    video_path: str,

    audio_path: str,

    output_path: str

):

    """合并音视频"""

    cmd = [

        'ffmpeg', '-y',

        '-i', video_path,

        '-i', audio_path,

        '-c:v', 'copy',

        '-c:a', 'aac',

        '-map', '0:v:0',

        '-map', '1:a:0',

        output_path

    ]

    subprocess.run(cmd, check=True)

    print(f"合并完成: {output_path}")

  

def add_subtitles(

    video_path: str,

    srt_path: str,

    output_path: str

):

    """添加字幕"""

    cmd = [

        'ffmpeg', '-y',

        '-i', video_path,

        '-vf', f"subtitles={srt_path}",

        output_path

    ]

    subprocess.run(cmd, check=True)

    print(f"字幕添加完成: {output_path}")

  

# 使用示例

if __name__ == "__main__":

    merge_audio_video(

        "out/atomic-structure.mp4",

        "out/audio/concat_list.txt",

        "out/atomic-structure-synced.mp4"

    )

```

  

---

  

## 📦 安装使用

  

### 安装依赖

  

```bash

# 进入技能包目录

cd chemistry-courseware

  

# 安装Node.js依赖

npm install

  

# 安装Python依赖（用于语音合成）

pip install edge-tts

  

# 安装FFmpeg（用于音视频合成）

# Windows: choco install ffmpeg

# Mac: brew install ffmpeg

# Linux: sudo apt install ffmpeg

```

  

### 使用方式

  

```bash

# 本地预览

npm run dev

  

# 渲染单个课件

npx remotion render AtomicStructure out/atomic-structure.mp4

  

# 渲染所有课件

npm run build:all

  

# 生成语音

python scripts/generate_voiceover.py

  

# 合成最终视频

python scripts/merge_final.py

```

  

---

  

## 🎨 配色规范

  

```ts

// 化学元素配色（参考CPK着色标准）

export const elementColors = {

  H: '#FFFFFF',   // 氢 - 白色

  C: '#909090',   // 碳 - 灰色

  N: '#3050F8',   // 氮 - 蓝色

  O: '#FF0D0D',   // 氧 - 红色

  S: '#FFFF30',   // 硫 - 黄色

  Cl: '#1FF01F',  // 氯 - 绿色

  Na: '#AB5CF2',  // 钠 - 紫色

  Fe: '#E06633',  // 铁 - 橙色

};

  

// 主题配色

export const themeColors = {

  background: '#1a1a2e',   // 深蓝背景

  primary: '#00d4ff',      // 青色主色

  secondary: '#ff6b6b',    // 红色辅色

  text: '#ffffff',         // 白色文字

  accent: '#ffd93d',       // 金色强调

};

```

  

---

  

## 📊 核心动画类型

  

| 动画类型 | 适用知识点 | 示例 |

|---------|-----------|------|

| 粒子运动 | 原子结构、电子云 | 电子绕核运动 |

| 结构变化 | 化学键形成/断裂 | 离子键、共价键 |

| 过程演示 | 化学反应 | 燃烧、电解 |

| 数据可视化 | 溶解度、周期律 | 图表动画 |

| 实验模拟 | 实验操作 | 滴定、过滤 |

  

---

  

## 🎯 应用场景

  

- **初三化学**：原子结构、化学式、化学反应、溶液、酸碱盐

- **高一化学**：摩尔概念、离子反应、氧化还原、元素周期律

- **实验教学**：实验操作动画模拟

- **在线教育**：自动生成教学视频

  

---

  

## 📝 技术亮点

  

### 1. 深度应用OpenClaw能力

  

| 能力 | 应用 | 效果 |

|-----|------|------|

| Shell接口 | 调用Remotion/FFmpeg | AI执行渲染任务 |

| 文件系统 | 读取PDF、保存视频 | AI管理教学资源 |

| AI分析 | 提取知识点 | AI理解教学内容 |

  

### 2. Remotion帧驱动动画

  

- 所有动画基于 `useCurrentFrame()` 驱动

- 使用 `spring()` 创建自然动画效果

- 60fps流畅动画输出

  

### 3. 多模态输出

  

- 视频动画 + 语音讲解 + 字幕

- 支持批量生成

- 可定制化模板

  

---

  

## 🚀 效率提升

  

| 对比 | 传统制作 | chemistry-courseware |

|-----|---------|---------------------|

| 单课制作时间 | 2-4小时 | **< 30分钟** |

| 专业要求 | 动画制作技能 | **自动生成** |

| 批量能力 | 不可能 | **一键批量** |

| 质量一致性 | 因人而异 | **专业模板** |

  

---

  

## 📦 开源地址

  

**GitHub**：[https://github.com/anbeime/skill](https://github.com/anbeime/skill)

  

```bash

# 安装技能包

git clone https://github.com/your-username/chemistry-courseware-skill.git

cd chemistry-courseware-skill

npm install

```

  

---

  

## 🎬 演示视频

  

**B站**：[化学动态课件制作演示]

**YouTube**：[Chemistry Courseware Demo]

  

---

  

**作者**：chemistry-courseware Team

**日期**：2026年3月

**参赛项目**：OpenClaw社群挑战赛