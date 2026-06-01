# YQ 铁匠铺 · 打工人语音面板 v1

## 这是啥

一个嵌入到飞书文档的**像素风可交互 NPC 语音面板**:点击人族农民 / 兽族苦工,他们会冒对话气泡 + 播放对应 War3 语音。

## 部署到 GitHub Pages (3 分钟)

```bash
# 1. 在 GitHub 创建一个新的公开仓库,假设叫 yq-forge-npc
# 2. 把 npc_voice_panel/ 整个目录推上去
cd npc_voice_panel
git init
git add .
git commit -m "init: npc voice panel v1"
git branch -M main
git remote add origin git@github.com:<YOUR_GITHUB_USER>/yq-forge-npc.git
git push -u origin main

# 3. 在 GitHub repo 设置 → Pages → Source 选 "main / root" → Save
# 4. 等 1 分钟,访问 https://<YOUR_GITHUB_USER>.github.io/yq-forge-npc/
```

## 嵌入到飞书文档

页面跑起来后,把 URL 发给我,我用 lark-cli 在铁匠铺顶部 callout 下面插一个 `<iframe>` 块,推荐尺寸:

- 宽: 100%
- 高: 480px

## 文件结构

```
npc_voice_panel/
├── index.html          # 单文件入口(包含全部 CSS + JS)
├── README.md           # 本文件
└── assets/
    ├── img/
    │   ├── bg.jpeg     # 像素风铁匠铺背景
    │   ├── peasant.jpeg # 人族农民 sprite
    │   └── peon.jpeg   # 兽族苦工 sprite
    └── audio/
        ├── peasant/    # 19 条人族农民语音
        └── peon/       # 17 条兽族苦工语音
```

## 交互设计

| 触发 | 行为 |
|---|---|
| 鼠标 hover NPC | NPC 上浮 + 放大反馈 |
| 点击 NPC | 冒气泡 + 随机语音 + 抖动动画 + 总计数 +1 |
| 第 1 次点击 | yes 类(好的老爷) |
| 2-3 次点击 | what 类(啥/咋了) |
| 4+ 次点击 | pissed 类(又要干活/忙啊忙)—— 越点越烦,这是核心解压点 |
| 8% 概率 | 触发 yesattack / warcry 彩蛋 |
| 全局"集结!"按钮 | 两个 NPC 同时喊 |
| 入场 1 秒 | 农民自动喊"准备干活" |
| 每 45 秒 | 随机 NPC 自言自语(氛围) |

## 后续升级 idea (v2 起再做)

- **v2:** 加铁匠师傅 / 大法师两个 NPC,每个角色独立技能
- **v3:** 鼠标移动光标变成"小工具"(锤子/法球)
- **v4:** 接 LLM,NPC 真·有性格的对话(豆包 / Doubao API)
- **v5:** 像素动画 sprite sheet,NPC 真的会走来走去
