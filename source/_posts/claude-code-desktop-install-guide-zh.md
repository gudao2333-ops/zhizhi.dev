---
title: Claude Code 桌面版国内安装指南（Windows + Mac）
date: 2026-06-06 18:24:05
updated: 2026-06-06 18:24:05
description: 一篇面向国内用户的 Claude Code 桌面版安装教程，覆盖 Windows 与 macOS 的下载、安装、API 配置和常见问题。
cover: /img/covers/zhizhi-default-cover.png
categories:
  - Claude Code
tags:
  - Claude Code
  - Windows
  - macOS
  - 安装指南
  - Anthropic
---

> **适用版本：** Claude Code Desktop App（2026 年最新版）  
> **适用人群：** 普通用户，想用桌面端图形界面操作  
> **前置条件：** 需要有一个 **Claude Pro / Max 账号**（可免费试用）

---

## 目录

1. [Claude Code 桌面版是什么](#1-claude-code-桌面版是什么)
2. [macOS 安装（3 分钟）](#2-macos-安装3-分钟)
3. [Windows 安装（3 分钟）](#3-windows-安装3-分钟)
4. [配置国内可用的 API（必做）](#4-配置国内可用的-api必做)
5. [开始使用](#5-开始使用)
6. [常见问题](#6-常见问题)

---

## 1. Claude Code 桌面版是什么

Claude Code 是 Anthropic 官方推出的 **AI 编程桌面应用**，它有完整的图形界面：

- 🖥️ 不是黑乎乎的终端，而是**可视化桌面应用**
- 🤖 能理解你的整个项目，帮你写代码、改 Bug、做重构
- 📝 支持**差异对比（Diff）**，改了什么一目了然
- 🔄 支持**并行会话**，同时处理多个任务
- 🎯 深度集成 Git，自动生成提交信息

### 跟 CLI 版本的区别

| | 桌面版 | CLI 版 |
|--|--------|--------|
| 操作方式 | 图形界面，鼠标操作 | 命令终端 |
| 适合人群 | **普通用户、编程初学者** | 开发者、工程师 |
| 安装难度 | ⭐ 简单 | ⭐⭐⭐ 中等 |
| 功能完整度 | 核心功能都有 | 全部功能 |

> 💡 **本文只讲桌面版，零命令行基础也能装。**

---

## 2. macOS 安装（3 分钟）

### 方法一：官网下载 DMG（推荐）

1. 打开浏览器访问 **<https://claude.ai/download>**
2. 页面底部找到 **"Download Desktop App"** 按钮
3. 选择 **macOS** 版本下载（自动识别 Apple Silicon 或 Intel）
4. 双击下载的 `Claude Code.dmg` 文件
5. 将图标拖入 **Applications（应用程序）** 文件夹
6. 首次打开时，如果提示"无法验证开发者"：
   - 打开 **系统设置 → 隐私与安全性**
   - 往下滑，点击 **"仍要打开"**
7. 完成！从 Launchpad 打开 Claude Code

> ⚠️ 如果 `claude.ai` 打不开，跳到方法二或方法三。

### 方法二：Homebrew 安装

适合电脑上已经有 Homebrew 的用户：
```bash
brew install --cask claude-code
```

### 方法三：国内网盘下载安装包

如果官网下载不了，从百度网盘下载离线安装包：

1. 下载地址：`https://pan.baidu.com/s/1FDVMR0n5bb5BuFUNMAojyQ`（提取码：`9d8a`）
2. 下载 `Claude Code.dmg` 文件
3. 双击安装，步骤同方法一

---

## 3. Windows 安装（3 分钟）

### 方法一：官网下载 EXE（推荐）

1. 打开浏览器访问 **<https://claude.ai/download>**
2. 页面底部找到 **"Download Desktop App"** 按钮
3. 选择 **Windows** 版本下载
4. 双击下载的安装包，按提示完成安装
5. 如果 Windows Smartscreen 弹出提示，点击 **"更多信息" → "仍要运行"**
6. 完成！从开始菜单启动 Claude Code

> ⚠️ 如果官网打不开，跳到方法二或方法三。

### 方法二：WinGet 命令安装

适合愿意用一行命令的用户：
```powershell
winget install Anthropic.ClaudeCode
```

### 方法三：国内网盘下载安装包

1. 下载地址：`https://pan.baidu.com/s/1FDVMR0n5bb5BuFUNMAojyQ`（提取码：`9d8a`）
2. 下载 `claude.msix` 文件
3. **双击**该文件 → 点击 **"安装"**
4. 如果双击报错，用 PowerShell 管理员模式运行：
   ```powershell
   Add-AppxPackage -Path "下载路径\claude.msix"
   ```

---

## 4. 配置国内可用的 API（必做）

> **为什么需要配置？** Claude Code 默认连接 Anthropic 海外服务器，国内网络无法直连。  
> **你需要提前准备：** 一个 **Anthropic API Key**（或通过第三方中转）。

### 使用 CC Desktop Switch 图形化配置（推荐，最简单）

**CC Desktop Switch** 是一个可视化配置工具，可以一键切换 API 端点。

**下载方式：**
- 上面百度网盘链接里已包含（文件名：`CC Desktop Switch.exe`）
- 或在网上搜索 "CC Desktop Switch" 下载

**配置步骤：**

1. 打开 **CC Desktop Switch**
2. 点击 **"添加供应商"**
3. 选择你的 API 来源：

   **方案 A：使用阿里云百炼（国内正规渠道）**
   | 字段 | 填写内容 |
   |------|---------|
   | 供应商名称 | 阿里百炼 |
   | API 地址 | `https://dashscope.aliyuncs.com/compatible-mode/v1` |
   | API Key | 你的阿里云百炼 Key |
   | 模型 | `qwen3-coder-plus`（或其他可用模型） |

   **方案 B：使用 DeepSeek**
   | 字段 | 填写内容 |
   |------|---------|
   | 供应商名称 | DeepSeek |
   | API 地址 | `https://api.deepseek.com` |
   | API Key | 你的 DeepSeek API Key |
   | 模型 | `deepseek-coder` |

   **方案 C：使用中转代理（如果你已有 Anthropic Key）**
   | 字段 | 填写内容 |
   |------|---------|
   | 供应商名称 | 自定义中转 |
   | API 地址 | 你的中转地址（如 `https://xxx.com/v1`） |
   | API Key | 你的中转 API Key |
   | 模型 | `claude-sonnet-4-6` |

4. 点击 **"启用"**
5. 打开 Claude Code，就可以正常使用了

---

## 5. 开始使用

安装并配置好 API 后：

1. **打开 Claude Code** — 你会看到一个干净的界面
2. **登录账号** — 用你的 Claude 账号登录（需要 Pro 或 Max 订阅）
3. **选择"Code"标签页** — 进入编程模式
4. **打开一个项目文件夹** — 点击"Open Folder"
5. **开始对话** — 例如：
   - "帮我写一个 Python 计算器"
   - "解释这段代码的作用"
   - "给这个页面加一个暗色模式"

### 初次使用提示

- 如果弹出终端设置向导，按回车接受默认值即可
- 首次使用会询问是否信任当前目录，选择 **Yes**
- 界面语言默认为英文，可在设置中调整

---

## 6. 常见问题

### Q1：`claude.ai/download` 打不开
**原因：** 该域名在国内受限。  
**解决：** 使用百度网盘下载安装包，或挂代理后访问。

### Q2：安装后打开闪退
**解决：**
- 检查系统版本（Windows 10+ / macOS 12+）
- 更新显卡驱动
- 以管理员身份运行（Windows）

### Q3：提示 "Your subscription is required"
**原因：** 需要 Claude Pro 或 Max 订阅。  
**解决：** 登录你的 Claude 账号，确保订阅有效；或用 API Key + 中转方式。

### Q4：API 连接失败 / 一直转圈
**解决：**
- 检查 CC Desktop Switch 中的 API 地址是否正确
- 确认 API Key 未过期
- 尝试更换其他 API 供应商

### Q5：打开后是英文，怎么切换中文？
目前 Claude Code 桌面版主要界面为英文，中文支持尚在完善中。不过它对中文命令的理解没有问题，直接用中文跟它对话即可。

### Q6：如何更新 Claude Code？
- **Mac：** 重新下载最新 DMG 安装覆盖，或通过 Homebrew 更新
- **Windows：** 重新下载安装包覆盖安装

---

## 总结：一句话版

| 你的系统 | 安装方法 | 需要命令行？ |
|----------|---------|:----------:|
| **Mac** | [下载 DMG](https://claude.ai/download) → 双击 → 拖入 Applications | ❌ 不需要 |
| **Mac（备用）** | `brew install --cask claude-code` | ⚠️ 一行命令 |
| **Mac（离线）** | 百度网盘下载安装包 → 同上安装 | ❌ 不需要 |
| **Windows** | [下载 EXE](https://claude.ai/download) → 双击安装 | ❌ 不需要 |
| **Windows（备用）** | `winget install Anthropic.ClaudeCode` | ⚠️ 一行命令 |
| **Windows（离线）** | 百度网盘下载 `.msix` → 双击安装 | ❌ 不需要 |
| **全部** | 用 **CC Desktop Switch** 配置国内 API | ⚠️ 图形化配置，点点点就行 |

---

> **参考资料：**
> - Claude Code 官方下载页：<https://claude.ai/download>
> - Claude Code 文档：<https://code.claude.com/docs/en/desktop-app>
> - 阿里云百炼：<https://bailian.console.aliyun.com>
> - DeepSeek：<https://platform.deepseek.com>
> - CC Desktop Switch：百度网盘链接内包含（提取码 `9d8a`）
> - 百度网盘安装包来源：<https://www.cnblogs.com/lijiext/p/20186706>
