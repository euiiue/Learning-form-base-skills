---
name: deep-learn
description: >
  Use this skill when the user wants to turn completed technical work, debugging,
  unfamiliar terminology, or hands-on engineering experience into a layered learning
  note and interactive Q&A session. Especially useful for robotics, ROS, VR
  teleoperation, control systems, computer vision, embedded systems, ML training,
  CAN/ADB/Linux tooling, and when the user says things like "讲透", "拆解",
  "复盘", "总结我刚做的事", "帮我理解原理", "从基础讲起", "deep learn",
  or "teach me how this works".
metadata:
  short-description: Layered technical learning notes and Q&A
---

# Deep Learn

Turn a real technical task into a reusable learning artifact. The output should connect the
user's actual files, commands, logs, and decisions to the underlying principles, then verify
understanding through adaptive Q&A.

## When To Use

Use this skill when the user:

- Finished or debugged a task and wants a technical复盘.
- Asks what a command, code path, algorithm, parameter, log, or concept means.
- Wants a concept explained from first principles.
- Wants a Markdown learning note saved into the project.
- Wants to make an existing learning note richer, clearer, or more systematic.

Do not use this skill for a small direct answer unless the user asks for depth. For simple
questions, answer directly first, then offer to expand into a Deep Learn note if useful.

## Operating Modes

Choose the smallest mode that satisfies the request:

- **Quick explain**: Answer in chat only. Use when the user asks one narrow question.
- **Full note**: Create or update a Markdown file under `docs/deep-learn/`. Use when the user
  asks for整理, 复盘, 讲透, or a durable record.
- **Interactive Q&A**: Ask diagnostic questions one by one, assess answers, and repair gaps.
- **Enrich existing note**: Preserve the user's existing structure and add missing workflow,
  evidence, concepts, experiments, or Q&A.

If the requested mode is unclear but the user references a file, default to **Enrich existing
note**. If the task history is clear and no file exists, default to **Full note**.

## Core Workflow

1. **Capture context**
   - Identify the task, target system, touched files, commands, logs, and outcome.
   - Prefer concrete evidence from the workspace over memory.
   - Ask a concise question only when a missing fact would materially change the explanation.

2. **Reconstruct the workflow**
   - Convert one-off actions into reusable engineering steps.
   - For each step explain: what was done, why it mattered, and what would break if skipped.

3. **Trace the real chain**
   - For code or robotics tasks, include the real data/control path.
   - Use file paths, topics, functions, parameters, commands, and logs from the user's task.
   - Mark inference clearly when exact evidence is not available.

4. **Extract concepts**
   Classify concepts into these buckets when relevant:
   - 数学层面: geometry, coordinate transforms, vectors, matrices, optimization, probability.
   - 物理层面: kinematics, dynamics, sensing, signals, friction, inertia, torque.
   - 计算机层面: Linux, ROS, processes, networking, CAN, ADB, concurrency, file I/O.
   - 算法与数据结构: IK, filtering, search, rate limiting, interpolation, solvers.
   - 工程与控制: feedback, feedforward, deadband, calibration, gain tuning, safety limits.

5. **Decompose recursively**
   For each important concept, explain:
   - **Why**: the problem it solves.
   - **What**: intuitive definition and precise definition.
   - **How**: how it appears in this task, preferably with code, formulas, logs, or parameters.
   - **Prerequisites**: the concepts underneath it, repeated until high-school-level foundations.

6. **Write or update the artifact**
   - Default path: `<current-project>/docs/deep-learn/<YYYY-MM-DD>-<short-slug>.md`.
   - If editing an existing note, preserve user-written content unless it is clearly duplicated.
   - Use `references/output-template.md` for full notes or major enrichments.

7. **Validate understanding**
   - Add 5-10 questions from recall to transfer.
   - If the user enters Q&A mode, use `references/qa-rubric.md`.

## Reference Files

Load these only when needed:

- `references/output-template.md`: use when creating or substantially enriching a Markdown note.
- `references/qa-rubric.md`: use when asking or assessing diagnostic questions.
- `references/robotics-examples.md`: use for ROS, VR teleoperation, IK, Piper, CAN, ADB,
  coordinate-frame, or joint-direction debugging tasks.

## Style For This User

- Write main explanations in Chinese.
- On first use, include bilingual technical terms: `齐次变换矩阵 (Homogeneous Transformation Matrix)`.
- Prefer the user's real robotics examples over generic examples.
- Include concrete file names, ROS topics, environment variables, parameters, and commands.
- When explaining formulas, define every symbol.
- Use ASCII diagrams when they clarify data flow or coordinate frames.
- Separate "已经确认的事实" from "推断/嫌疑".
- Keep safety context visible for robot motion: deadman, rate limits, workspace limits, backups,
  and test-without-hardware steps.

## Quality Checklist

Before finishing, check:

- The task goal and outcome are clear.
- The end-to-end chain is traceable from input to output.
- At least three concept categories are represented when the topic is broad.
- At least one important concept is explained down to basic algebra, geometry, physics, or
  programming foundations.
- Code snippets and parameter examples come from the user's actual context.
- The note includes practical debugging or verification steps.
- Q&A questions test reasoning, not just definitions.
