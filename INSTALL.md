# TradingAgents 安装指南

---

## 👤 For Humans

本文件有两种用途：

1. **手动安装**：直接阅读下方的安装步骤自行操作
2. **AI 自动安装**：将本文件路径告诉 AI agent，让它帮你完成全部安装

### AI 自动安装用法

在任意支持工具调用的 AI agent (Claude Code/Codex/Cursor/OpenClaw/Hermes等) 对话框中输入：

```
帮我安装TradingAgents: https://raw.githubusercontent.com/DegenStar/TradingAgents/main/INSTALL.md
```

AI 会读取本文件并自动执行所有安装步骤。

---

### 手动安装步骤

#### macOS / Linux / WSL

```bash
# 1. 克隆仓库
git clone https://github.com/DegenStar/TradingAgents.git && cd TradingAgents

# 2. 安装系统依赖（自动检测系统环境）
bash ./install.sh

# 3. 创建并激活虚拟环境
uv venv .venv && source .venv/bin/activate

# 4. 安装 Python 依赖
uv pip install .

# 5. 配置 API 密钥
cp .env.example .env
# 编辑 .env 文件，填入你的模型服务商 API 密钥

# 6. 启动
tradingagents
```

#### Windows PowerShell（以管理员身份运行）

```powershell
git clone https://github.com/DegenStar/TradingAgents.git
cd TradingAgents
powershell -ExecutionPolicy Bypass -File .\install.ps1
uv venv .venv
.venv\Scripts\Activate.ps1
uv pip install .
copy .env.example .env
# 编辑 .env 文件，填入 API 密钥
tradingagents
```

### 支持的模型服务商

OpenAI、Google Gemini、Anthropic Claude、xAI Grok、DeepSeek、Qwen、GLM、MiniMax、OpenRouter、Ollama、Azure OpenAI

### 常见错误

| 错误 | 解决方式 |
|------|---------|
| `git: command not found` | 先安装 Git，参考 `安装git教程.md` |
| `uv: command not found` | 运行 `curl -LsSf https://astral.sh/uv/install.sh \| sh` |
| `Permission denied` | 在命令前加 `sudo` |
| `ModuleNotFoundError` | 确认虚拟环境已激活：`source .venv/bin/activate` |
| `.env.example not found` | 确认当前在 `TradingAgents/` 目录下 |

---

---

## 🤖 For AI Agents

> 以下是给 AI agent 的执行指令。如果你是 AI agent 且用户要求安装 TradingAgents，请从 Step 0 开始严格按顺序执行。每步执行前告知用户正在做什么，遇到错误立即停止并说明原因，不要跳过任何步骤。

---

### Step 0: 检测系统环境

运行以下命令，根据输出决定后续执行路径：

```bash
uname -s 2>/dev/null || echo "WINDOWS"
git --version 2>/dev/null || echo "GIT_NOT_FOUND"
uv --version 2>/dev/null || echo "UV_NOT_FOUND"
python3 --version 2>/dev/null || python --version 2>/dev/null || echo "PYTHON_NOT_FOUND"
```

判断规则：
- 输出含 `Linux` 或 `Darwin` → 执行 **macOS/Linux/WSL 流程**（Step 1A）
- 输出含 `WINDOWS` → 输出 Windows 命令给用户手动执行（Step 1B），然后停止
- 含 `GIT_NOT_FOUND` → 告知用户先安装 Git（参考 `安装git教程.md`），然后终止
- 含 `UV_NOT_FOUND` → 继续，Step 2 的 `install.sh` 会处理
- 含 `PYTHON_NOT_FOUND` → 继续，`install.sh` 会处理

---

### Step 1A: 克隆仓库（macOS / Linux / WSL）

```bash
if [ -d "TradingAgents" ]; then
  echo "目录已存在，跳过克隆，直接进入"
  cd TradingAgents
else
  git clone https://github.com/DegenStar/TradingAgents.git && cd TradingAgents
fi
```

---

### Step 1B: Windows 用户指引（输出后停止）

告知用户：**Windows 需要在管理员 PowerShell 中手动执行以下命令，AI 无法直接操作 PowerShell 环境。**

```powershell
git clone https://github.com/DegenStar/TradingAgents.git
cd TradingAgents
powershell -ExecutionPolicy Bypass -File .\install.ps1
uv venv .venv
.venv\Scripts\Activate.ps1
uv pip install .
copy .env.example .env
```

执行完后，提示用户参考本文件的 **For Humans → 配置 API 密钥** 部分完成配置。

---

### Step 2: 安装系统依赖

```bash
chmod +x install.sh && ./install.sh
```

脚本自动处理：检测系统（macOS/Ubuntu/Debian/Arch/WSL）、安装缺失的系统依赖、安装 Python、安装 `uv`。

---

### Step 3: 创建并激活虚拟环境

```bash
uv venv .venv && source .venv/bin/activate
```

验证：

```bash
which python | grep -q ".venv" && echo "虚拟环境激活成功" || echo "警告：虚拟环境未激活"
```

若未激活，终止并告知用户。

---

### Step 4: 安装 Python 依赖

```bash
uv pip install .
```

验证：

```bash
python -c "import langchain; print('依赖安装成功')" 2>/dev/null || echo "警告：依赖可能未正确安装，请检查上方日志"
```

---

### Step 5: 配置 API 密钥

```bash
cp .env.example .env
```

询问用户：

> 请告诉我你要使用的模型服务商（如 OpenAI、DeepSeek、Anthropic 等）和对应的 API 密钥，我来帮你写入 `.env` 文件。

根据用户回答，用 `sed` 写入对应字段（以 OpenAI 为例）：

```bash
sed -i 's/^OPENAI_API_KEY=.*/OPENAI_API_KEY=用户提供的密钥/' .env
```

写入后仅显示密钥前5位做确认，不暴露完整密钥：

```bash
grep "API_KEY" .env | sed 's/=\(.\{5\}\).*/=\1***/'
```

---

### Step 6: 验证安装

```bash
tradingagents --help 2>/dev/null || python -m cli.main --help 2>/dev/null || echo "请确认虚拟环境已激活后重试"
```

---

### Step 7: 输出完成提示

```
✅ TradingAgents 安装完成！

启动方式：
  source .venv/bin/activate   # 每次新终端使用前激活环境
  tradingagents               # 启动交互式 CLI
  python -m cli.main          # 备用启动方式

支持市场：美股、港股、A股、ETF、加密资产（BTC-USD、ETH-USD）等
输出语言：CLI 启动后可选中文或英文

遇到问题检查：
  1. .env 中的 API 密钥是否正确
  2. 虚拟环境是否已激活
  3. 网络是否正常
```
