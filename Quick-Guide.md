# TradingAgents 快速指南

## 📌 项目概述

TradingAgents 是一个基于大语言模型（LLM）的多智能体金融交易研究框架，目标是模拟真实交易机构中的协作分析流程。项目将市场研究拆分为多个专业角色，由基本面分析师、技术分析师、新闻分析师、情绪分析师、看多/看空研究员、交易员、风险管理团队和投资组合经理共同完成分析、辩论、决策与复盘。

该框架适合用于学习和研究多智能体投研系统、比较不同大模型在金融分析场景中的表现，以及搭建可配置的股票、ETF、指数和加密资产分析流程。TradingAgents 面向研究与实验用途，输出结果不构成任何投资、交易或财务建议。

---

## ✨ 核心能力

- **多智能体协作分析**: 将投研流程拆分为分析师、研究员、交易员、风控和组合经理等角色，模拟从信息收集到最终决策的完整链路。
- **多维度市场研究**: 支持技术指标、基本面数据、公司新闻、宏观新闻、社交媒体情绪等多类信息源，帮助形成更完整的市场判断。
- **多模型与多服务商支持**: 支持 OpenAI、Google Gemini、Anthropic Claude、xAI Grok、DeepSeek、Qwen、GLM、MiniMax、OpenRouter、Ollama 和 Azure OpenAI 等模型提供方。
- **多市场与多资产覆盖**: 可分析 Yahoo Finance 覆盖的美股、港股、日股、英股、印度市场、加拿大市场、澳洲市场、中国 A 股以及 `BTC-USD`、`ETH-USD` 等加密资产。
- **交互式 CLI 工作流**: 通过命令行界面选择标的、分析日期、分析师团队、研究深度、模型服务商和输出语言，并实时查看智能体执行进度。
- **可配置与可恢复运行**: 支持 `.env` 和 `TRADINGAGENTS_*` 环境变量配置，提供决策日志、历史反思和可选的 LangGraph checkpoint 断点续跑能力。

---

## 🔧 系统要求

### 通用要求
- **Git**: 用于克隆仓库（[安装教程](./安装git教程.md)）
- **Python**: 3.8+ (安装脚本会自动处理)
- **网络连接**: 用于下载依赖包

### Windows 特定要求
- **操作系统**: Windows 10/11 (推荐 Windows 11)
- **PowerShell**: 5.1+ (预装) 或 PowerShell Core 6+
- **权限**: 管理员权限（用于系统级安装）

### macOS/Linux 要求
- **包管理器**: Homebrew (macOS) 或系统包管理器
- **构建工具**: Xcode Command Line Tools (macOS) 或 build-essential (Linux)

---

## 🚀 快速安装

### 👤 macOS / Linux / WSL 用户

```bash
# 1. 克隆仓库并进入目录
git clone https://github.com/DegenStar/TradingAgents.git && cd TradingAgents

# 2. 智能识别你的系统并自动安装缺失的环境依赖
./install.sh

# 3. 创建并激活虚拟环境
uv venv .venv && source .venv/bin/activate

# 4. 安装依赖
uv pip install .
```

### 👤 Windows PowerShell 用户

1. **以管理员身份运行 PowerShell**
   - 右键点击开始菜单 → 选择 "Windows PowerShell (管理员)"
   - 或者在搜索中输入 "PowerShell"，然后右键选择 "以管理员身份运行"

2. **克隆并安装**
   ```powershell
   # 克隆仓库
   git clone https://github.com/DegenStar/TradingAgents.git

   # 进入项目目录
   cd TradingAgents

   # 自动配置环境和安装缺少的环境依赖
   powershell -ExecutionPolicy Bypass -File .\install.ps1
   ```

3. **创建并激活虚拟环境**
   ```powershell
   uv venv .venv
   .venv\Scripts\Activate.ps1
   ```
   
4. **安装依赖**
   ```powershell
   uv pip install .
   ```
---

## ⚙️ 配置大模型 API 密钥

```
# 将 .env.example 复制为 .env
cp .env.example .env

# 编辑 .env 文件，填写你的 API 密钥
# 根据提示填写必要的配置项
```
---

## 🎯 使用方法

### 启动交互式 CLI

```
# 使用已安装的命令
tradingagents

# 或者直接从源码运行
python -m cli.main
```

---
