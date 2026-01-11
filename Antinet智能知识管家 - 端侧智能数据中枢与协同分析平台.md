 📊 项目真实定位确认

  项目全称: Antinet智能知识管家 - 端侧智能数据中枢与协同分析平台

  赛道: AIPC赛道-通用赛
  团队: TOPGO

  ---
  🎯 核心定位与创新点

  产品定位

  部署于骁龙AIPC的端侧智能数据工作站，将数据分析和知识管理深度融合：

  数据分析层 ────┐
                 ├──> NPU加速推理 ──> 四色卡片沉淀 ──> 本地知识库
  知识管理层 ────┘

  核心创新点

  1. 端侧AI驱动的数据分析
  - 自然语言驱动的数据查询（"上个月销售额趋势是什么？"）
  - 自动数据分析与可视化
  - NPU加速轻量化模型（Qwen2-1.5B/7B）

  2. 四色卡片方法论沉淀分析结果
  - 🔵 蓝色卡片(事实): 数据分析的客观结果和指标
  - 🟢 绿色卡片(解释): 数据背后的原因分析和关联
  - 🟡 黄色卡片(风险): 潜在问题和风险预警
  - 🔴 红色卡片(行动): 基于分析的行动建议

  3. 数据安全与本地化
  - 连接飞书、钉钉等云端数据源
  - 所有原始数据处理在本地完成
  - 数据不出域，保障企业核心数据资产

  ---
  🏗️ 技术架构

  ┌─────────────────────────────────────────────────────┐
  │              前端展示层 (React + Vite)               │
  │  数据看板 | 四色卡片管理 | 自然语言查询界面         │
  └────────────────────┬────────────────────────────────┘
                       │
  ┌────────────────────┴────────────────────────────────┐
  │         端侧AI推理层 (骁龙NPU加速)                   │
  │  • Qwen2-1.5B/7B (NLU + 数据分析)                   │
  │  • LSTM/Transformer (时序预测)                       │
  │  • QNN SDK 执行提供程序                              │
  └────────────────────┬────────────────────────────────┘
                       │
  ┌────────────────────┴────────────────────────────────┐
  │            数据处理层 (本地化)                       │
  │  • 本地数据库 (SQLite/DuckDB)                       │
  │  • 数据清洗与ETL                                     │
  │  • 连接器 (飞书/钉钉API - 仅获取不存储)             │
  └─────────────────────────────────────────────────────┘

  ---
  🚀 远程AIPC开发测试完整方案

  阶段1: 基础环境搭建 (今天完成)

  步骤1: 远程桌面连接
  Win + R → mstsc.exe
  配置磁盘重定向 (勾选C盘)
  连接: ai-pc.cvmart.net:1007
  账号: AI-PC-19
  密码: M)7dCjOe06Twi[xFnumMkfYMq

  步骤2: 复制项目到远程AIPC
  # 在远程AIPC的PowerShell中执行
  xcopy "\\tsclient\C\D\compet\xiaolong" "C:\workspace\antinet" /E /I /Y
  cd C:\workspace\antinet

  步骤3: 验证开发环境
  # 检查Node.js (前端)
  node --version  # 需要 v18+

  # 检查Python (AI模型)
  python --version  # 需要 3.10+

  # 检查pnpm
  pnpm --version

  # 如果缺少，安装它们
  npm install -g pnpm

  步骤4: 启动Web前端
  pnpm install
  pnpm run dev

  # 访问: http://localhost:3000

  ---
  阶段2: 集成骁龙NPU加速 (核心工作)

  2.1 部署Qwen2轻量化模型

  方案A: 使用QNN SDK (推荐)

  参考 资料参考/command.txt 中的环境:
  # 已有的AI引擎环境
  cd %USERPROFILE%\Desktop\ai-engine-direct-helper\samples

  # 安装QAI AppBuilder
  pip install qai_appbuilder-2.31.0-cp312-cp312-win_amd64.whl

  # 部署Qwen2-1.5B模型
  python deploy_qwen2.py --model qwen2-1.5b --backend QNN --device NPU

  创建 deploy_qwen2.py:
  # deploy_qwen2.py - 部署Qwen2到骁龙NPU
  import qai_appbuilder as qai
  from pathlib import Path

  def deploy_qwen2_npu():
      """部署Qwen2-1.5B到骁龙NPU"""

      print("=" * 50)
      print("Antinet - 部署Qwen2到骁龙NPU")
      print("=" * 50)

      # 配置
      config = {
          "model_name": "qwen2-1.5b",
          "backend": "QNN",
          "device": "NPU",
          "precision": "INT8",  # 量化以提升性能
          "cache_dir": "./models"
      }

      print(f"\n[1/4] 下载Qwen2-1.5B模型...")
      # 从Hugging Face或本地路径加载
      model_path = qai.hub.download_model(config["model_name"])

      print(f"\n[2/4] 转换模型为QNN格式...")
      # 转换为ONNX再转QNN
      onnx_model = qai.convert_to_onnx(model_path)
      qnn_model = qai.convert_to_qnn(onnx_model,
                                       device="NPU",
                                       precision="INT8")

      print(f"\n[3/4] 编译模型到NPU...")
      compiled_model = qai.compile_for_npu(qnn_model)

      print(f"\n[4/4] 保存编译后的模型...")
      output_path = Path("./models/qwen2-1.5b-npu.bin")
      qai.save_model(compiled_model, output_path)

      print(f"\n✓ 模型部署完成!")
      print(f"  路径: {output_path}")
      print(f"  后端: {config['backend']}")
      print(f"  设备: {config['device']}")

      # 性能测试
      print(f"\n[性能测试] 测试NPU推理延迟...")
      test_input = "分析上个月的销售数据"
      latency = qai.benchmark_inference(compiled_model, test_input)
      print(f"  平均延迟: {latency:.2f}ms")

      return compiled_model

  if __name__ == "__main__":
      deploy_qwen2_npu()

  2.2 集成到前端应用

  创建后端API服务 (backend/server.py):
  # backend/server.py - 数据分析后端服务
  from fastapi import FastAPI, HTTPException
  from pydantic import BaseSettings, BaseModel
  import qai_appbuilder as qai
  import json

  app = FastAPI(title="Antinet数据分析API")

  # 加载NPU模型
  print("加载Qwen2-NPU模型...")
  model = qai.load_model("./models/qwen2-1.5b-npu.bin", device="NPU")
  print("✓ 模型加载完成")

  class QueryRequest(BaseModel):
      query: str  # 自然语言查询
      data_source: str  # 数据源 (local/feishu/dingtalk)
      context: dict = {}  # 额外上下文

  class AnalysisResult(BaseModel):
      facts: list[str]  # 事实卡片
      explanations: list[str]  # 解释卡片
      risks: list[str]  # 风险卡片
      actions: list[str]  # 行动卡片
      visualizations: list[dict]  # 可视化配置

  @app.post("/api/analyze", response_model=AnalysisResult)
  async def analyze_data(request: QueryRequest):
      """自然语言驱动的数据分析"""

      try:
          # 1. 使用NPU模型理解查询意图
          print(f"[NPU推理] 分析查询: {request.query}")
          intent = model.infer(
              prompt=f"分析以下数据查询请求，提取关键信息：{request.query}",
              max_tokens=512
          )

          # 2. 执行数据查询 (本地处理)
          # 这里应该连接本地数据库或通过API获取数据
          data = fetch_data_locally(request.data_source, intent)

          # 3. 使用NPU模型生成四色卡片分析
          analysis_prompt = f"""
          基于以下数据，生成四色卡片分析：
          数据: {json.dumps(data)}
          查询: {request.query}

          请分别生成：
          1. 事实(Facts): 客观数据结果
          2. 解释(Explanations): 数据背后的原因
          3. 风险(Risks): 潜在问题和风险点
          4. 行动(Actions): 具体行动建议

          以JSON格式返回。
          """

          analysis = model.infer(prompt=analysis_prompt, max_tokens=1024)
          result = json.loads(analysis)

          # 4. 生成可视化配置
          visualizations = generate_visualizations(data, intent)

          return AnalysisResult(
              facts=result.get("facts", []),
              explanations=result.get("explanations", []),
              risks=result.get("risks", []),
              actions=result.get("actions", []),
              visualizations=visualizations
          )

      except Exception as e:
          raise HTTPException(status_code=500, detail=str(e))

  def fetch_data_locally(source: str, intent: dict) -> dict:
      """本地化数据获取 - 数据不出域"""
      # 实现本地数据库查询或API调用
      # 关键: 原始数据不发送到云端
      return {"mock": "data"}

  def generate_visualizations(data: dict, intent: dict) -> list[dict]:
      """生成可视化配置"""
      return [
          {"type": "line", "data": data, "config": {}}
      ]

  @app.get("/api/health")
  async def health_check():
      """健康检查"""
      return {
          "status": "healthy",
          "model": "qwen2-1.5b",
          "device": "NPU",
          "service": "Antinet数据分析API"
      }

  if __name__ == "__main__":
      import uvicorn
      uvicorn.run(app, host="0.0.0.0", port=8000)

  启动后端服务:
  cd C:\workspace\antinet\backend
  pip install fastapi uvicorn qai_appbuilder
  python server.py

  # 输出:
  # 加载Qwen2-NPU模型...
  # ✓ 模型加载完成
  # INFO: Uvicorn running on http://0.0.0.0:8000

  2.3 前端集成自然语言查询

  修改前端代码 (src/components/DataAnalysisPanel.tsx):
  // src/components/DataAnalysisPanel.tsx
  import React, { useState } from 'react';
  import { Search, Loader, TrendingUp } from 'lucide-react';
  import { toast } from 'sonner';

  interface AnalysisResult {
    facts: string[];
    explanations: string[];
    risks: string[];
    actions: string[];
    visualizations: any[];
  }

  export const DataAnalysisPanel: React.FC = () => {
    const [query, setQuery] = useState('');
    const [loading, setLoading] = useState(false);
    const [result, setResult] = useState<AnalysisResult | null>(null);

    const handleAnalyze = async () => {
      if (!query.trim()) return;

      setLoading(true);
      try {
        const response = await fetch('http://localhost:8000/api/analyze', {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify({
            query: query,
            data_source: 'local',
            context: {}
          })
        });

        if (!response.ok) throw new Error('分析失败');

        const data = await response.json();
        setResult(data);

        // 自动创建四色卡片
        createFourColorCards(data);

        toast('分析完成！四色卡片已自动生成', {
          className: 'bg-green-50 text-green-800'
        });

      } catch (error) {
        toast('分析失败，请检查后端服务', {
          className: 'bg-red-50 text-red-800'
        });
      } finally {
        setLoading(false);
      }
    };

    const createFourColorCards = (analysis: AnalysisResult) => {
      // 创建蓝色卡片(事实)
      analysis.facts.forEach(fact => {
        createCard({ title: '数据事实', content: fact, color: 'blue' });
      });

      // 创建绿色卡片(解释)
      analysis.explanations.forEach(exp => {
        createCard({ title: '原因解释', content: exp, color: 'green' });
      });

      // 创建黄色卡片(风险)
      analysis.risks.forEach(risk => {
        createCard({ title: '风险预警', content: risk, color: 'yellow' });
      });

      // 创建红色卡片(行动)
      analysis.actions.forEach(action => {
        createCard({ title: '行动建议', content: action, color: 'red' });
      });
    };

    return (
      <div className="bg-white dark:bg-gray-800 rounded-xl p-6">
        <h2 className="text-xl font-bold mb-4 flex items-center">
          <TrendingUp className="mr-2" size={20} />
          智能数据分析
        </h2>

        <div className="flex gap-3 mb-6">
          <div className="relative flex-1">
            <Search className="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400" size={18} />
            <input
              type="text"
              placeholder="例如: 上个月销售额趋势是什么？"
              value={query}
              onChange={(e) => setQuery(e.target.value)}
              onKeyPress={(e) => e.key === 'Enter' && handleAnalyze()}
              className="w-full pl-10 pr-4 py-3 border rounded-lg focus:ring-2 focus:ring-blue-500"
            />
          </div>
          <button
            onClick={handleAnalyze}
            disabled={loading}
            className="px-6 py-3 bg-blue-600 hover:bg-blue-700 text-white rounded-lg flex items-center gap-2 disabled:opacity-50"
          >
            {loading ? <Loader className="animate-spin" size={16} /> : <Search size={16} />}
            分析
          </button>
        </div>

        {result && (
          <div className="grid grid-cols-2 gap-4">
            {/* 四色卡片展示 */}
            <CardPreview title="事实" items={result.facts} color="blue" />
            <CardPreview title="解释" items={result.explanations} color="green" />
            <CardPreview title="风险" items={result.risks} color="yellow" />
            <CardPreview title="行动" items={result.actions} color="red" />
          </div>
        )}
      </div>
    );
  };

  ---
  📈 核心价值指标验证

  需要在AIPC上测试并记录的数据:

  1. 效率提升指标
  传统方式: 数据分析 + 报告撰写 = 数小时
  Antinet方式: 自然语言查询 → NPU分析 → 自动生成四色卡片 = 分钟级

  目标: 提升效率 70%+

  2. NPU加速效果
  # 性能对比测试脚本
  def benchmark_npu_acceleration():
      test_query = "分析上个月销售趋势"

      # CPU推理
      cpu_time = run_inference(device="CPU", query=test_query)

      # NPU推理
      npu_time = run_inference(device="NPU", query=test_query)

      speedup = cpu_time / npu_time
      print(f"NPU加速比: {speedup:.2f}x")
      print(f"CPU延迟: {cpu_time:.2f}ms")
      print(f"NPU延迟: {npu_time:.2f}ms")

  目标指标:
  - NPU推理延迟 < 500ms
  - 相比CPU加速 3-5倍
  - 端到端分析时间 < 5分钟

  3. 数据安全验证
  - ✅ 所有敏感数据仅在本地处理
  - ✅ 云端API仅用于非敏感元数据
  - ✅ 模型推理完全在端侧NPU执行