---
title: Codex Computer Use 消失解决办法
date: 2026-06-05 18:49:56
updated: 2026-06-05 18:55:49
description: 记录 Windows 版 Codex Desktop 中 Browser、Chrome、Computer Use 插件突然消失时，一套更稳妥的排查与恢复办法。
cover: /img/zhizhi-ai-banner.svg
categories:
  - Codex
tags:
  - Codex
  - Windows
  - Browser
  - Chrome
  - Computer Use
  - 故障排查
---

这两天我碰到一个挺烦的问题。

Windows 版 Codex Desktop 里，`Browser`、`Chrome`、`Computer Use` 这几个插件突然不见了，设置页里也找不到，甚至还会冒出一句很吓人的报错：`Computer Use native pipe path is unavailable`。

如果你也刚好遇到的是这个问题，这篇就别当成技术分析看了，直接当成一份“能最快恢复使用”的处理记录就行。

## 你先确认一下，是不是同一个情况

如果你有下面这些现象，基本就是我这次遇到的这一类：

- `Browser`、`Chrome`、`Computer Use` 在设置页里消失了
- 前几天还正常，今天突然不能用了
- 出现 `Computer Use native pipe path is unavailable`
- 你明明已经升级过 Codex Desktop，但插件还是没有回来

如果你是 macOS，或者消失的不是这 3 个插件，那这篇可能帮不到你。

## 先说结论：别急着重装

我一开始也以为重装最快，但后来发现这类问题很多时候不在主程序本体，而在用户目录下那几份“旧缓存”和“旧配置”。

说白了就是：

- Codex Desktop 可能已经升级了
- 但本地插件缓存还停在旧版本
- 临时 marketplace 状态也没刷新干净
- 最后就变成插件没正常加载，相关 helper 也没起来

所以这时候你就会看到一种很奇怪的状态：`主程序像是新的，但插件像是旧的，最后谁也带不动谁`。

这也是为什么我不建议上来就重装。很多情况下，重装了主程序，问题还是会留在用户目录里。

## 我最后用的办法很简单

核心只有一句：

**不要直接删，先备份，再重命名。**

我建议只看这 3 个位置：

```text
%LOCALAPPDATA%\OpenAI\Codex\chrome-native-hosts.json
%USERPROFILE%\.codex\plugins\cache\openai-bundled
%USERPROFILE%\.codex\.tmp\bundled-marketplaces\openai-bundled
```

然后按这个顺序来：

1. 先把 Codex Desktop 完整退出
2. 再把 Chrome 也完整退出
3. 把上面这 3 个位置先备份，再重命名退避
4. 重启 Windows
5. 重启后重新打开 Codex Desktop，看看 `Browser`、`Chrome`、`Computer Use` 有没有回来

为什么我一直强调“重命名退避”而不是“直接删除”？

原因很朴素：

- 安全一点，判断错了也能回滚
- 对普通用户更友好
- 不容易误伤你别的本地状态

## 为什么这个办法比“重装试试”更靠谱

因为这类问题的关键通常不在安装目录，而在这些用户目录里的东西：

- `%LOCALAPPDATA%` 里的 native host 配置
- `%USERPROFILE%\.codex` 里的插件缓存
- `.tmp` 里的临时 marketplace 状态

只要这些地方还卡着旧状态，主程序就算是新的，也不一定能把插件重新拉起来。

而“备份 + 重命名 + 重启”这套动作，本质上是在逼 Codex 重新生成这些状态。对这类问题来说，它比盲目重装更对症。

## 如果你不想手动折腾，最省事的方法是把下面这段话丢给你自己的 Codex

这是我更推荐的用法。

你不用自己逐个目录处理，直接把下面这段 Prompt 发给你自己的 Codex，让它帮你检查和执行。

```Prompt
请帮我修复 Windows 版 Codex Desktop 中 Browser / Chrome / Computer Use 插件消失的问题。症状可能包括：
- 设置页里看不到 Browser / Chrome / Computer Use
- 提示 "Computer Use native pipe path is unavailable"

请按下面流程处理，并尽量直接执行，不要只给建议：

1. 先检查是否像“Codex 主程序已更新，但本地插件缓存 / native host 配置仍是旧状态”的问题。
2. 关闭 Codex 和 Chrome 相关进程。
3. 只处理下面这几个位置，不要扩展到无关文件：
   - %LOCALAPPDATA%\OpenAI\Codex\chrome-native-hosts.json
   - %USERPROFILE%\.codex\plugins\cache\openai-bundled
   - %USERPROFILE%\.codex\.tmp\bundled-marketplaces\openai-bundled
4. 对这些文件或目录执行“先备份，再重命名退避”，不要直接删除。备份名请自动加时间戳。
5. 如果某个目录或文件被占用，请明确告诉我是哪一个，并尽量先完成其他能做的步骤。
6. 修复后告诉我下一步应该做什么。若需要，请明确提示我“现在重启 Windows”，不要只说“重启一下试试”。
7. 重启后请继续帮我检查 Browser / Chrome / Computer Use 是否已恢复。
8. 全程保持改动最小化，不要重装 Codex，不要删除用户其他文件。

请先执行检查和修复，再用简短中文告诉我你做了什么、改了哪些路径、接下来我只需要做哪一步。
```

> 这段 Prompt 只适用于 Windows 上 Codex Desktop 的 `Browser` / `Chrome` / `Computer Use` 插件消失问题。如果你是 macOS，或者不是这 3 个插件有问题，就不要直接照搬。

## 如果你照着做了，还是没恢复

那就说明这次的问题可能不只是本地缓存没同步，可能还包括：

- 账号权限或功能灰度的问题
- 更高层的插件加载异常
- 某个文件或目录一直被占用，导致状态没法重建

但如果你只是想先把大多数“突然消失”的情况处理掉，那我还是建议先从这套最小动作开始。它够简单，也够安全，成功率也不低。

## 最后一句

如果你这次遇到的是和我一样的问题，我最建议的思路不是“重装碰碰运气”，而是：

**先把旧缓存和旧配置退开，让 Codex 自己重新长一套新的出来。**

---

参考：

- [原文记录](https://note.com/brainy_racoon759/n/n64bb7eb8cf46)
