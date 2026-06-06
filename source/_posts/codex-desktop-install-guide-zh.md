---
title: Codex 桌面版国内安装指南（Windows + Mac）
date: 2026-06-06 18:15:43
updated: 2026-06-06 18:15:43
description: 面向国内用户的 Codex 桌面版安装教程，覆盖 Windows 与 macOS 的下载、安装、API 配置和常见问题。
cover: /img/covers/zhizhi-default-cover.png
categories:
  - Codex
tags:
  - Codex
  - Windows
  - macOS
  - 安装指南
  - OpenAI
---

> **适用平台：** Windows 10/11、macOS 12+（Apple Silicon / Intel）  
> **适用人群：** 普通用户，零命令行基础也能装  
> **发布时间：** 2026 年 6 月（针对 Codex 桌面版 v26.5+）

---

## 目录

1. [Codex 桌面版是什么](#1-codex-桌面版是什么)
2. [macOS 安装（3 分钟）](#2-macos-安装3-分钟)
3. [Windows 安装（3 分钟）](#3-windows-安装3-分钟)
4. [配置 API（国内必做）](#4-配置-api国内必做)
5. [开始使用](#5-开始使用)
6. [常见问题](#6-常见问题)

---

## 1. Codex 桌面版是什么

Codex 是 OpenAI 推出的 **AI 编程助手桌面应用**，它：

- 🖥️ 有完整的图形界面，不是黑乎乎的终端
- 🤖 能读懂你的整个项目，帮你写代码、改代码、回答问题
- 🔧 支持 VS Code、JetBrains 等编辑器集成
- 📦 开箱即用，装好就能跟 AI 对话编程

**前提条件：** 需要有一个 **ChatGPT Plus / Pro 账号**（付费订阅）或 **OpenAI API Key**。

---

## 2. macOS 安装（3 分钟）

### 方法一：直接下载 DMG 安装包（推荐）

**Apple Silicon（M1/M2/M3/M4 芯片）：**

1. 点击下载：**[Codex.dmg（Apple Silicon 版）](https://persistent.oaistatic.com/codex-app-prod/Codex.dmg)**
2. 双击下载的 `Codex.dmg` 文件
3. 将 Codex 图标拖入 **Applications（应用程序）** 文件夹
4. 首次打开时，如果提示"无法验证开发者"，去 **系统设置 → 隐私与安全性**，点击"仍要打开"
5. 大功告成！从 Launchpad 或应用程序文件夹打开 Codex

**Intel Mac 用户：**
- 下载：**[Codex-latest-x64.dmg](https://persistent.oaistatic.com/codex-app-prod/Codex-latest-x64.dmg)**
- 后续步骤同上

### 方法二：App Store 安装

如果方法一下载慢（`oaistatic.com` 域名可能受限），试试从 **App Store** 安装：

1. 打开 **App Store**
2. 搜索 **"Codex"**
3. 点击 **"获取"** 安装

### 方法三：镜像站下载（国内加速）

如果官方链接下载不动，使用国内镜像：

| 版本 | 镜像链接 |
|------|---------|
| Apple Silicon | `https://codexapp.agentsmirror.com/latest/mac-arm64` |
| Intel | `https://codexapp.agentsmirror.com/latest/mac-intel` |

> 镜像站定时从官方同步，文件未经任何修改，安全可靠。

---

## 3. Windows 安装（3 分钟）

### 方法一：微软商店安装（首选）

1. 打开 **Microsoft Store**（开始菜单搜"Microsoft Store"）
2. 搜索 **"Codex"**（或直接打开[商店链接](https://apps.microsoft.com/detail/9plm9xgg6vks)）
3. 点击 **"安装"**
4. 安装完成后，从开始菜单启动 Codex

> ⚠️ 如果微软商店打不开或下载慢，跳到方法二。

### 方法二：国内镜像下载安装包（推荐给国内用户）

如果微软商店无法访问，从国内镜像直接下载 `.msix` 安装包：

1. 下载地址：**[Codex Windows 安装包](https://codexapp.agentsmirror.com/latest/win)**
2. 下载得到 `Codex-Windows-x64.msix` 文件
3. **双击**该文件 → 点击"安装"即可

**如果双击报错，用这个方法：**
1. 右键点击 `.msix` 文件 → **重命名**，把后缀 `.msix` 改成 `.zip`
2. 解压这个 zip 文件
3. 进入解压后的文件夹，直接双击运行 **`Codex.exe`**

### 方法三：winget 命令安装

适合愿意用一行命令的用户（**仅此一行**）：

```powershell
# 打开 Windows Terminal 或 PowerShell，粘贴回车
winget install --id 9PLM9XGG6VKS --source msstore
```

> 如果提示需要登录微软账号，按提示登录即可。

---

## 4. 配置 API（国内必做）

> **为什么需要配置？** Codex 默认连接 OpenAI 的服务器，国内网络无法直连。  
> **你需要提前准备：** 一个 **OpenAI API Key** 或第三方兼容 API Key。

### 4.1 找到配置文件

**macOS：**
- 打开 **终端**（应用程序 → 实用工具 → 终端）
- 粘贴以下命令并回车：
  ```bash
  open ~/.codex
  ```
- 如果提示"文件不存在"，先运行 `mkdir -p ~/.codex && open ~/.codex`

**Windows：**
- 打开 **文件资源管理器**
- 在地址栏输入 `%USERPROFILE%\.codex` 并回车
- 如果文件夹不存在，手动新建一个名为 `.codex` 的文件夹

### 4.2 创建配置文件

在 `.codex` 文件夹里新建一个文件，命名为 **`config.toml`**（注意扩展名是 `.toml`，不是 `.txt`）。

用记事本打开，粘贴以下内容之一：

**方案 A：使用 OpenAI 中转代理（推荐）**

```toml
openai_base_url = "https://你的代理地址/v1"
model = "gpt-4o"
sandbox_mode = "workspace-write"
web_search = "disabled"
```

**方案 B：使用 DeepSeek（国产模型）**

如果没有 OpenAI Key，可以用 DeepSeek 替代：

```toml
openai_base_url = "https://api.deepseek.com/v1"
model = "deepseek-coder"
sandbox_mode = "workspace-write"
web_search = "disabled"
```

### 4.3 设置 API Key

**macOS：**
- 打开 **终端**，粘贴以下命令（把 `sk-xxx` 换成你的真实 Key）：
  ```bash
  echo 'export OPENAI_API_KEY="sk-你的Key"' >> ~/.zshrc
  source ~/.zshrc
  ```
- 或者关掉终端重新打开 Codex，它会提示你输入 Key

**Windows：**
- 按 `Win + R`，输入 `sysdm.cpl`
- 点 **"高级"** → **"环境变量"**
- 在"用户变量"下点 **"新建"**
- 变量名：`OPENAI_API_KEY`
- 变量值：你的 API Key
- 确定后**重启 Codex**

> 💡 **没有 API Key？**  
> 注册 DeepSeek 等国产平台（api.deepseek.com），它们提供兼容 OpenAI 接口的 API，有免费额度。

---

## 5. 开始使用

安装并配置好 API 后：

1. **打开 Codex** — 会看到一个聊天界面
2. **选择一个项目文件夹** — Codex 会读取你的代码
3. **开始对话** — 例如："帮我解释这段代码"或"给我写一个计算器"
4. **进阶功能** — Codex 可以直接修改文件、运行命令、创建 Git 提交

### 首次使用提示

- 如果提示登录，选择 **"Use API Key"**（使用 API Key），粘贴你的 Key
- 默认界面是英文的，介意的可以在设置里改成中文，后面会说怎么弄
- 建议先用一个简单项目测试，熟悉后再处理正式项目

### 刚打开全是英文怎么办

这应该是大家问得最多的一个问题了。Codex 装好后默认是英文界面，设置里也确实有语言选项，但很多人发现选了中文没反应，或者干脆没有中文这个选项。

**原因是这样的：** Codex 的语言包不是自带的，需要从 OpenAI 的服务器上下载。国内网络连那个地址不太稳定，语言包下载不下来，所以就卡住了。

**解决办法分两种情况：**

**情况一：设置里有中文选项，但选了没变化**
进 **File → Settings → General**，找到 **Language for the app UI**，选 **Chinese (China)**。然后**完全退出 Codex 再重新打开**，不要只是关窗口，右键托盘图标退出那种。如果还是不生效，大概率是语言包没下载完，切到情况二处理。

**[需插入图片：Settings → General → Language 下拉菜单位置截图]**

**情况二：设置里根本没有中文选项**
这说明语言包压根没下载下来。最简单的方法是**临时开一次代理**（开全局或 TUN 模式都行），然后重复上面的操作选中文。语言包只要下载一次就会存到本地，之后关掉代理，界面也还是中文的，不用每次都开。

**情况三：不想折腾代理**
那也可以不换界面语言，直接让 Codex 用中文回你就行了。在项目目录下建一个 `AGENTS.md` 文件，里面写一行：

```bash
echo 'Always respond in Chinese-simplified' > .codex/AGENTS.md
```

这样 AI 回你的时候会自动用中文，界面虽然还是英文，但不影响用。大部分人选这个方案，省事。

> 另外说一句，如果你开代理改了中文，之后关掉代理发现界面又变回英文了，说明语言包在会话期间被清了，重新下载一次就行。不过这种情况我身边没人遇到过，基本都是一次搞定。

---

## 6. 常见问题

### Q1：`oaistatic.com` 下载链接打不开
**解决：** 使用镜像站下载（见上文方法三），或挂代理后重试。

### Q2：微软商店无法访问
**解决：** 使用国内镜像下载 `.msix` 安装包（见 Windows 安装方法二）。

### Q3：`.msix` 双击安装报错
**解决：** 改成 `.zip` 解压后运行 `Codex.exe`，这是微软商店应用的备用安装方式。

### Q4：打开 Codex 一直转圈/连接失败
**解决：** 检查 API 配置是否正确，即 `config.toml` 中的 `openai_base_url` 是否可访问。

### Q5：提示 "Your subscription is required"
**原因：** 如果没有配置 API Key 而使用账号登录，需要 ChatGPT Plus/Pro 订阅。
**解决：** 使用 API Key 方式（或确保 Plus 订阅有效）。

### Q6：Codex 打开后白屏/闪退
**解决：**
- 检查系统版本是否满足最低要求（Win 10 19041+ / macOS 12+）
- 更新显卡驱动
- 重新安装

### Q7：换了中文之后，界面有些地方还是英文
正常。Codex 的中文翻译不是全覆盖的，菜单栏、某些弹窗还是英文居多。这不影响用，习惯就好。真正受不了的建议用上面说的 AGENTS.md 方案。

### Q8：如何更新 Codex？
- **Mac：** 重新下载最新 DMG 安装覆盖，或通过 App Store 更新
- **Windows：** 通过微软商店更新，或重新下载镜像站最新版安装包

---

## 总结：一句话版

| 你的系统 | 安装方法 |
|----------|---------|
| **Mac（M 芯片）** | [下载 Codex.dmg](https://persistent.oaistatic.com/codex-app-prod/Codex.dmg) → 双击 → 拖入 Applications |
| **Mac（Intel）** | [下载 Codex-x64.dmg](https://persistent.oaistatic.com/codex-app-prod/Codex-latest-x64.dmg) → 同上 |
| **Windows** | [微软商店](https://apps.microsoft.com/detail/9plm9xgg6vks) 或 [国内镜像](https://codexapp.agentsmirror.com/latest/win) |
| **全部用户** | 创建 `config.toml` 配置 API 端点 + 设置 `OPENAI_API_KEY` 环境变量 |

---

> **免责声明：** 本文仅提供技术教程，国内使用请确保遵守相关法律法规。镜像站 `codexapp.agentsmirror.com` 为第三方维护，仅做安装包镜像，不涉及任何破解或修改。
