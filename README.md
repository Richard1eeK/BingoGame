# Word Bingo / 单词 Bingo

**English** | [中文](#中文说明)

Word Bingo is an interactive classroom vocabulary battle game designed for large-screen projection. 

Red and Blue teams compete to occupy cells by answering vocabulary questions correctly. The first team to connect the required number of cells (horizontally, vertically, or diagonally) wins!

## Features

- **Zero Dependencies**: Pure HTML/CSS/JS. Just double-click `BingoGame.html` to play entirely offline.
- **Optional Windows EXE**: Package the same HTML game as a desktop `.exe` with Electron.
- **Bilingual Interface**: Instantly switch between English and Chinese UI using the top-right toggle button.
- **Dynamic Board Sizes**: Choose from `5x5`, `6x6`, `7x7`, `8x8`, `9x9`, or `10x10`. Words automatically scale to fit the cells.
- **Custom Win Conditions**: Set the goal to Connect 3, Connect 4, or Connect 5.
- **Word Bank Import**: Easily import your custom vocabulary lists using a simple `.txt` file.
- **Star Multiplier**: Mark important words with a star (`*word`) to increase their appearance rate.
- **Word Bank Editing**: After importing, remove words you do not need from the Word Bank Settings before reshuffling.
- **Victory Effects**: Fireworks burst, confetti shower, and falling ribbons celebrate the winning team. All effects auto-cleanup after animation — no DOM residue.
- **Sound Effects (Default Off)**: Lightweight Web Audio API tones for cell click, correct answer, and victory fanfare. No external audio files required. Toggle on/off in the top bar. Sound never plays on page load — only after user interaction.
- **Projection Friendly**: Optimized layout and colors for classroom smartboards, complete with a Fullscreen mode and a "reduced-motion" fallback (which also disables fireworks & ribbons).

## How to Play

> **Tip:** You can also click the **How to Play** button in the top-right corner of the game for in-game instructions!

1. **Open the Game**: Double click `BingoGame.html` in your browser.
2. **Setup**: Select your desired Board Size and Win Condition on the left panel.
3. **Import Words (Optional)**: Click "Import Words" to load a custom `.txt` vocabulary list.
4. **Choose Mode**:
   - **Turn-based Mode**: Teams take turns answering. Correct answers win the cell, incorrect answers skip the turn.
   - **Buzz-in Mode**: The teacher clicks a cell, and whichever team answers first gets the cell.
5. **Start Game**: Click "Start Game". Connect the required number of cells to win!

## Windows EXE Build

The browser version remains the source of truth. The Electron wrapper only opens `BingoGame.html` in a desktop window.

```powershell
git clone https://github.com/Richard1eeK/BingoGame.git
cd BingoGame
npm install

# Test the desktop wrapper locally
npm run start

# Build a Windows x64 ZIP. Extract it, then run BingoGame.exe.
npm run dist:win

# Optional: build a Windows ARM64 ZIP
npm run dist:win:arm64

# Optional: build a single-file self-extracting EXE instead.
# This is slower on low-end classroom PCs and USB drives.
npm run dist:win:portable

# Optional: build a Windows installer instead
npm run dist:win:installer
```

The generated ZIP will be in `dist/`, for example `dist/BingoGame-2.4.0-win-x64.zip`.
Extract the ZIP first, then run `BingoGame.exe` from the extracted folder. Do not run it directly from the ZIP or a half-copied USB drive.

For the simplest Windows build, run these commands on Windows with Node.js installed.

## Custom Vocabulary & Starred Words

You can import any `.txt` file where each word is on a new line.

To highlight important words, prefix them with an asterisk `*` (e.g., `*apple` or `* banana`).
- Starred words appear with a ⭐ badge in the Word Bank Settings.
- You can adjust the **Star Multiplier** (2x or 3x) in the settings, making starred words more likely to appear on the board.
- You can also delete words from the settings list, then click **Apply & Shuffle** to rebuild the board with the remaining words.

---

<h2 id="中文说明">中文说明</h2>

单词 Bingo 是一款专为课堂投屏设计的互动词汇对战游戏。

红蓝两队通过正确回答单词问题来占领格子，率先连成指定数量（横、竖、斜均可）的队伍获胜！

## 核心特性

- **纯单机离线**：无需任何外部依赖，双击 `BingoGame.html` 即可运行。
- **可选 Windows EXE**：用 Electron 把同一个 HTML 游戏打包成桌面 `.exe`。
- **中英双语界面**：点击右上角按钮即可无缝切换中文/English 界面。
- **自定义棋盘**：支持 `5x5` 到 `10x10` 六种尺寸。长单词会自动缩放字号以适应格子。
- **自定义获胜条件**：支持选择“连 3”、“连 4”或“连 5”获胜。
- **词库导入**：支持直接导入 `.txt` 文本文件作为词库。
- **星标高频词**：通过加星号（`*word`）标记重点词汇，可设置倍数提高出现概率。
- **词库筛选**：导入后可在“词库设置”中删除本轮暂时不需要的单词。
- **胜利动效**：烟花爆发、五彩纸屑、彩带飘落 — 三重胜利庆祝。所有动效自动清理 DOM，不留残留节点。
- **音效开关（默认关闭）**：基于 Web Audio API 的轻量音效 — 点击格子、占格成功、胜利提示音。无需外部音频文件。顶部开关控制，默认关闭避免课堂突然出声。仅在用户交互后播放，不在页面加载时播放。
- **大屏适配**：专为课堂触控一体机优化，支持一键全屏，自带精美动效及防晕眩降级（reduced-motion 下跳过烟花和彩带，仅保留轻量状态变化）。

## 玩法说明

> **提示：** 游戏中也内置了详细指南，点击右上角的 **玩法说明** 按钮即可随时查看。

1. **运行游戏**：在浏览器中双击打开 `BingoGame.html`。
2. **游戏设置**：在左侧面板选择合适的“棋盘尺寸”与“获胜条件”。
3. **导入词库（可选）**：点击“导入词库”上传您的 `.txt` 单词表。
4. **选择模式**：
   - **轮流模式**：两队轮流答题。答对占领该格，答错则跳过当前回合。
   - **抢答模式**：老师点击格子，最先答对的队伍占领该格。
5. **开始对战**：点击“开始游戏”，率先连成指定格数的一方获胜！

## Windows EXE 打包

浏览器版仍然是主版本。Electron 只负责用桌面窗口打开 `BingoGame.html`，不会拆分或重写游戏文件。

```powershell
git clone https://github.com/Richard1eeK/BingoGame.git
cd BingoGame
npm install

# 本地测试桌面壳
npm run start

# 打包 Windows x64 ZIP。解压后运行里面的 BingoGame.exe
npm run dist:win

# 可选：打包 Windows ARM64 ZIP
npm run dist:win:arm64

# 可选：打包单文件自解压 EXE。
# 低性能一体机和 U 盘场景不推荐，启动更慢。
npm run dist:win:portable

# 可选：改为打包 Windows 安装程序
npm run dist:win:installer
```

生成的 ZIP 会在 `dist/` 里，例如 `dist/BingoGame-2.4.0-win-x64.zip`。
先解压 ZIP，再运行解压目录里的 `BingoGame.exe`。不要直接从压缩包里运行，也不要从未复制完整的 U 盘文件运行。

最简单的方式是在 Windows 上安装 Node.js 后直接运行以上命令。

## TXT 词库与星标词格式

导入的 `.txt` 文件只需每行写一个单词即可。

如果你希望某些重点词汇更容易出现在棋盘上，请在单词前加星号 `*`（例如：`*apple` 或 `* banana`）。
- 导入后，点击“⭐ 词库设置”即可查看所有词汇，星标词会带有 ⭐ 标记。
- 你可以在设置中调整 **星标倍数**（2x 或 3x），让这些重点词汇在生成棋盘时的出现概率翻倍。
- 如果本轮只想练其中一部分词，也可以在设置列表里删除不需要的词，再点击“应用并重排棋盘”。
