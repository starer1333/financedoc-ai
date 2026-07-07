# FinanceDoc AI｜财务文档智能分析与风险审阅系统

FinanceDoc AI 是一个基于 Streamlit 的财务文档分析系统，用于展示“财务文档上传、文本和表格解析、关键指标提取、RAG 问答、多 Agent 风险审阅、分析底稿导出”的完整工作流。

系统默认支持 demo mode，不依赖本地 Ollama，也不强制调用付费 LLM API，因此可以部署到 Streamlit Community Cloud。配置 API key 后，可切换到 OpenAI 或 DeepSeek 进行真实 LLM 问答和 Multi-Agent 分析。

## 在线网站部署

这个项目的目标是部署成一个所有人都能访问的网页应用，而不是只在本地电脑运行。

推荐部署平台：Streamlit Community Cloud

部署后会得到一个公网链接，形式类似：

```text
https://your-app-name.streamlit.app
```

部署设置：

```text
Repository: starer1333/financedoc-ai
Branch: main
Main file path: streamlit_app.py
```

部署步骤：

1. 打开 Streamlit Community Cloud：https://share.streamlit.io
2. 使用 GitHub 账号登录
3. 点击 New app 或 Create app
4. 选择仓库 `starer1333/financedoc-ai`
5. Branch 选择 `main`
6. Main file path 填 `streamlit_app.py`
7. 点击 Deploy

部署完成后，把生成的 `.streamlit.app` 链接放到 GitHub 仓库简介、README 顶部和个人网站项目卡片里。

> `http://localhost:8501` 只代表本地开发地址，只有在你自己的电脑运行 Streamlit 时才能打开。它不是公网网站链接，其他人无法通过这个地址访问你的项目。

## 业务场景

- 年报、审计报告、招股书、尽调材料的快速初筛
- 财务分析岗、审计岗、商业分析岗面试作品展示
- 将财务数据录入、风险审阅、分析底稿生成流程产品化
- 用规则、RAG 检索和可选 LLM API 结合，提升分析可解释性

## 核心功能

- 上传并解析 PDF、Excel、CSV 文件
- 使用 PyPDF2 提取 PDF 文本
- 使用 pandas 和 openpyxl 读取表格数据
- 自动识别收入、成本、利润、现金流、资产负债等关键字段
- 生成财务摘要和趋势图表
- 基于规则识别收入下降、利润承压、现金流质量、负债率、费用率、审计意见、关联交易等风险
- 支持 RAG Search，返回问答引用的证据片段
- Q&A Assistant 支持 Demo Mode、OpenAI 和 DeepSeek
- Multi-Agent Review 包括 Accounting Agent、Risk Review Agent、Strategy Analyst Agent、Report Writer Agent
- 支持多文件上传和横向解析
- 生成面试或投研可用的 Analyst Brief
- 支持导出 Markdown、CSV、Word 审计底稿和 PDF 审计底稿

## 技术栈

- Python
- Streamlit
- Pandas
- Plotly
- PyPDF2
- openpyxl
- python-dotenv
- python-docx
- ReportLab

## 项目架构

```text
financedoc-ai
├── .streamlit
│   └── config.toml
├── streamlit_app.py
├── requirements.txt
├── README.md
├── .gitignore
└── sample_data
    └── sample_financials.csv
```

## 本地开发运行

本地运行只是给开发者调试用，不是给别人访问的网站链接。

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
- Q&A Assistant：基于 RAG 检索、财务规则和可选 LLM API 问答
- RAG Search：查看系统检索到的文本和表格证据
- Multi-Agent Review：用多个分析角色生成审阅意见
- Analyst Brief：生成结构化分析稿
- Export：下载 Markdown、CSV、Word 和 PDF 结果

## 可选 LLM 配置

如果不配置 API key，系统会自动使用 Demo Mode，本地和 Streamlit Cloud 都能正常运行。

OpenAI：

```text
OPENAI_API_KEY=your_openai_key
OPENAI_MODEL=gpt-4o-mini
OPENAI_BASE_URL=https://api.openai.com/v1/chat/completions
```

DeepSeek：

```text
DEEPSEEK_API_KEY=your_deepseek_key
DEEPSEEK_MODEL=deepseek-chat
DEEPSEEK_BASE_URL=https://api.deepseek.com/chat/completions
```

在 Streamlit Community Cloud 中，可把这些变量配置到 App Secrets。

## 已实现升级

- OpenAI / DeepSeek API 可选接入
- RAG 文档检索问答
- 多文件上传和对比解析
- Multi-Agent 财务分析层
- Word / PDF 审计底稿导出

## 后续可继续扩展

- 更细粒度的年报章节切分
- OCR 扫描件识别
- 与个人作品集网站互相跳转
- 行业 benchmark 数据接入
