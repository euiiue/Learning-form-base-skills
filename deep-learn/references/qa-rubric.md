# Deep Learn Q&A Rubric

Use this reference when the user wants interactive learning or when a note needs stronger
assessment questions.

## Question Types

Use a balanced set:

- **Recall**: Can the user repeat the core definition or data path?
- **Mechanism**: Can the user explain why A causes B?
- **Code trace**: Can the user follow a value through files, functions, topics, or parameters?
- **Debugging**: Can the user choose the next observation or experiment from a symptom?
- **Transfer**: Can the user apply the principle to a related but new setup?

## Difficulty Labels

- **基础**: One concept, direct answer, no multi-step reasoning.
- **进阶**: Two or three linked concepts, requires causal explanation.
- **综合**: Requires reading a symptom, choosing evidence, and proposing a safe change.

## Assessment Levels

After each answer, classify it:

- **掌握**: Correct, causal, and uses task-specific details.
- **基本掌握**: Mostly correct but missing one key term, unit, or boundary condition.
- **部分掌握**: Contains a useful intuition but mixes up cause/effect or frame/unit/direction.
- **未掌握**: Cannot explain the core relation or chooses an unsafe/unrelated action.

## Feedback Pattern

For every answer:

1. State what is correct.
2. State the exact missing or incorrect piece.
3. Give a corrected explanation in one smaller layer.
4. Ask one follow-up question only if needed.

Avoid long lectures after every answer. Save deep re-teaching for repeated misses or safety-critical
misunderstandings.

## Robotics-Specific Diagnostic Prompts

Use these patterns for robotics and control tasks:

- "这个变量在哪个坐标系里？单位是什么？"
- "这个频率控制的是采样、求解、发命令，还是反馈？"
- "如果方向反了，是改轴映射、符号、还是 IK 算法？为什么？"
- "这个日志能证明什么？还有什么不能证明？"
- "如果不启动真实驱动，怎么验证上游逻辑没有崩？"
- "这个改动的最小实机测试是什么？停止条件是什么？"

## Mini Exercise Patterns

- Draw the data path as ASCII.
- Change one parameter and predict which log/topic/hardware behavior changes.
- Given a short log snippet, identify the next observation command.
- Explain the same concept once to an engineer and once to a high-school student.
- Propose a safe rollback path before an实机 test.
