# Deep Learn Output Template

Use this template when writing a full learning note or substantially enriching an existing note.
Keep sections that fit the task; remove sections that would be empty.

```markdown
# <任务标题>

## 任务概览

- 目标:
- 当前状态:
- 涉及系统:
- 关键文件:
- 关键命令:
- 关键日志/现象:
- 结论一句话:

## 已确认事实与推断

### 已确认事实

- <来自代码、命令、日志、实测的事实>

### 推断/嫌疑

- <基于现象和代码链路做出的判断，标明还需要如何验证>

## 端到端链路

```text
<输入/传感器>
  -> <数据发布/中间话题/进程>
  -> <算法/控制逻辑>
  -> <命令话题/驱动>
  -> <硬件执行>
  -> <反馈/日志>
```

逐段说明:

1. `<环节名>`:
   - 输入:
   - 输出:
   - 关键代码/参数:
   - 失败模式:

## 标准工作流

### Step 1: <步骤名>

- 做了什么:
- 为什么需要:
- 不做会怎样:
- 如何验证:

### Step 2: <步骤名>

- 做了什么:
- 为什么需要:
- 不做会怎样:
- 如何验证:

## 关键代码与参数

| 项目 | 位置 | 作用 | 现值/建议值 | 风险 |
|---|---|---|---|---|
| `<变量或参数>` | `<文件:行/命令>` | `<作用>` | `<值>` | `<调错会怎样>` |

## 知识地图

```text
任务层
  -> 工程链路
  -> 核心算法/控制
  -> 数学/物理基础
  -> 可观测现象与调参方法
```

## 知识分解

### 1. <一级概念> (<English Term>)

#### Why

<它解决什么问题，为什么这个任务需要它。>

#### What

<直观定义 + 精确定义。>

#### How

<它在当前任务里如何出现，引用真实代码、命令、日志或参数。>

#### 前置知识

##### 1.1 <前置概念>

- Why:
- What:
- How:

##### 1.2 <前置概念>

- Why:
- What:
- How:

### 2. <另一个一级概念>

...

## 调试决策树

```text
现象 A
  -> 先看日志/话题/参数 X
  -> 如果 X 正常，看 Y
  -> 如果 X 异常，修改 Z 后重新测试
```

## 实验与验证

### 无硬件/低风险验证

- 命令:
- 预期:
- 异常说明:

### 实机小步验证

- 启动参数:
- 操作顺序:
- 观察指标:
- 停止条件:

## 常见误区

- 误区:
  - 为什么容易错:
  - 正确理解:

## 思考与问答

1. 【基础】<定义/链路复述问题>
2. 【基础】<参数作用问题>
3. 【进阶】<为什么/因果问题>
4. 【进阶】<根据日志定位问题>
5. 【综合】<迁移到新场景的问题>

## 小练习

- 练习 1:
- 练习 2:

## 术语表

| 中文 | English | 一句话解释 |
|---|---|---|
|  |  |  |
```

## Writing Notes

- Prefer fewer concepts with deeper explanations over many shallow definitions.
- If the note is based on a bug, keep the original symptom visible throughout the explanation.
- If a formula appears, define every symbol immediately below it.
- If a code path appears, include enough surrounding context to show where data enters and leaves.
- For robotics tasks, always distinguish coordinate frame, units, rate, and safety limits.
