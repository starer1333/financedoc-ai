# FinanceDoc AI｜财务文档智能分析与风险审阅系统

FinanceDoc AI 是一个基于 Streamlit 的公开网页项目，用于展示“财务文档上传、文本和表格解析、关键指标提取、RAG 问答、多 Agent 风险审阅、分析底稿导出”的完整工作流。

系统接入 DeepSeek API，不依赖本地 Ollama，因此可以部署到 Streamlit Community Cloud。DeepSeek 密钥只存放在 Streamlit Secrets 中，不会公开到 GitHub 或网页前台。

## 在线访问

公开网站：

```text
https://financedoc-ai.streamlit.app/
```

页面采用一页式下滑体验。打开网站后，不需要逐个点击页面菜单，直接向下滚动即可依次看到：

```text
项目概览 → 数据输入 → 财务摘要 → 风险审阅 → RAG 问答 → Multi-Agent 分析 → 底稿导出
```

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
- 提供 5 套内置财务样例：制造业、SaaS、零售连锁、地产服务、拟 IPO
- 使用 PyPDF2 提取 PDF 文本
- 使用 pandas 和 openpyxl 读取表格数据
- 自动识别收入、成本、利润、现金流、资产负债等关键字段
- 生成财务摘要和趋势图表
- 基于规则识别收入下降、利润承压、现金流质量、负债率、费用率、审计意见、关联交易等风险
- 支持 RAG Search，返回问答引用的证据片段
- Q&A Assistant 使用 DeepSeek API + RAG 检索生成回答
- Multi-Agent Review 包括 Accounting Agent、Risk Review Agent、Strategy Analyst Agent、Report Writer Agent
- 支持多文件上传和横向解析
- 生成面试或投研可用的 Analyst Brief
- 支持导出 Markdown、CSV、Word 审计底稿和 PDF 审计底稿

## 内置样例数据

```text
sample_data/sample_financials.csv              制造业｜利润修复与回款压力
sample_data/sample_saas_financials.csv         SaaS｜高增长与亏损收窄
sample_data/sample_retail_financials.csv       零售连锁｜库存周转与费用压力
sample_data/sample_real_estate_services.csv    地产服务｜高负债与偿债压力
sample_data/sample_ipo_financials.csv          拟 IPO｜收入增长与关联交易审阅
```

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
    └── sample_saas_financials.csv
    └── sample_retail_financials.csv
    └── sample_real_estate_services.csv
    └── sample_ipo_financials.csv
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

- 项目概览：说明产品定位和 DeepSeek + RAG 工作流
- 数据输入：上传 PDF、Excel、CSV，或切换内置样例数据
- 财务摘要：生成关键指标和 Plotly 趋势图
- 风险审阅：展示规则化风险识别结果和审阅建议
- RAG 问答：基于文本检索、财务规则和 DeepSeek API 回答问题
- Multi-Agent 分析：用多个分析角色生成审阅意见
- 底稿导出：下载 Markdown、CSV、Word 和 PDF 结果

## DeepSeek API 配置

正式展示使用 Streamlit Cloud 的 App Secrets：

```text
Streamlit Cloud → App → Settings → Secrets
```

仓库里提供了 `.streamlit/secrets.toml.example` 作为模板。真实的 `.streamlit/secrets.toml` 已被 `.gitignore` 排除，不会提交到 GitHub。

DeepSeek：

```text
DEEPSEEK=your_deepseek_key
DEEPSEEK_MODEL=deepseek-v4-flash
DEEPSEEK_BASE_URL=https://api.deepseek.com/chat/completions
```

也可以使用：

```text
DEEPSEEK_API_KEY=your_deepseek_key
```

在 Streamlit Community Cloud 中，可把这些变量配置到 App Secrets。

Streamlit Secrets 示例：

```toml
DEEPSEEK = "your_deepseek_key"
DEEPSEEK_MODEL = "deepseek-v4-flash"
DEEPSEEK_BASE_URL = "https://api.deepseek.com/chat/completions"
```

## DeepSeek 接入验证文件

仓库提供了专门用于验证 API 是否真实接入的测试文件：

```text
test_documents/deepseek_api_probe_memo.pdf
test_documents/deepseek_api_probe_financials.csv
test_documents/deepseek_api_probe_instructions.md
```

把 PDF 和 CSV 同时上传到网页后，在 RAG 问答区提问：

```text
请根据我上传的测试文档，完成 DeepSeek API 接入验证。请输出验证暗号、最主要的三个财务风险，并判断这是现金流质量问题还是收入规模问题。
```

如果 DeepSeek 正常接入，回答应能识别暗号 `DS-PROBE-7429`，并说明主要问题是现金流质量、回款压力和存货周转，而不是单纯收入规模下降。

## 已实现升级

- DeepSeek API 接入
- RAG 文档检索问答
- 多文件上传和对比解析
- 多行业样例数据切换
- 一页式下滑网页体验
- Multi-Agent 财务分析层
- Word / PDF 审计底稿导出

## 后续可继续扩展

- 更细粒度的年报章节切分
- OCR 扫描件识别
- 与个人作品集网站互相跳转
- 行业 benchmark 数据接入
