# ⚖️ 要件审判九步法 AI 技能 v4.0

基于邹碧华《要件审判九步法》的 AI 裁判辅助工具。提供案件卷宗材料，AI 按九步法流程生成裁判文书草稿。

**适用于**：法官/法官助理起草裁判文书、律师预判案件走向、法学教学案例分析。

## 怎么用？

### 微信 ClawBot / OpenClaw（最简单）

**方式一：微信里发一句话，让 Bot 帮你装（推荐）**

在微信里直接发这段话给你的 Bot：

> 帮我安装一个技能：从 https://github.com/happylawyer/jiubufa-skill 把 openclaw 文件夹里的 SKILL.md 下载到 ~/.openclaw/workspace/skills/jiubufa/SKILL.md

Bot 会自动执行，装完后发 `/jiubufa` 即可使用。

**方式二：自己在电脑终端里装**

```bash
git clone https://github.com/happylawyer/jiubufa-skill.git /tmp/jiubufa-skill && mkdir -p ~/.openclaw/workspace/skills/jiubufa && cp /tmp/jiubufa-skill/openclaw/SKILL.md ~/.openclaw/workspace/skills/jiubufa/SKILL.md
```

装好后，在微信里对你的 Bot 发 `/jiubufa` 或说「**九步法**」，它就会启动。

> 没有 OpenClaw？先装：`npm install -g openclaw`，然后 `openclaw init` 初始化。

### Claude Code

```bash
# 在电脑终端里执行这两行
mkdir -p ~/.claude/skills/jiubufa
cp claude-code/SKILL.md ~/.claude/skills/jiubufa/SKILL.md
```

装好后输入 `/jiubufa` 启动。

### Claude Web / Kimi / DeepSeek / 通义千问等

不用装任何东西。打开 `prompt/system-prompt.md` 这个文件，**全选复制**，粘贴到对应平台的「系统提示词」或「自定义指令」里，保存即可。

### Codex CLI

```bash
codex --system-prompt "$(cat prompt/system-prompt.md)" "请分析以下案件材料..."
```

## 它能做什么？

你提供起诉状（+答辩状、证据、庭审笔录），它会：

```
1. 固定权利请求（原告要什么？）
2. 确定请求权基础（法律依据是什么？）
3. 确定抗辩权基础（被告怎么反驳？）
4. 拆解构成要件（法条拆成几个条件？）
5. 检索诉讼主张（双方说全了没有？）
6. 整理争点（到底争的是什么？）
7. 分配举证责任（谁来举证？）
8. 认定事实（证据够不够？）
9. 要件归入 → 生成裁判文书草稿
```

**两种模式**：
- **模式 1**：全自动，一次出稿
- **模式 2**：一步一停，你确认后再走下一步

## 它有什么安全机制？

| 机制 | 说明 |
|------|------|
| 六条铁律 | 禁止编造事实、禁止和稀泥、禁止跳步、禁止用旧法、禁止编造法学理论、必须回应抗辩 |
| 法条风控 | 自动校验法条是否现行有效、条文是否对得上、引用的理论是不是真实存在 |
| 材料缺失预处理 | 缺什么材料会告诉你，不会假装看过 |
| "八个一致"校验 | 出稿前自查：诉请和判决对不对得上、事实和证据对不对得上…… |

## 文件说明

```
jiubufa-skill/
├── README.md                    # 你正在看的这个文件
├── openclaw/SKILL.md            # OpenClaw / 微信 ClawBot 版
├── claude-code/SKILL.md         # Claude Code 版（支持 /jiubufa 命令）
├── prompt/system-prompt.md      # 通用版（复制粘贴到任何 AI 平台）
└── examples/                    # 示例案件的完整输出
```

## 注意事项

- 这是**辅助草稿**，不能替代法官的独立裁判，所有输出必须经过人工审核。
- AI 可能存在法条记忆偏差，虽然内置了风控机制，仍建议核对法条原文。
- 仅适用于中国大陆民商事案件。

## 版本历史

| 版本 | 变更 |
|------|------|
| v1.0 | 基础九步法 + 双模式 + 八个一致校验 |
| v2.0 | 新增法条风控 |
| v3.0 | 新增执行原则、每步输出要求、文书结构要求 |
| **v4.0** | **新增：禁止编造法学理论、材料缺失预处理、诉请依赖关系、被告缺席处理** |

## 致谢

方法论基础来自邹碧华法官（1967—2014）所著《要件审判九步法》。邹碧华法官是中国司法改革的先驱者，他提出的要件审判九步法为中国民商事审判提供了科学、规范的裁判方法论。

## 许可证

MIT License — 随便用，注明出处就行。
