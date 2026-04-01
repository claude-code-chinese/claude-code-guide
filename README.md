# Claude Code国内如何使用 ？最容易懂的 Claude Code 介绍与教学指南（2026年最新）

## 什么是 Claude Code？

Claude Code 是 Anthropic（Claude AI 的开发者）于2025年初推出的命令行工具。它不是简单的代码补全AI，而是“代理式”（agentic）助手，能根据你的自然语言指令，自主规划步骤、执行任务。比如，你说“帮我构建一个React组件”，它会分析你的代码库、生成代码、测试并集成。它生活在你的终端（terminal）中，支持各种编程语言和环境，帮助开发者加速从想法到代码的过程。

与其他AI编码工具（如 GitHub Copilot）不同，Claude Code 更注重整个项目级别的协作：它能读取整个代码库、使用 bash 命令、查看 git 历史，甚至运行测试。研究显示，使用它能让开发速度提升5倍以上！

### 主要特点和优势
- **代理式工作流**：不只是补代码，还能规划多步任务，如“探索代码结构、提出优化方案”。
- **集成性强**：支持终端、VS Code 扩展，支持 Node.js、React、Express 等热门框架。
- **上下文理解**：通过 CLAUDE.md 文件（一个特殊的 Markdown 文件），它能记住项目细节，如代码风格、常见问题。
- **安全性**：沙箱环境，确保工具不会乱改文件；支持审计日志。
- **2025年新功能**：新增 Skills 模块（可重用工作流），支持 Git 版本控制和市场共享；集成 Claude Agent SDK 用于构建自定义代理。

优势：适合团队协作，减少重复工作；局限：更偏向开发者，不适合非技术用户；需要命令行基础。

## 在中国如何使用 Claude Code？（绕过限制的实用方法）

由于Claude 禁止CN地区访问，直接访问 Anthropic 官网（anthropic.com）或 Claude Code 文档（code.claude.com）可能被屏蔽。下载工具或使用 API 也需要翻墙。但别担心，有简单解决方案！

