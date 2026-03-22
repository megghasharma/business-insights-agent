# 🤖 Business Insights Agent

> An AI-powered data analysis agent that answers natural-language business questions using Claude's tool-use capabilities.

![Python](https://img.shields.io/badge/Python-3.10+-blue)
![Claude AI](https://img.shields.io/badge/Claude_AI-Tool_Use-blueviolet)
![MCP](https://img.shields.io/badge/MCP-Inspired-purple)

## 📌 Overview

Drop in any CSV file, ask a business question in plain English, and the agent autonomously inspects the data, runs the right analyses, detects anomalies, and delivers an executive summary — all powered by Claude's tool-use (function calling) capabilities.

This project demonstrates practical AI agent development inspired by the **Model Context Protocol (MCP)** architecture, where the LLM orchestrates tools to complete complex analytical tasks.

## 💡 What It Does

```bash
python src/agent.py data/sales_data.csv "Which region has the highest profit margin and why?"
```

The agent will:
1. **Inspect** the dataset structure and statistics
2. **Query** the data with auto-generated Pandas code
3. **Calculate** relevant metrics (margins, growth rates, correlations)
4. **Detect** anomalies in key columns
5. **Summarise** findings in an executive report

All tool calls are decided and orchestrated by Claude — the agent loop runs until the question is fully answered.

## 🏗️ Architecture

```
┌─────────────┐     ┌──────────────┐     ┌─────────────────┐
│  User Query  │────▶│  Claude API   │────▶│  Tool Execution  │
│ (plain text) │     │  (tool use)   │     │  (Python/Pandas) │
└─────────────┘     └──────┬───────┘     └────────┬────────┘
                           │                       │
                           ◀───────────────────────┘
                        (results fed back into context)
```

### Available Tools

| Tool | Description |
|------|-------------|
| `inspect_data` | Dataset overview: shape, types, stats, sample rows |
| `query_data` | Execute arbitrary Pandas queries on the dataset |
| `calculate_metric` | Compute metrics: mean, sum, correlation, growth_rate, percentile |
| `detect_anomalies` | Find statistical outliers using IQR or Z-score |
| `generate_summary` | Produce structured executive summary |

## 🚀 Quick Start

```bash
git clone https://github.com/YOUR_USERNAME/business-insights-agent.git
cd business-insights-agent
pip install -r requirements.txt

# Generate sample data
python data/generate_data.py

# Set API key
export ANTHROPIC_API_KEY=your_key_here

# Ask questions
python src/agent.py data/sales_data.csv "What are the top 5 products by profit?"
python src/agent.py data/sales_data.csv "Is there seasonality in our revenue?"
python src/agent.py data/sales_data.csv "Which sales reps are underperforming?"
python src/agent.py data/sales_data.csv "Detect anomalies in discount patterns"
```

### Demo Mode (No API Key)

Without an API key, the agent runs in demo mode showing dataset statistics and instructions for full usage.

## 📊 Sample Questions

- "What is our overall profit margin and how does it vary by region?"
- "Which customer type generates the most revenue per transaction?"
- "Are there any anomalies in our discount patterns?"
- "Compare online vs in-store channel performance"
- "What's the correlation between satisfaction scores and revenue?"
- "Give me a full executive summary of this dataset"

## 🔗 MCP Connection

This project is architecturally aligned with Anthropic's **Model Context Protocol** — the agent follows the same pattern of tool discovery, selection, and execution that MCP servers implement. The tool definitions follow the MCP-compatible JSON schema format, making this easily extensible into a full MCP server.

## 🛠️ Tech Stack

**Core:** Python, Pandas, NumPy
**AI:** Anthropic Claude API (tool use / function calling)
**Architecture:** Agentic loop with tool orchestration

## 🔮 Extending the Agent

Add new tools by:
1. Adding a tool definition to `TOOLS` list (JSON schema)
2. Adding the implementation method to `DataTools` class
3. Claude will automatically discover and use the new tool

Example — adding a chart tool:
```python
# In TOOLS list:
{"name": "create_chart", "description": "Generate a chart specification", ...}

# In DataTools class:
def create_chart(self, chart_type, x_col, y_col): ...
```

## 👩‍💻 Author

**Megha Sharma** — MSc Management (Business Analytics), Swansea University
- Certified: Claude Code in Action, MCP Advanced Topics, AI Fluency (Anthropic)

## 📄 Licence

MIT
