---
title: Claude Code CLI 国内安装指南（Windows + Mac）
date: 2026-06-06 18:29:38
updated: 2026-06-06 18:29:38
description: 面向国内用户的 Claude Code CLI 安装教程，覆盖 Windows 与 Mac 的 Node.js、Git、npm 镜像、API 配置和常见问题。
cover: /img/covers/zhizhi-default-cover.png
categories:
  - Claude Code
tags:
  - Claude Code
  - CLI
  - Windows
  - macOS
  - 安装指南
---

> **适用版本：** Claude Code CLI（2026 年最新版）  
> **适用人群：** 开发者、愿意用终端的用户  
> **本文特点：** 全程复制粘贴即可，无需科学上网

---

## 目录

1. [CLI 版适合谁？](#1-cli-版适合谁)
2. [前置准备](#2-前置准备)
3. [Mac 安装](#3-mac-安装)
4. [Windows 安装](#4-windows-安装)
5. [配置国内 API（最重要的一步）](#5-配置国内-api最重要的一步)
6. [首次启动](#6-首次启动)
7. [常用命令速查](#7-常用命令速查)
8. [常见问题](#8-常见问题)

---

## 1. CLI 版适合谁？

CLI（Command Line Interface）就是**在终端里跑的命令行工具**，适合：
- 习惯用终端的开发者
- 想把 AI 编程集成到工作流的用户
- 需要远程 SSH 连接服务器使用的场景

**跟桌面版的区别：**

| | CLI 版 | 桌面版 |
|--|--------|--------|
| 界面 | 终端文字界面（TUI） | 图形窗口 |
| 启动方式 | 命令行 `claude` | 双击图标 |
| 适合场景 | 开发工作流、自动化 | 日常编程、可视化操作 |
| 资源占用 | 更低 | 更高 |

> 💡 **如果你不习惯用终端，推荐用桌面版**，看我另一篇文章即可。

---

## 2. 前置准备

### 2.1 安装 Node.js（必须）

Claude Code CLI 依赖 Node.js，需要 **18 以上**，推荐 **22 LTS**。

**Mac 用户：**
```bash
# 用 Homebrew 安装（一行搞定）
brew install node

# 验证
node -v   # 看到 v22.x.x 就行
npm -v    # 看到 10.x.x 就行
```

**Windows 用户：**
1. 打开浏览器访问 **<https://nodejs.org>**（或中文镜像 <https://nodejs.org.cn>）
2. 下载 **LTS 版本**（左侧按钮，推荐给大多数用户）
3. 双击安装包，一路点"下一步"即可
4. 安装完成后，打开 PowerShell 验证：
   ```powershell
   node -v
   npm -v
   ```

### 2.2 安装 Git（重要）

Claude Code 依赖 Git 来读写文件。

**Mac：** 通常自带，没有的话运行：
```bash
brew install git
```

**Windows：**
1. 下载 <https://git-scm.com/downloads/win>
2. 双击安装，**关键一步：** 在"调整 PATH 环境"页，选 **"从命令行使用 Git"**
3. 安装完成后重启 PowerShell，验证：
   ```powershell
   git --version
   ```

### 2.3 配置 npm 国内镜像（加速下载）

**这一步必做，否则下载会卡死或极慢：**
```bash
npm config set registry https://registry.npmmirror.com
```

---

## 3. Mac 安装

提供两种方式，**推荐方式一（npm）**。

### 方式一：npm 安装（推荐，国内可用）

```bash
npm install -g @anthropic-ai/claude-code --registry=https://registry.npmmirror.com
```

> 如果提示权限错误，不要用 `sudo`，改用：
> ```bash
> mkdir -p ~/.npm-global
> npm config set prefix ~/.npm-global
> # 然后把下面这行加到 ~/.zshrc 或 ~/.bashrc 文件末尾
> export PATH=~/.npm-global/bin:$PATH
> # 重新打开终端，再运行 npm install
> ```

### 方式二：Homebrew 安装

适合已经用 Homebrew 的用户：
```bash
brew install --cask claude-code
```

### 验证安装

```bash
claude --version
```

看到版本号（如 `v0.3.x`）即成功。

---

## 4. Windows 安装

### 方式一：npm 安装（推荐，国内可用）

以**管理员身份**打开 PowerShell：
```powershell
npm install -g @anthropic-ai/claude-code --registry=https://registry.npmmirror.com
```

> 如果提示 `claude` 命令找不到，把 npm 全局路径加入 PATH：
> ```powershell
> $npmPrefix = npm config get prefix
> [Environment]::SetEnvironmentVariable("Path", "$env:Path;$npmPrefix", "User")
> # 然后重启 PowerShell
> ```

### 方式二：WinGet 安装

```powershell
winget install Anthropic.ClaudeCode
```

### 方式三：使用镜像安装脚本

如果 npm 因网络问题失败，可以用社区镜像脚本：

**PowerShell（管理员）：**
```powershell
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser -Force
irm https://www.qiaoqiaoyun.com/claude/boot.ps1 | iex
```

> ⚠️ 镜像脚本由第三方维护，仅供网络受限时备选。

### 验证安装

```powershell
claude --version
```

---

## 5. 配置国内 API（最重要的一步）

> **为什么必须配？** Claude Code 默认连 Anthropic 海外服务器，国内网络**无法直连**。  
> **你需要什么？** 一个 **API Key**（推荐 DeepSeek 或阿里云百炼）。

### 方案 A：用 CC-Switch 图形化配置（推荐，最简单）

[CC-Switch](https://github.com/farion1231/cc-switch) 是一个开源的可视化工具，不用手动改配置。

1. 下载对应系统的版本（Windows `.exe` / Mac `.dmg`）
2. 打开 CC-Switch，点击 **"添加供应商"**
3. 填入信息（以 DeepSeek 为例）：

   | 字段 | 内容 |
   |------|------|
   | 供应商 | DeepSeek |
   | API 地址 | `https://api.deepseek.com/anthropic` |
   | API Key | 你的 DeepSeek Key |
   | 模型 | `deepseek-v4-pro` |

4. 点击 **"启用"**，CC-Switch 会自动写入环境变量
5. 打开终端运行 `claude`，即可正常使用

### 方案 B：手动创建配置文件（一劳永逸）

创建 `~/.claude/settings.json`：

**Mac（在终端运行）：**
```bash
mkdir -p ~/.claude
```

**Windows（在 PowerShell 运行）：**
```powershell
New-Item -ItemType Directory -Force ~/.claude
```

然后创建 `settings.json` 文件，粘贴以下内容之一：

**选 DeepSeek（推荐，国内可直接访问）：**
```json
{
  "env": {
    "ANTHROPIC_AUTH_TOKEN": "sk-你的DeepSeek API Key",
    "ANTHROPIC_BASE_URL": "https://api.deepseek.com/anthropic",
    "ANTHROPIC_MODEL": "deepseek-v4-pro"
  }
}
```

**选阿里云百炼（阿里云官方渠道）：**
```json
{
  "env": {
    "ANTHROPIC_AUTH_TOKEN": "你的阿里云百炼API Key",
    "ANTHROPIC_BASE_URL": "https://dashscope.aliyuncs.com/apps/anthropic",
    "ANTHROPIC_MODEL": "qwen3-coder-plus"
  }
}
```

**选智谱 GLM（国产大模型）：**
```json
{
  "env": {
    "ANTHROPIC_AUTH_TOKEN": "你的智谱API Key",
    "ANTHROPIC_BASE_URL": "https://open.bigmodel.cn/api/anthropic",
    "ANTHROPIC_MODEL": "glm-4.7"
  }
}
```

### 哪里获取 API Key？

| 供应商 | 注册地址 | 特点 |
|--------|---------|------|
| **DeepSeek** | <https://platform.deepseek.com> | 国内可访问，有新用户免费额度 |
| **阿里云百炼** | <https://bailian.console.aliyun.com> | 阿里官方，按量计费 |
| **智谱 GLM** | <https://open.bigmodel.cn> | 国产大模型，兼容性较好 |
| **Kimi** | <https://platform.moonshot.cn> | 国内可访问 |

---

## 6. 首次启动

```bash
# 进入你的项目目录
cd 你的项目

# 启动 Claude Code
claude
```

首次启动会依次出现以下提示：

1. **Choose a theme（选择主题）** → 按回车选默认即可
2. **Security overview（安全提示）** → 按回车继续
3. **Would you like to trust this directory?** → 输入 `y`（信任当前目录）
4. **API Key 提示** → 如果上一步已经配好了 `settings.json`，这里会自动跳过

看到 Claude Code 的交互界面就说明成功了！🎉

---

## 7. 常用命令速查

| 命令 | 作用 |
|------|------|
| `claude` | 启动交互式编程会话 |
| `claude -p "写一个登录页面"` | 直接执行一次性任务 |
| `claude -c` | 继续上一次对话 |
| `claude commit` | 自动生成 Git 提交信息 |
| `claude doctor` | 健康检查（诊断配置问题） |
| `claude update` | 更新到最新版 |
| `/clear` | 在会话中清空上下文 |
| `/cost` | 查看花费 |
| `/model` | 切换模型 |

---

## 8. 常见问题

### Q1：`claude` 命令找不到
**原因：** npm 全局路径不在系统 PATH 中。  
**解决：**
```bash
# 先看看 npm 全局装在哪里
npm config get prefix
# 把输出的路径下的 bin 目录加入 PATH
# Mac: 加到 ~/.zshrc
# Windows: 加到系统环境变量
```

### Q2：npm 安装卡住不动
**原因：** 没有配置国内镜像源。  
**解决：**
```bash
npm config set registry https://registry.npmmirror.com
# 然后重新安装
```

### Q3：启动后提示 "API connection failed"
**原因：** API 端点配置不对，或网络无法连接。  
**解决：** 检查 `settings.json` 中的 `ANTHROPIC_BASE_URL` 是否正确，Key 是否有效。推荐先用 DeepSeek。

### Q4：提示 "Authentication failed"
**原因：** API Key 错误或环境变量未生效。  
**解决：**
- 确认 Key 没写错
- 确认 `settings.json` 中字段名是 `ANTHROPIC_AUTH_TOKEN`（不是 `ANTHROPIC_API_KEY`）
- 重新打开终端再试

### Q5：npm 权限报错 (EACCES)
**原因：** 全局安装需要写权限。  
**解决：** 不要用 `sudo`！用 nvm 管理 Node，或设置自定义路径：
```bash
npm config set prefix ~/.npm-global
# 然后把 ~/.npm-global/bin 加入 PATH
```

### Q6：如何升级？
```bash
npm update -g @anthropic-ai/claude-code --registry=https://registry.npmmirror.com
# 或
claude update
```

---

## 总结：一句话版

| 步骤 | 做什么 |
|------|--------|
| **① 装 Node.js** | 从 <https://nodejs.org> 下载 LTS 版安装 |
| **② 装 Git** | Windows 用户必装，Mac 通常自带 |
| **③ 配镜像** | `npm config set registry https://registry.npmmirror.com` |
| **④ 安装 CLI** | `npm install -g @anthropic-ai/claude-code` |
| **⑤ 配 API** | 创建 `~/.claude/settings.json` 填入 DeepSeek 或阿里百炼信息 |
| **⑥ 启动** | 进入项目目录，运行 `claude` |

> **全程无需科学上网，所有链接国内可访问。**

---

> **参考资料：**
> - Claude Code 官方文档：<https://docs.anthropic.com/en/docs/claude-code>
> - GitHub 仓库：<https://github.com/anthropics/claude-code>
> - npm 淘宝镜像：<https://npmmirror.com>
> - DeepSeek：<https://platform.deepseek.com>
> - 阿里云百炼：<https://bailian.console.aliyun.com>
> - CC-Switch：<https://github.com/farion1231/cc-switch>