### 方法：使用 api 代理站（推荐初学者）
[https://api.yixia.ai](https://api.yixia.ai)

## Claude Code 快速入门指南 ​ ​

欢迎使用Claude Code！这个强大的AI编程助手能够帮助您提高编程效率，自动化开发任务。

## 1\. 安装与配置 ​ ​

## 1.1 系统要求 ​ ​

* **操作系统**: macOS 10.15+, Ubuntu 20.04+/Debian 10+, Windows ， Windows via WSL
* **硬件**: 4GB+ RAM
* **软件**: Node.js 18+
* **网络**: 需要互联网连接进行身份验证和AI处理

## 1.2 安装步骤 ​ ​

使用npm进行全局安装：

bash

```
npm install -g @anthropic-ai/claude-code@latest
```

**重要**: 不要使用 `sudo npm install -g`，这可能导致权限问题和安全风险。

**更新**，官方推出了，不依赖于`nodejs` 的客户端：

![image-20251103153006420](https://api.yixia.ai/docs/assets/image-20251103153006420.3wfjm8HH.png)

**安装方式**：

* macOS/Linux

sh

```
curl -fsSL https://claude.ai/install.sh | bash
```

* Homebrew

sh

```
brew install --cask claude-code
```

* Windows

powershell

```
irm https://claude.ai/install.ps1 | iex
```


**老用户迁移：**

如果我们之前已经安装过 Claude Code，迁移方法也非常简单。首先我们要确保关闭所有的 Claude code 会话窗口，然后在终端输入：

这条命令会自动下载原生可执行文件，并替换旧的 npm 版本。但在实测中，建议大家在使用 claude install 后再打开终端输入:

sh

```
npm uninstall -g @anthropic-ai/claude-code
```

通过这条命令就可以确保把旧版本给删除了。

安装完成后，导航到您的项目 目录并启动Claude Code：

bash

```
cd your-awesome-project
claude --version
# 正确显示出版本号，说明安装成功
```

## 2\. API密钥获取与配置 ​ ​

## 2.1 注册账户 ​ ​

1. 访问 https://api.yixia.ai/
2. 点击右上角注册按钮创建新账户
3. 填写必要的注册信息

![注册账户](https://api.yixia.ai/docs/assets/signup.DqY_XY7c.png)

## 2.2 创建API密钥 ​ ​

1. 登录成功后，点击左侧菜单栏的"令牌管理"，进入令牌管理页面
2. 点击“添加令牌”按钮 ![创建令牌](https://api.yixia.ai/docs/assets/createkey1.BlhW2dPI.png)
3. 输入令牌名称，选择默认分组，勾选无限额度，点击“提交”按钮 ![创建新的令牌](https://api.yixia.ai/docs/assets/createkey2.B5uX3KqV.png)
4. 生成并复制您的API密钥 ![创建新的令牌](https://api.yixia.ai/docs/assets/createkey3.C3nql_mL.png)

## 3\. 编辑配置文件 ​ ​

## 3.1 API密钥配置 ​ ​

### 配置文件设置方法 ​ ​

创建或编辑配置文件：

bash

```
# 用户设置 (全局)
~/.claude/settings.json

# 项目设置 (项目级)
.claude/settings.json
```

配置文件示例：

json

```
{
"env": {
"ANTHROPIC_API_KEY": "您的APIkey",
"ANTHROPIC_BASE_URL": "https://api.yixia.ai/",
"CLAUDE_CODE_MAX_OUTPUT_TOKENS":64000,
"CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC":1,
"CLAUDE_MODEL": "Claude模型名称,例如：claude-4-sonnet"
},
"permissions": {
"allow": [],
"deny": []
}
}
```

## 3.2 权限设置（可选） ​ ​

Claude Code采用保守的权限策略，默认需要用户确认可能修改系统的操作。您可以自定义允许的工具列表：

* 使用 `/permissions` 命令添加或移除工具
* 编辑 `settings.json` 文件进行批量配置
* 使用 `--allowedTools` CLI标志设置会话特定权限

## 3.3 工作目录配置（可选） ​ ​

配置Claude可以访问的附加工作目录：

json

```
{
"permissions": {
"additionalDirectories": ["../docs/", "../shared/"]
}
}
```

## 3.4 省流、一键脚本 ​ ​

购买了API之后，只需要修改这个脚本第8行的`readonly API_KEY=""`，填上你的APIkey(令牌)，再将这个脚本保存为`claudecode.sh`，然后打开终端：

bash

```
chmod +x claudecode.sh
./claudecode.sh
```

跟着提示走就好了。

bash

```
#!/bin/bash

# ==============================================================================
# 🔧 配置区域 - 请在这里设置您的 API 配置
# ==============================================================================

# 🔑 API 密钥 - 请填入您的 API 密钥
readonly API_KEY="修改这里"

# 🌐 API 基础地址 - 请填入您的 API 基础地址 (例如: "https://api.yixia.ai/")
readonly API_BASE_URL="https://api.yixia.ai/"

# ==============================================================================
# 以下内容请勿修改
# ==============================================================================

# 脚本常量
readonly CLAUDE_COMMAND="claude"
readonly NPM_PACKAGE="@anthropic-ai/claude-code"
readonly CLAUDE_DIR="$HOME/.claude"
readonly SETTINGS_FILE="$CLAUDE_DIR/settings.json"

# 检测操作系统
detect_os() {
case "$(uname -s)" in
Darwin)
echo "macos"
;;
Linux)
echo "linux"
;;
*)
echo "unknown"
;;
esac
}

# 检查配置是否完整
check_config() {
if [ -z "$API_KEY" ] || [ -z "$API_BASE_URL" ]; then
echo "❌ 配置不完整！请编辑脚本并填入以下信息："
echo " - API_KEY: 您的 API 密钥"
echo " - API_BASE_URL: API 基础地址 (例如: https://api.yixia.ai/)"
exit 1
fi
}

# 安装 Homebrew (仅限 macOS)
install_homebrew() {
if ! command -v brew &> /dev/null; then
echo "正在安装 Homebrew..."
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# 添加 Homebrew 到 PATH
if [[ -f "/opt/homebrew/bin/brew" ]]; then
eval "$(/opt/homebrew/bin/brew shellenv)"
elif [[ -f "/usr/local/bin/brew" ]]; then
eval "$(/usr/local/bin/brew shellenv)"
fi

echo "✅ Homebrew 安装完成"
else
echo "ℹ️ Homebrew 已安装"
fi
}

# 在 macOS 上安装软件包
install_macos_packages() {
install_homebrew

# 安装 Node.js (包含 npm)
if ! command -v node &> /dev/null; then
echo "正在安装 Node.js..."
brew install node
echo "✅ Node.js 安装完成"
else
echo "ℹ️ Node.js 已安装"
fi

# 安装 jq
if ! command -v jq &> /dev/null; then
echo "正在安装 jq..."
brew install jq
echo "✅ jq 安装完成"
else
echo "ℹ️ jq 已安装"
fi

# 安装 Python3
if ! command -v python3 &> /dev/null; then
echo "正在安装 Python3..."
brew install python3
echo "✅ Python3 安装完成"
else
echo "ℹ️ Python3 已安装"
fi
}

# 在 Linux 上安装软件包
install_linux_packages() {
# 检测 Linux 发行版
if command -v apt-get &> /dev/null; then
# Ubuntu/Debian
echo "检测到 Ubuntu/Debian 系统"

# 更新包管理器
echo "正在更新包管理器..."
sudo apt-get update

# 安装 Node.js
if ! command -v node &> /dev/null; then
echo "正在安装 Node.js..."
# 安装 NodeSource 仓库
curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
sudo apt-get install -y nodejs
echo "✅ Node.js 安装完成"
else
echo "ℹ️ Node.js 已安装"
fi

# 安装 jq
if ! command -v jq &> /dev/null; then
echo "正在安装 jq..."
sudo apt-get install -y jq
echo "✅ jq 安装完成"
else
echo "ℹ️ jq 已安装"
fi

# 安装 Python3
if ! command -v python3 &> /dev/null; then
echo "正在安装 Python3..."
sudo apt-get install -y python3 python3-pip
echo "✅ Python3 安装完成"
else
echo "ℹ️ Python3 已安装"
fi

elif command -v yum &> /dev/null; then
# CentOS/RHEL
echo "检测到 CentOS/RHEL 系统"

# 安装 Node.js
if ! command -v node &> /dev/null; then
echo "正在安装 Node.js..."
curl -fsSL https://rpm.nodesource.com/setup_lts.x | sudo bash -
sudo yum install -y nodejs
echo "✅ Node.js 安装完成"
else
echo "ℹ️ Node.js 已安装"
fi

# 安装 jq
if ! command -v jq &> /dev/null; then
echo "正在安装 jq..."
sudo yum install -y jq
echo "✅ jq 安装完成"
else
echo "ℹ️ jq 已安装"
fi

# 安装 Python3
if ! command -v python3 &> /dev/null; then
echo "正在安装 Python3..."
sudo yum install -y python3 python3-pip
echo "✅ Python3 安装完成"
else
echo "ℹ️ Python3 已安装"
fi

elif command -v pacman &> /dev/null; then
# Arch Linux
echo "检测到 Arch Linux 系统"

# 安装 Node.js
if ! command -v node &> /dev/null; then
echo "正在安装 Node.js..."
sudo pacman -S --noconfirm nodejs npm
echo "✅ Node.js 安装完成"
else
echo "ℹ️ Node.js 已安装"
fi

# 安装 jq
if ! command -v jq &> /dev/null; then
echo "正在安装 jq..."
sudo pacman -S --noconfirm jq
echo "✅ jq 安装完成"
else
echo "ℹ️ jq 已安装"
fi

# 安装 Python3
if ! command -v python3 &> /dev/null; then
echo "正在安装 Python3..."
sudo pacman -S --noconfirm python python-pip
echo "✅ Python3 安装完成"
else
echo "ℹ️ Python3 已安装"
fi

else
echo "❌ 不支持的 Linux 发行版，请手动安装以下软件包："
echo " - Node.js (包含 npm)"
echo " - jq"
echo " - python3"
exit 1
fi
}

# 安装 Claude Code
install_claude_code() {
if command -v "$CLAUDE_COMMAND" &> /dev/null; then
echo "ℹ️ Claude Code 已安装"
else
echo "正在安装 Claude Code..."

if ! command -v npm &> /dev/null; then
echo "❌ npm 未安装，无法安装 Claude Code"
exit 1
fi

if ! npm install -g "$NPM_PACKAGE"; then
echo "❌ Claude Code 安装失败"
exit 1
fi

echo "✅ Claude Code 安装完成"
fi
}

# 配置 Claude Code
configure_claude_code() {
echo "正在配置 Claude Code..."

# 创建 .claude 目录
if [ ! -d "$CLAUDE_DIR" ]; then
mkdir -p "$CLAUDE_DIR"
fi

# 备份原配置（如果存在）
if [ -f "$SETTINGS_FILE" ]; then
cp "$SETTINGS_FILE" "$SETTINGS_FILE.backup"
echo "ℹ️ 原配置已备份为 settings.json.backup"
fi

# 创建新的配置文件
cat > "$SETTINGS_FILE" << EOF
{
"env": {
"ANTHROPIC_API_KEY": "$API_KEY",
"ANTHROPIC_BASE_URL": "$API_BASE_URL",
"CLAUDE_CODE_MAX_OUTPUT_TOKENS": 64000,
"CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC": 1
},
"permissions": {
"allow": [],
"deny": []
},
"apiKeyHelper": "echo '$API_KEY'"
}
EOF

echo "✅ 配置文件创建完成"
}

# 主函数
main() {
echo "🚀 Claude Code 自动安装配置脚本"
echo "=================================="

# 检查配置
check_config

# 检测操作系统
OS=$(detect_os)
echo "检测到操作系统: $OS"

# 根据操作系统安装依赖
case "$OS" in
"macos")
install_macos_packages
;;
"linux")
install_linux_packages
;;
*)
echo "❌ 不支持的操作系统: $OS"
exit 1
;;
esac

# 安装 Claude Code
install_claude_code

# 配置 Claude Code
configure_claude_code

echo "🎉 所有配置完成！"
echo "配置文件位置: $SETTINGS_FILE"
echo "现在您可以使用 'claude' 命令了！"
}

# 运行主函数
main "$@"
```

## 4\. 基础使用 ​ ​

## 4.1 启动方式 ​ ​

### 交互式模式 ​ ​

![Claude进入界面](https://api.yixia.ai/docs/assets/cc1.B5tB747V.png)

### 带初始提示启动 ​ ​

bash

```
claude "explain this project"
```

### 非交互式模式 ​ ​

bash

```
claude -p "explain this function"
```

### 处理管道输入 ​ ​

bash

```
cat logs.txt | claude -p "explain"
```

## 4.2 常用命令 ​ ​

* `claude update` - 更新claude code到最新版本
* `claude -c` - 继续最近的对话
* `claude -r <session-id>` - 恢复特定会话
* `claude mcp` - 配置MCP服务器

## 4.3 快捷键 ​ ​

### 通用控制 ​ ​

* `Ctrl+C`: 取消当前输入或生成
* `Ctrl+D`: 退出Claude Code会话
* `Ctrl+L`: 清除终端屏幕
* `Up/Down`: 浏览命令历史
* `Esc + Esc`: 编辑上一条消息

### 多行输入 ​ ​

* `\ + Enter`: 适用于所有终端
* `Option+Enter`: macOS默认
* `Shift+Enter`: 执行`/terminal-setup`后可用

## 5\. 高级功能 ​ ​

## 5.1 CLI参考 ​ ​

Claude Code提供丰富的命令行选项来自定义其行为：

### 基础CLI命令 ​ ​

命令

描述

示例

`claude`

启动交互式REPL

`claude`

`claude "query"`

带初始提示启动REPL

`claude "explain this project"`

`claude -p "query"`

通过SDK查询后退出

`claude -p "explain this function"`

`cat file | claude -p "query"`

处理管道内容，将文件内容通过管道传递给Claude Code 进行分析或处理

`cat logs.txt | claude -p "explain"`

`claude -c`

继续最近的对话

`claude -c`

`claude update`

更新到最新版本

`claude update`

`claude commit`

创建一个Git提交

`claude commit`

### 重要CLI标志 ​ ​

标志

描述

示例

`--allowedTools`

允许的工具列表

`--allowedTools "Bash(git log:*)" "Read"`

`--verbose`

启用详细日志

`claude --verbose`

`--model`

设置使用的模型

`claude --model claude-sonnet-4`

`--permission-mode`

指定权限模式

`claude --permission-mode plan`

`--dangerously-skip-permissions`

跳过权限提示（谨慎使用）

`claude --dangerously-skip-permissions`

## 5.2 交互式模式 ​ ​

### Vim模式 ​ ​

启用vim风格编辑：

#### 模式切换 ​ ​

* `Esc`: 进入NORMAL模式
* `i`: 在光标前插入
* `a`: 在光标后插入
* `o`: 在下方新建行

#### 导航（NORMAL模式） ​ ​

* `h/j/k/l`: 左/下/上/右移动
* `w`: 下一个单词
* `0`: 行首
* `$`: 行尾
* `gg`: 文本开头
* `G`: 文本结尾

## 5.3 斜杠命令 ​ ​

Claude Code提供多种斜杠命令来增强交互体验：

### 基础命令 ​ ​

命令

描述

示例

`/help`

显示帮助信息

`/help`

`/clear`

清除对话历史

`/clear`

`/config`

管理配置

`/config`

`/permissions`

管理权限

`/permissions`

`/vim`

启用vim模式

`/vim`

`/compact`

压缩对话,降低Token使用量

`/compact`

`/doctor`

检查安装健康状况

`/doctor`

### 高级命令 ​ ​

命令

描述

功能

`/init`

初始化项目

自动生成CLAUDE.md文件

`/terminal-setup`

设置终端

配置键盘快捷键

`/project:<command>`

项目特定命令

运行项目自定义命令

### 自定义斜杠命令 ​ ​

您可以创建自定义斜杠命令：

1. 在 `.claude/commands/` 目录创建Markdown文件
2. 文件名即为命令名
3. 内容为命令模板，可使用 `$ARGUMENTS` 占位符

示例：`.claude/commands/fix-github-issue.md`

markdown

```
请分析并修复GitHub issue: $ARGUMENTS。

请按以下步骤操作：
1. 使用 `gh issue view` 获取issue详情
2. 理解问题描述
3. 搜索相关代码文件
4. 实现必要的修复
5. 编写并运行测试
6. 确保代码通过lint检查
7. 创建描述性的提交信息
8. 推送并创建PR
```

## 6\. 实战教程 ​ ​

## 6.1 理解新代码库 ​ ​

### 快速了解代码库概况 ​ ​

如果你刚加入一个新项目，想要快速了解其结构，你可以按照以下步骤进行：

1. 进入项目根目录：`cd /path/to/project`
2. 启动 Claude Code：`claude`
3. 请求代码库的概况：`> 给我一个代码库概览`
4. 深入了解特定组件：
* `> 解释这里使用的主要架构模式`
* `> 关键的数据模型有哪些？`
* `> 认证是如何处理的？`

**小技巧：**

* 从广泛的问题入手，然后逐步聚焦到具体领域
* 询问项目中使用的编码约定和模式
* 请求项目特定术语的词汇表

### 查找相关代码 ​ ​

当你需要定位与某个功能相关的代码时，可以按如下方式操作：

1. 请求 Claude 查找相关文件：`> 查找处理用户认证的文件`
2. 获取组件交互的上下文：`> 这些认证文件是如何协同工作的？`
3. 了解执行流程：`> 从前端到数据库，跟踪登录过程`

**小技巧：**

* 明确你想要查找的内容
* 使用项目中领域特有的语言

## 6.2 高效修复Bug ​ ​

### 诊断错误消息 ​ ​

遇到错误时，你可以通过以下方法找出并修复问题：

1. 与 Claude 分享错误消息：`> 我在运行 npm test 时看到错误`
2. 请求修复建议：`> 提供一些修复 user.ts 中 @ts-ignore 的方法`
3. 应用修复：`> 更新 user.ts，添加你建议的 null 检查`

**小技巧：**

* 告诉 Claude 用于重现问题的命令，并提供堆栈跟踪
* 提及任何重现错误的步骤
* 说明错误是间歇性的还是一致性的

## 6.3 代码重构 ​ ​

### 现代化旧代码 ​ ​

当需要更新旧代码，采用现代的编程模式时，可以按照以下步骤进行：

1. 识别要重构的旧代码：`> 查找我们代码库中弃用的 API`
2. 请求重构建议：`> 建议如何重构 utils.js，使用现代 JavaScript 特性`
3. 安全地应用更改：`> 重构 utils.js，使用 ES2024 特性，同时保持原有行为`
4. 验证重构：`> 对重构后的代码运行测试`

**小技巧：**

* 向 Claude 询问现代方法的好处
* 要求在需要时保持向后兼容性
* 进行小步、可测试的增量式重构

## 6.4 处理测试 ​ ​

### 添加测试覆盖率 ​ ​

若需要为未覆盖的代码添加测试，可以按如下步骤进行：

1. 识别未经测试的代码：`> 查找 NotificationsService.swift 中未覆盖的函数`
2. 生成测试框架：`> 为通知服务添加测试`
3. 添加有意义的测试用例：`> 为通知服务中的边缘情况添加测试用例`
4. 运行并验证测试：`> 运行新测试，修复任何失败`

**小技巧：**

* 要求覆盖边缘情况和错误条件的测试
* 根据需要请求单元测试和集成测试
* 请 Claude 解释测试策略

## 6.5 创建Pull Request ​ ​

### 生成全面的PR ​ ​

当你需要为你的更改创建一个文档清晰的 pull request 时，按以下步骤操作：

1. 总结你的更改：`> 总结我对认证模块所做的更改`
2. 使用 Claude 生成 PR：`> 创建一个 PR`
3. 审查并完善描述：`> 增强 PR 描述，补充有关安全性改进的更多信息`
4. 添加测试信息：`> 添加关于如何测试这些更改的信息`

**小技巧：**

* 直接要求 Claude 为你创建一个 PR
* 提交前审查 Claude 生成的 PR
* 要求 Claude 突出潜在的风险或注意事项

## 6.6 处理文档 ​ ​

### 生成代码文档 ​ ​

如果你需要添加或更新代码文档，可以按照以下步骤操作：

1. 识别没有适当 JSDoc 注释的代码：`> 查找 auth 模块中没有适当 JSDoc 注释的函数`
2. 生成文档：`> 为 auth.js 中未注释的函数添加 JSDoc 注释`
3. 审查和增强文档：`> 改进生成的文档，增加更多上下文和示例`
4. 验证文档：`> 检查文档是否符合我们项目的标准`

**小技巧：**

* 指定你所需的文档风格（如 JSDoc、docstrings 等）
* 在文档中要求提供示例
* 为公共 API、接口和复杂逻辑请求文档

## 6.7 使用图像 ​ ​

### 分析图像和屏幕截图 ​ ​

如果你需要在代码库中使用图像或让 Claude 分析图像内容，按照以下步骤进行：

1. 将图像添加到对话中：

* 将图像拖入 Claude Code 窗口
* 复制并粘贴图像至 CLI (ctrl+v)
* 提供图像路径：`> 分析此图像：/path/to/your/image.png`
2. 请求 Claude 分析图像：

* `> 这张图显示了什么？`
* `> 描述一下这张截图中的 UI 元素`
* `> 这个图表中有什么问题吗？`
3. 使用图像获取上下文：

* `> 这是错误的截图，是什么导致了它？`
* `> 这是当前的数据库架构，我们需要如何修改以支持新特性？`
4. 从图像中获取代码建议：

* `> 生成与这个设计草图匹配的 CSS`
* `> 用什么 HTML 结构可以重建这个组件？`

**小技巧：**

* 当文本描述不清晰或繁琐时，可以使用图像
* 提供错误、UI 设计或图表的截图，以便获得更好的上下文
* 可以在对话中使用多个图像

## 6.8 设置项目记忆 ​ ​

### 创建有效的CLAUDE.md文件 ​ ​

为了存储重要的项目信息、约定和常用命令，你可以设置一个 CLAUDE.md 文件：

为你的代码库初始化 CLAUDE.md 文件：`> /init`

**小技巧：**

* 包括常用命令（如构建、测试、检查）以避免重复搜索
* 记录代码风格偏好和命名约定
* 添加特定于项目的重要架构模式

你可以将 CLAUDE.md 文件添加到你运行 Claude 的文件夹、父目录（Claude 会自动读取这些文件）或子目录（Claude 会按需拉取这些文件）。

## 6.9 Unix风格实用程序 ​ ​

### 添加到验证过程 ​ ​

将 Claude 添加到你的构建脚本：

json

```
// package.json
{
...
"scripts": {
...
"lint:claude": "claude -p '你是一个代码检查工具，请查看与主分支的差异，并报告任何与拼写错误相关的问题。每个问题的文件名和行号要在一行上，描述在第二行。不要返回任何其他文字。'"
}
}
```

### 管道输入输出 ​ ​

通过 Claude 管道传输数据：

bash

```
cat build-error.txt | claude -p '简明扼要地解释这个构建错误的根本原因' > output.txt
```

## 6.10 MCP服务器配置 ​ ​

### 配置MCP服务器 ​ ​

如果你想通过将 Claude 连接到专用工具和外部服务器来增强其功能，请按以下步骤操作：

1. 添加 MCP Stdio 服务器：

* 基本语法：`claude mcp add <name> <command> [args...]`
* 示例：添加本地服务器：`claude mcp add my-server -e API_KEY=123 -- /path/to/server arg1 arg2`
2. 管理 MCP 服务器：

* 列出所有配置的服务器：`claude mcp list`
* 获取特定服务器的详细信息：`claude mcp get my-server`
* 删除服务器：`claude mcp remove my-server`

**小技巧：**

* 使用 `-s` 或 `--scope` 标志与 `project`（默认）或 `global` 一起指定配置的存储位置
* 使用 `-e` 或 `--env` 标志设置环境变量（例如，`-e KEY=value`）
* MCP 遵循客户端-服务器架构，Claude Code（客户端）可以连接到多个专用服务器

### 连接到Postgres MCP服务器 ​ ​

如果你希望 Claude 具有只读权限来查询 PostgreSQL 数据库和检查架构，按照以下步骤操作：

1. 添加 Postgres MCP 服务器：

bash

```
claude mcp add postgres-server /path/to/postgres-mcp-server --connection-string "postgresql://user:pass@localhost:5432/mydb"
```

2. 使用 Claude 查询数据库：
* `> 描述一下我们用户表的架构`
* `> 系统中最新的订单有哪些？`
* `> 展示客户和发票之间的关系`

**小技巧：**

* Postgres MCP 服务器提供只读访问，确保安全
* Claude 可以帮助你探索数据库结构并运行分析查询
* 使用它可以快速了解不熟悉项目中的数据库架构
* 确保你的连接字符串使用具有所需最低权限的凭据

## 7\. 进阶特性 ​ ​

## 7.1 IDE集成 ​ ​

Claude Code 支持连接到主流IDE：

* 您可以直接在IDE中看到Claude Code的改动，在IDE中与其交互
* Claude Code 现在支持 VSCode 与 JetBrains
* 如果您使用Linux / MacOS，您可以直接使用该插件
* 如果您使用VSCode，在VSCode的内置终端唤起Claude Code，插件将被自动安装
* 如果您使用JetBrains，您需要通过此链接下载：Claude Code \[Beta\] - IntelliJ IDEs Plugin
* 您可能需要手动指定IDE或检查IDE连接，通过以下命令测试：`> /ide`
* 如果您使用 VSCode+WSL，请您提前在VSCode 插件商店安装 WSL 插件
* 对于更多的用法，您可以参考Claude Code的官方文档

## 7.2 模型切换和配置 ​ ​

Claude Code 支持 Claude 4 Opus 与 Claude 4 Sonnet 灵活切换：

* 我们强烈推荐您使用Claude 4 Sonnet，其使用体验与Claude 4 Opus没有明显差别，但计费倍率仅为1/5
* 我们为您默认选择了Claude 4 Sonnet，您可以在登录后在配置中修改这一选项
* 如果您没有在站点中关闭"强制使用 Sonnet"，您在/model中切换的模型不会被切换
* 在 Claude Code 中使用此命令切换模型：`> /model`

## 7.3 上下文管理 ​ ​

Claude Code 支持压缩上下文以节省点数：

* Claude Code 通常会有长上下文，我们建议您使用以下斜杠命令来压缩以节省点数，较长的上下文往往需要更多点数
* `/compact [您的描述]`

## 7.4 对话恢复 ​ ​

Claude Code 能够恢复以前的对话：

* 使用以下命令可以恢复您上次的对话：`claude --continue`
* 这会立即恢复您最近的对话，无需任何提示
* 您如果需要显示时间，可以输入此命令：`claude --resume`
* 这会显示一个交互式对话选择器，显示：
* 对话开始时间
* 初始提示或对话摘要
* 消息数量
* 使用箭头键导航并按Enter选择对话，您可以使用这个方法选择上下文

## 7.5 图像处理 ​ ​

Claude Code 可以处理图像信息：

* 您可以使用以下任何方法：
* 将图像拖放到Claude Code窗口中（在MacOS上）
* 复制图像并使用Ctrl+v粘贴到CLI中（在MacOS上）
* 提供图像路径：`> 分析这个图像：/path/to/your/image.png`
* 您可以完全使用自然语言要求他进行工作，如：
* `> 这是错误的截图。是什么导致了它？`
* `> 这个图像显示了什么？`
* `> 描述这个截图中的UI元素`
* `> 生成CSS以匹配这个设计模型`
* `> 什么HTML结构可以重新创建这个组件？`

## 7.6 深入思考 ​ ​

Claude Code 支持深入思考：

* 您需要通过自然语言要求其进行深入思考
* `> 我需要使用OAuth2为我们的API实现一个新的身份验证系统。深入思考在我们的代码库中实现这一点的最佳方法。`
* `> 思考这种方法中潜在的安全漏洞`
* `> 更深入地思考我们应该处理的边缘情况`
* 推荐您在使用复杂问题的时候使用这一功能，这也会消耗大量的额度点数

## 7.7 Git高级操作 ​ ​

Claude Code 支持使用自然语言操作Git，如：

* `> 提交我的更改`
* `> 创建一个 pr`
* `> 哪个提交在去年十二月添加了 markdown 测试？`
* `> 在 main 分支上变基并解决任何合并冲突`

### 使用Git工作树 ​ ​

您可以使用工作树创建隔离的编码环境：

* 如果您需要同时处理多个任务，并在Claude Code实例之间完全隔离代码，您可以使用此功能
* Git工作树允许您从同一存储库中检出多个分支到单独的目录。每个工作树都有自己的工作目录，文件是隔离的，同时共享相同的Git历史
* 创建新工作树：

bash

```
# 创建带有新分支的工作树
git worktree add ../project-feature-a -b feature-a

# 或使用现有分支创建工作树
git worktree add ../project-bugfix bugfix-123
```

* 在每个工作树中运行Claude Code：

bash

```
# 导航到您的工作树
cd ../project-feature-a

# 在这个隔离环境中运行Claude Code
claude
```

## 7.8 其他高级功能 ​ ​

Claude Code 支持多种高级功能：

* Claude Code可以被用作类Unix工具
* Claude Code支持自定义斜杠指令
* Claude Code支持使用$ARGUMENTS添加命令参数
* Claude Code支持高级设置配置
* Claude Code支持GitHub Actions集成
* Claude Code支持SDK开发
* Claude Code支持模型上下文协议（MCP）

## 8\. 常见问题解决 ​ ​

## 8.1 存储记忆问题 ​ ​

### Claude Code如何存储记忆？ ​ ​

Claude Code 将记忆存储在`~/.claude`中，如果没有特殊要求，请不要删除此目录。

## 8.2 模型名称问题 ​ ​

### 为什么偶尔回复错误的模型名称？ ​ ​

TryAllAI 向您承诺不会替换您请求的模型，绝不掺杂其他模型。这是由于Claude Code在使用简单任务时，不会使用Claude 4 系列模型。

## 8.3 命令行错误 ​ ​

### 命令行参数执行错误怎么办？ ​ ​

此类问题在WSL上常见，是Agent自身的错误。我们推荐您使用MacOS/Ubuntu，这类环境往往问题较少。

## 8.4 清理Claude Code ​ ​

### 如何彻底清理Claude Code？ ​ ​

您可以执行以下命令清理Claude Code的登录信息：

## 8.5 API错误 ​ ​

### 遇到API Error、Tools Error怎么办？ ​ ​

这通常是网络问题，请您退出后使用`claude -c`重新执行。如果问题依然存在，请联系售后支持。

## 8.6 OAuth验证错误 ​ ​

### OAuth验证错误的解决方案 ​ ​

* 请您确保环境变量中没有配置任何代理再进行登录验证
* 如果问题仍然存在，请您无视弹出的浏览器并复制终端中的链接并打开，通过验证码方式验证

## 8.7 响应超时问题 ​ ​

### 长时间没有响应怎么办？ ​ ​

* 我们建议您按下ctrl+c并重启Claude Code，这往往是网络问题
* 如果命令行仍然无响应，我们建议您杀死进程并重新进行会话，这将不会影响您的工作进度
* 您可以通过以下命令恢复上次的会话：`claude -c`

## 9\. 结语 ​ ​

Claude Code是一个强大的AI编程助手，通过合理的配置和使用，可以显著提高您的开发效率。建议您：

1. 从基础功能开始，逐步探索高级特性
2. 根据项目需求定制配置
3. 利用CLAUDE.md文件记录项目特定信息
4. 合理使用权限管理确保安全
5. 探索MCP和自定义命令扩展功能

祝您使用愉快！如有问题，请参考官方文档或社区支持。

## 基本使用教学（从零起步）

启动 Claude Code：终端运行 `claude`，进入交互模式。

### 示例1：探索代码库
- 输入："探索项目结构，找出认证逻辑。"
- Claude 会用 bash 命令列目录、grep 搜索，输出报告。

### 示例2：生成代码
- 输入："为 UserService 写单元测试。"
- Claude 规划步骤、生成 test 文件、建议运行 `npm test`。

### 示例3：调试问题
- 输入："修复这个错误：TypeError in auth.js line 45。"
- 它分析上下文、建议修复，并编辑文件（需确认）。

### 示例4：使用 Skills
- 安装 "CODE_REVIEW" Skill。
- 输入：`claude use CODE_REVIEW project_path=~/my-app`
- 它自动审查代码，生成报告。

**提示**：用 /slash 命令如 `/slashplan` 预览步骤；多会话并行（如 git worktrees）；日志查看 `~/.claude/activity.log`。

## 高级用法示例

- **前端开发**： "构建一个带 Zod 验证的 React 表单组件。" Claude 生成 hooks、组件、测试。
- **后端集成**： "用 Prisma 和 JWT 实现 Express 认证路由。" 包括 Docker 配置。
- **CI/CD**：在 GitHub Actions 中集成 Claude 为 PR 自动审查。
- **自定义代理**：用 Claude Agent SDK 构建专属工具（如 Supabase 集成）。

## 注意事项和局限性

- **性能**：大项目需优化提示；免费版限额低，建议 Pro。
- **安全**：别分享 API Key；Skills 有权限控制。
- **中国特有**：网络不稳时用代理；支付用 FastGPTPlus 避开信用卡问题。
- **学习曲线**：新手先练简单任务，参考官方最佳实践。

Claude Code 让编码更高效有趣！如果有问题，欢迎评论或查官方文档。2025年，它将继续更新，敬请期待。
