# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 项目概述

BingoGame — 单词五子棋：抢格连线。课堂投屏用红蓝对战游戏，10×10 棋盘，五连获胜。

**硬约束（不可违反）**
- 必须保持单文件 `BingoGame.html`，不拆文件、不引入 npm/CDN/外部资源
- 必须离线可运行（双击打开即可）
- 必须适配低分辨率一体机投屏（1366×768 不溢出）
- 英文单词不能硬拆行（`word-break: normal`）
- 所有动效必须包含 `prefers-reduced-motion` 降级

## 运行方式

```bash
# 唯一运行方式 — 浏览器直接打开
open BingoGame.html
```

无构建步骤、无测试框架、无 lint。修改后刷新浏览器验证。

## 架构

整个应用在 `BingoGame.html` 内，分三层：

### 数据层
```
defaultWordBank    — 100 个内建英语词（不可变）
activeWordBank     — 运行时词库，可被 .txt 导入替换
boardWords[100]    — 棋盘当前显示的词
gridData[100]      — 格子归属：null | 'red' | 'blue'
```

### 状态机
```
gameState: idle → playing → won
currentMode: turn | buzz
currentTurn: red | blue
selectedCellIndex: -1 | 0..99
```

状态流转：
- `idle` — 点击"开始游戏" → `playing`
- `playing` — 五连检测触发 → `won`
- `won` — 点击"重置"/"再来一局" → `idle`
- 打乱棋盘/导入词库 → 回到 `idle`

### DOM 渲染
- `renderBoard(animate)` — 唯一棋盘渲染入口。`animate=true` 时执行 cellPop stagger 入场
- `refreshCellStyles()` — 批量重置格子 CSS class（用于 resetGame/startGame）
- `updateUI()` — 更新左侧状态栏、按钮、队伍卡片、分数、词数

### 动效系统（11 个 keyframes + confetti 粒子）
| 动效 | 触发点 |
|---|---|
| slideDown / slideRight / scaleUpBoard | CSS animation，页面加载自动触发 |
| cellPop stagger | `renderBoard(true)`，延迟 = `(x+y)*0.02s` |
| breathRed / breathBlue | `.team-card.active` CSS |
| mode-slider | `.mode-switch[data-mode]` translateX |
| rippleScale | `.cell.selected::after` |
| occupyPop | `occupyCell()` 加 class，500ms 后清理 |
| shake | `triggerShake()` 加 class，400ms 后清理 |
| boardExit | `generateBoard()` 加 `.exiting`，350ms 后重渲染 |
| winGlow | `triggerWin()` setTimeout 逐个加 `.win-light`，间隔 150ms |
| confetti | `spawnConfetti()` 60 粒子，requestAnimationFrame 物理循环 |

### 关键交互逻辑

**轮流模式**（`handleAnswer`）
- 答对 → `occupyCell` + `checkWin` + 换队
- 答错 → `triggerShake` + 换队
- 取消 → 只 `closeModal`，不换队

**抢答模式**（`handleBuzzAnswer`）
- 红队答对 → `occupyCell(red)` + `checkWin`
- 蓝队答对 → `occupyCell(blue)` + `checkWin`
- 无人答对 → `triggerShake`
- 取消 → 只 `closeModal`

**五连检测**（`checkWin`）— 4 方向遍历：→ ↓ ↘ ↗，连续 5 个同队即胜。

**词库导入**（`handleFileImport`）
- 读取 `.txt`，按行 split，trim 过滤空行
- 词数 >= 100：随机取 100
- 词数 < 100：重复填充至 100
- 空文件不破坏当前棋盘

## Git

- 仓库：https://github.com/Richard1eeK/BingoGame
- 分支：`main`
- 提交信息末尾加 `Co-Authored-By: Claude Opus 4.8 <noreply@anthropic.com>`
