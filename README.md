# FinanceDoc AI｜财务文档智能分析与风险审阅系统

FinanceDoc AI 是一个基于 Streamlit 的财务文档分析 demo，用于展示“财务文档上传、文本和表格解析、关键指标提取、规则化风险识别、问答辅助、分析底稿导出”的完整工作流。

第一版采用 demo mode，不依赖本地 Ollama，也不强制调用付费 LLM API，因此可以部署到 Streamlit Community Cloud。后续可以在同一接口层接入 OpenAI 或 DeepSeek API，升级为 RAG 或 Multi-Agent 财务分析系统。

## 业务场景

- 年报、审计报告、招股书、尽调材料的快速初筛
- 财务分析岗、审计岗、商业分析岗面试作品展示
- 将财务数据录入、风险审阅、分析底稿生成流程产品化
- 在 LLM API 接入前，用规则和文本检索保证可解释性

## 核心功能

- 上传并解析 PDF、Excel、CSV 文件
- 使用 PyPDF2 提取 PDF 文本
- 使用 pandas 和 openpyxl 读取表格数据
- 自动识别收入、成本、利润、现金流、资产负债等关键字段
- 生成财务摘要和趋势图表
- 基于规则识别收入下降、利润承压、现金流质量、负债率、费用率、审计意见、关联交易等风险
- 使用文本检索模拟 Q&A Assistant
- 生成面试或投研可用的 Analyst Brief
- 支持导出 Markdown 分析底稿、风险清单 CSV、解析表格 CSV

## 技术栈

- Python
- Streamlit
- Pandas
- Plotly
- PyPDF2
- openpyxl
- python-dotenv

## 项目架构

```text
financedoc-ai
├── streamlit_app.py
├── requirements.txt
├── README.md
├── .gitignore
└── sample_data
    └── sample_financials.csv
```

## 本地运行

```bash
python -m pip install -r requirements.txt
python -m streamlit run streamlit_app.py
```

打开浏览器访问：

```text
http://localhost:8501
```

如果没有上传文件，系统会自动使用 `sample_data/sample_financials.csv` 展示 demo。

## 页面说明

- Home：项目定位、使用场景、技术栈
- Upload & Parse：上传 PDF、Excel 或 CSV，预览解析文本和表格
- Financial Summary：生成财务指标摘要和 Plotly 图表
- Risk Review：展示规则化风险识别结果和审阅建议
- Q&A Assistant：基于文本检索和财务规则模拟问答
- Analyst Brief：生成结构化分析稿
- Export：下载分析结果

## 未来升级方向

- 接入 OpenAI / DeepSeek API
- 增加 RAG 年报问答能力
- 增加多文件横向对比分析
- 增加 Multi-Agent 财务分析层：
  - Accounting Agent
  - Risk Review Agent
  - Strategy Analyst Agent
  - Report Writer Agent
- 导出 Word 或 PDF 审计底稿
- 与个人作品集网站互相跳转
