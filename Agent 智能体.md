# Agent 智能体

[](https://github.com/xlang-ai/OSWorld/blob/main/mm_agents/README.md#agent)

## Prompt-based Agents 基于提示词的智能体

[](https://github.com/xlang-ai/OSWorld/blob/main/mm_agents/README.md#prompt-based-agents)

### Supported Models 支持的模型

[](https://github.com/xlang-ai/OSWorld/blob/main/mm_agents/README.md#supported-models)
[[高德智能体（Agent）的提示词模板]]
We currently support the following models as the foundational models for the agents:我们目前支持以下模型作为智能体的基础模型：

- `GPT-3.5` (gpt-3.5-turbo-16k, ...) `GPT-3.5`（gpt-3.5-turbo-16k，……）
- `GPT-4` (gpt-4-0125-preview, gpt-4-1106-preview, ...)`GPT-4`（gpt-4-0125-preview、gpt-4-1106-preview……）
- `GPT-4V` (gpt-4-vision-preview, ...) `GPT-4V`（gpt-4-vision-preview，……）
- `Gemini-Pro`
- `Gemini-Pro-Vision`
- `Claude-3, 2` (claude-3-haiku-2024030, claude-3-sonnet-2024022, ...)`Claude-3, 2`（claude-3-haiku-2024030、claude-3-sonnet-2024022……）
- ...

And those from the open-source community:以及来自开源社区的那些：

- `Mixtral 8x7B`
- `QWEN`, `QWEN-VL` `QWEN`，`QWEN-VL`
- `CogAgent`
- `Llama3`
- ...

In the future, we will integrate and support more foundational models to enhance digital agents, so stay tuned.未来，我们将整合并支持更多基础模型，以增强数字智能体，敬请期待。

### How to use 使用方法

[](https://github.com/xlang-ai/OSWorld/blob/main/mm_agents/README.md#how-to-use)

```python
from mm_agents.agent import PromptAgent

agent = PromptAgent(
    model="gpt-4-vision-preview",
    observation_type="screenshot",
)
agent.reset()
# say we have an instruction and observation
instruction = "Please help me to find the nearest restaurant."
obs = {"screenshot": open("path/to/observation.jpg", 'rb').read()}
response, actions = agent.predict(
    instruction,
    obs
)
```

### Observation Space and Action Space 观测空间与动作空间

[](https://github.com/xlang-ai/OSWorld/blob/main/mm_agents/README.md#observation-space-and-action-space)

We currently support the following observation spaces:我们目前支持以下观测空间：

- `a11y_tree`: the accessibility tree of the current screen`a11y_tree`：当前屏幕的无障碍树
- `screenshot`: a screenshot of the current screen`screenshot`：当前屏幕的屏幕截图
- `screenshot_a11y_tree`: a screenshot of the current screen with the accessibility tree overlay`screenshot_a11y_tree`：带有辅助功能树覆盖层的当前屏幕截图
- `som`: the set-of-mark trick on the current screen, with table metadata included.`som`：当前屏幕上的标记集技巧，包含表格元数据。

And the following action spaces: 以及以下动作空间：

- `pyautogui`: valid Python code with `pyautogui` code valid`pyautogui`：包含有效的`pyautogui`代码的合法Python代码
- `computer_13`: a set of enumerated actions designed by us`computer_13`：我们设计的一组枚举动作

To feed an observation into the agent, you have to maintain the `obs` variable as a dict with the corresponding information:要将观测值输入智能体，你必须将`obs`变量维护为一个包含相应信息的字典：

```python
# continue from the previous code snippet
obs = {
    "screenshot": open("path/to/observation.jpg", 'rb').read(),
    "a11y_tree": ""  # [a11y_tree data]
}
response, actions = agent.predict(
    instruction,
    obs
)
```

## Efficient Agents, Q* Agents, and more高效智能体、Q*智能体及更多

[](https://github.com/xlang-ai/OSWorld/blob/main/mm_agents/README.md#efficient-agents-q-agents-and-more)

Stay tuned for more updates. 敬请期待更多更新。