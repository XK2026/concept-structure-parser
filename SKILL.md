---
name: concept-structure-parser
description: Parse learning materials, textbook excerpts, lecture slides, notes, PDFs, or course concepts by decomposing definition sentences into "A is B" structures, action/process sentences into "A acts on B by doing C" structures, and qualifiers into scope, condition, feature, function, boundary, examples, counterexamples, and confusion points. Use when a learner asks Codex to explain new concepts, analyze university course PPTs, turn dense definitions into learnable structure, or study through subject-predicate-complement and subject-verb-object decomposition.
---

# Concept Structure Parser

## Goal

Help a learner understand course materials by turning dense academic language into explicit concept structures. Preserve the original meaning, reveal the core relation first, then explain qualifiers and boundaries.

Default to Simplified Chinese unless the user requests another language.

## Core Workflow

1. Identify candidate knowledge units: definitions, mechanisms, causal statements, classifications, processes, formulas with verbal meaning, and important terms.
2. Classify each unit as one or more of:
   - Definition: explains what something is.
   - Action/process: explains what acts on what, through which operation.
   - Relation: explains inclusion, contrast, cause, dependency, condition, or sequence.
   - Example/application: illustrates where the concept appears or how it is used.
3. Extract the skeleton first.
4. Explain qualifiers next.
5. Rewrite the idea in the learner's words.
6. Add examples, counterexamples, and confusion points when useful.
7. Keep traceability to the source when working from files: cite slide number, page number, section title, or quoted short phrase when available.

## Definition Sentences

For definition-like text, produce this structure:

```text
原句/来源：
核心骨架：A 是 B
A：被定义对象
B：上位类/本质归属
关键限定词：
- 限定词：作用类型；为什么重要；去掉后概念会怎样变化
用自己的话：
正例：
反例：
容易混淆：
一句话记忆：
```

When analyzing `A 是 B`, check whether `B` is a true upper category. If it is not, describe the actual relation, such as property, function, role, result, or metaphor.

Treat qualifiers as potentially essential. Do not dismiss adjectives, adverbs, clauses, or prepositional phrases as decoration. Decide whether each qualifier expresses:

- 范围限制
- 条件限制
- 对象限制
- 时间/空间限制
- 程度限制
- 方式/手段
- 功能/目的
- 关键属性
- 与相近概念的区别
- 必要定义边界

If removing a qualifier changes the concept's identity, mark it as `必要边界`.

## Action And Process Sentences

For mechanism, operation, process, or cause-effect text, produce this structure:

```text
原句/来源：
核心骨架：A 对 B 做 C
A：动作主体
B：动作对象
C：动作/操作
条件：
方式/工具：
结果：
关键限定词：
- 限定词：作用类型；为什么重要
用自己的话：
过程链：
容易混淆：
```

If the sentence is passive, restore the active relation when possible:

```text
被动句：B 被 C 处理/影响
还原：A 对 B 做 C
```

If the actor is hidden or unknown, write `隐含主体：未知/教材未说明/可从上下文推断为...` instead of inventing certainty.

For multi-step mechanisms, convert the explanation into a chain:

```text
第 1 步：A 对 B 做 C
第 2 步：C 导致 D
第 3 步：D 影响 E
最终结果：...
```

## Relation Sentences

When a sentence is not a definition or action, map the relation explicitly:

```text
关系类型：包含/属于/导致/依赖/对比/条件/顺序/组成/功能/限制
关系骨架：A 与 B 的关系是 R
限定条件：
学习提醒：
```

For comparisons, include:

```text
相同点：
差异点：
区分标准：
易错说法：
```

## Output Style

Prefer compact, learnable output over long summaries. For a slide deck or chapter, start with a short concept map:

```text
本节核心概念：
1. 概念 A：一句话
2. 概念 B：一句话

概念之间的关系：
A 是 B 的一种...
C 对 D 做 E...
F 在条件 G 下导致 H...
```

Then analyze the most important concepts one by one. If there are many concepts, prioritize definitions and mechanisms that are central to exams, assignments, or later reasoning.

Use tables when there are many parallel concepts. Use prose when a concept needs careful explanation.

## Quality Checks

Before finalizing, verify:

- The skeleton preserves the original meaning.
- Each important qualifier is classified.
- Necessary boundaries are not removed.
- Passive or hidden-agent sentences are handled honestly.
- Examples and counterexamples fit the definition.
- The explanation distinguishes "what it is" from "what it does".
- The output helps the learner reconstruct the concept without memorizing the original long sentence.

## What To Avoid

- Do not only summarize the material.
- Do not replace the source concept with an oversimplified analogy.
- Do not silently drop qualifiers that define scope or boundary.
- Do not invent actors, causes, or examples without marking them as inference.
- Do not produce a huge exhaustive extraction when the user asks for learning help; prioritize structure and understanding.
