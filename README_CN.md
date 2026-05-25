# Codex Skills: Deep Learn

这个仓库用于保存个人 Codex/Claude skill。目前包含一个技能：

- `deep-learn`: 把一次真实的技术工作、调试过程、概念学习或工程复盘，整理成分层的中文学习笔记，并生成互动问答。

## 适用场景

`deep-learn` 适合在这些情况下使用：

- 你刚完成一次技术任务，想把过程整理成可复用的学习文档。
- 你调试了一个问题，想知道背后的数学、控制、系统和工程原理。
- 你遇到一个新术语，想从直觉、定义、公式、代码和基础知识逐层讲透。
- 你希望把项目里的经验沉淀到 `docs/deep-learn/` 下面。
- 你在做机器人、ROS、VR 遥操作、IK、CAN、ADB、嵌入式、控制系统或机器学习训练相关工作。

## 目录结构

```text
codex-skills/
├── README_CN.md
└── deep-learn/
    ├── SKILL.md
    ├── agents/
    │   └── openai.yaml
    └── references/
        ├── output-template.md
        ├── qa-rubric.md
        └── robotics-examples.md
```

各文件作用：

- `deep-learn/SKILL.md`: skill 的主入口，定义触发条件、工作模式、流程和输出要求。
- `deep-learn/agents/openai.yaml`: Codex UI 元数据，包括显示名称、简短描述和默认 prompt。
- `deep-learn/references/output-template.md`: 生成完整学习笔记时使用的 Markdown 模板。
- `deep-learn/references/qa-rubric.md`: 互动问答时使用的评分和追问规则。
- `deep-learn/references/robotics-examples.md`: 针对 ROS、VR 遥操作、IK、Piper、CAN、ADB、坐标系和关节方向调试的案例参考。

## 安装到 Codex

把 `deep-learn` 目录复制到 Codex skills 目录：

```bash
mkdir -p ~/.codex/skills
cp -a deep-learn ~/.codex/skills/
```

如果你是在当前仓库根目录执行：

```bash
mkdir -p ~/.codex/skills
cp -a codex-skills/deep-learn ~/.codex/skills/
```

## 安装到 Claude

如果你也想在 Claude 的本地 skill 目录中使用：

```bash
mkdir -p ~/.claude/skills
cp -a codex-skills/deep-learn ~/.claude/skills/
```

## 使用示例

可以直接这样对 Codex 说：

```text
用 deep-learn 帮我复盘一下刚才的 QuestVR 遥操作调试。
```

```text
把我刚才 joint5 方向调参的过程整理成一篇深度学习笔记。
```

```text
这段 world_delta_xyz = current - previous 是什么意思？从基础讲透。
```

```text
帮我把 docs/deep-learn/xxx.md 再充实一点，加入调试决策树和问答。
```

## 推荐输出位置

`deep-learn` 默认把项目学习笔记写到当前项目的：

```text
docs/deep-learn/<YYYY-MM-DD>-<short-task-slug>.md
```

例如：

```text
docs/deep-learn/2026-05-25-joint5-orientation-axis-sign.md
```

这样可以把工程调试经验和项目代码放在一起，后续回看、交接或上传 GitHub 都更方便。

## 设计原则

这个 skill 的重点不是泛泛解释概念，而是把概念和真实工程链路绑定起来：

- 先还原实际做了什么。
- 再追踪输入、处理、输出和硬件执行链路。
- 然后拆解相关的数学、物理、计算机、算法和控制原理。
- 最后用问答检查是否真的理解。

对于机器人项目，文档会特别关注：

- 坐标系和单位。
- ROS topic、节点、参数和频率。
- IK、关节命令和驱动链路。
- deadman、限速、限位、跳变拒绝等安全机制。
- 无硬件验证和实机小步验证。

## 校验

如果本机有 Codex 的 `skill-creator` 系统 skill，可以用下面的命令做基础校验：

```bash
python3 ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py codex-skills/deep-learn
```

预期输出：

```text
Skill is valid!
```

## 维护建议

- 更新 `SKILL.md` 时，保持主流程简洁，不要塞入过长案例。
- 长模板、案例和评分细则放到 `references/`。
- 新增机器人项目经验时，优先补充 `references/robotics-examples.md`。
- 如果只是某个项目的一次学习记录，应写到项目自己的 `docs/deep-learn/`，不要写进 skill 本体。
- 上传 GitHub 前，确认没有包含本地密码、私有 IP、token 或真实硬件危险操作说明。
