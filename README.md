# YQ 铁匠铺 · 打工人语音面板 v2.4

一个像素风可交互 NPC 语音面板：点击人族农民 / 兽族苦工，他们会冒像素台词框 + 播放对应 War3 语音；工程师 YQ 不说话，只会定时冒泡。三个 NPC 都会在地面上自己瞎逛。

**v2.4 更新**：
- 加入天气系统（晴/多云/雨/夜），每 45s 自动轮转，点右上角标签也能手动切。换天气时 YQ 会顺嘴评论一句。
- YQ 台词池整体替换为「工程师 × AI 协作日常吐槽」21 条。

**v2.3**：右下角 🔊/🔇 静音切换，状态写 localStorage 自动记住。

## 本地预览

直接双击 `index.html` 即可在浏览器打开。

> 注意：部分浏览器对本地文件的音频加载有限制。如果点击 NPC 没声音，用一个本地 server 跑：
>
> ```bash
> cd npc_voice_panel
> python3 -m http.server 8000
> # 然后访问 http://localhost:8000
> ```

## 部署到 GitHub Pages

```bash
# 1. 在 GitHub 创建一个新的公开仓库，假设叫 yq-forge-npc
# 2. 把 npc_voice_panel/ 整个目录推上去
cd npc_voice_panel
git init
git add .
git commit -m "init: npc voice panel v2"
git branch -M main
git remote add origin git@github.com:<YOUR_GITHUB_USER>/yq-forge-npc.git
git push -u origin main

# 3. GitHub repo → Settings → Pages → Source 选 "main / root" → Save
# 4. 等 1 分钟，访问 https://<YOUR_GITHUB_USER>.github.io/yq-forge-npc/
```

## 文件结构

```
npc_voice_panel/
├── index.html              # 单文件入口（CSS + JS 全内联）
├── README.md
└── assets/
    ├── img/
    │   ├── bg.jpeg         # 像素风铁匠铺背景
    │   ├── peasant_*.png   # 人族农民 4 帧（idle/walk1/walk2/talk）
    │   ├── peon_*.png      # 兽族苦工 4 帧
    │   └── yq_*.png        # 工程师 YQ 4 帧
    └── audio/
        ├── peasant/        # 19 条人族农民语音
        └── peon/           # 17 条兽族苦工语音
```

## 角色 & 交互设计

| 角色 | 语音 | 行为 |
|---|---|---|
| ⚔ 人族农民 | War3 原声 19 条 | 点击说话 / 自主行走 / 30~50s 自言自语 |
| 🪓 兽族苦工 | War3 原声 17 条 | 同上，被画得更苦逼 |
| 💻 工程师 YQ | 无 | 每 12~20s 冒一句工程师日常吐槽 |

| 触发 | 行为 |
|---|---|
| 鼠标 hover NPC | NPC 上浮 + 放大反馈 |
| 点击 NPC | 冒台词框 + 随机语音 + 抖动动画 + 总计数 +1 |
| 第 1 次点击 | yes 类（好的老爷） |
| 2-3 次点击 | what 类（啥/咋了） |
| 4+ 次点击 | pissed 类（又要干活 / 忙啊忙）—— 越点越烦，这是核心解压点 |
| 8% 概率 | 触发 yesattack / warcry 彩蛋 |
| 全局"集结!"按钮 | 三个 NPC 同时喊 |

## v2 关键改进

- 角色 sprite 全部抠白底，导出透明 PNG，无白框
- 每个 NPC 4 帧（idle/walk1/walk2/talk），帧切换 + 自主行走 AI
- 行走严格限制在地面带（底部 35%），不会上天
- 音频单声道：新音频播放前会取消上一句，再也不叠加
- 加入第 3 个 NPC = 工程师 YQ
- 像素风游戏台词框（深棕厚边框 + 米黄底 + 像素台阶尖角）

## 后续升级 idea

- v3：鼠标移动光标变成"小工具"（锤子 / 法球 / iPad）
- v4：接 LLM，NPC 真·有性格的对话
- v5：sprite sheet 全动画，NPC 真的会挥锤子 / 砍树 / 敲键盘
