---
name: prompt-generator
description: Generate, refine, or rewrite professional structured prompts from rough user requirements. Use when the user asks to write a prompt, optimize a prompt, create a professional prompt, turn a task into an AI-executable instruction, or design a reusable prompt template. Default to Chinese unless the user requests another language.
---

# Prompt Generator

## Core Rule

Do not generate the final prompt until the user's intent, target output, required context, and constraints are clear enough for another AI to execute.

If critical information is missing, ask concise clarifying questions first. Generate the prompt only after the user answers or explicitly asks you to proceed with assumptions.

## Workflow

1. Parse the user's requirement.
2. Decide whether the information is sufficient.
3. If insufficient, ask only the missing questions that materially affect prompt quality.
4. If sufficient, generate one complete structured prompt.
5. Run the self-check before responding.

## Clarifying Questions

Ask questions when any of these are unclear:

- Task goal: what the AI should accomplish.
- Target user or audience: who will use or read the result.
- Input material: what the user will provide to the AI.
- Output format: document, table, JSON, code, checklist, analysis, etc.
- Style or tone: concise, professional, conversational, academic, sales-oriented, etc.
- Constraints: length, language, forbidden content, tools, sources, deadline, assumptions.
- Quality standard: what counts as a good answer.

Question rules:

- Ask in Chinese by default.
- Ask no more than 5 questions in one turn.
- Number the questions.
- Do not ask about information that can be reasonably inferred from the user's request.
- If only minor details are missing, state assumptions and proceed.
- If the user says "直接生成", "你自己决定", or equivalent, proceed with explicit assumptions.

## Final Prompt Template

Use this structure unless the user's task clearly needs a different format:

```markdown
# 角色
你是[专业角色]，擅长[关键能力/领域]。

# 任务目标
你的目标是[明确说明要完成的任务和最终结果]。

# 背景信息
[写入用户提供的上下文、业务背景、使用场景、目标受众。缺失但必要的信息用占位符标注。]

# 输入内容
用户会提供以下信息：
- [输入 1]
- [输入 2]
- [输入 3]

# 工作流程
请按以下步骤完成任务：
1. [步骤 1：理解/解析/提取]
2. [步骤 2：分析/判断/整理]
3. [步骤 3：生成/改写/输出]
4. [步骤 4：自检/优化]

# 输出格式
请严格按照以下格式输出：
[定义标题、表格、字段、JSON schema、Markdown 结构或其他格式要求]

# 约束要求
- 默认使用中文，除非用户另有要求。
- 不要编造用户没有提供的事实、数据、案例或来源。
- 信息不足时，先说明缺口或使用明确占位符。
- 保持表达清晰、具体、可执行。
- [加入用户指定的其他限制]

# 质量标准
最终结果需要满足：
- 目标明确，没有歧义。
- 输出格式稳定，可直接复制使用。
- 步骤完整，但不冗长。
- 约束被严格遵守。
- 对缺失信息有清楚处理方式。
```

## Prompt Quality Heuristics

Include these elements when useful:

- Role: define the model's expertise and perspective.
- Task: state the exact job to complete.
- Context: include relevant background and audience.
- Inputs: specify what information the user will provide.
- Process: provide an ordered workflow for complex tasks.
- Output format: make the final response shape explicit.
- Constraints: define language, length, style, source, and safety boundaries.
- Examples: add examples only when they clarify the desired output.
- Evaluation criteria: define what a high-quality result looks like.

## Response Format

When asking clarifying questions, respond only with the questions and a short reason if needed.

When generating the final prompt:

1. Start with `下面是生成好的专业提示词：`
2. Put the prompt in a Markdown code block.
3. If assumptions were used, add a short `使用假设` section before the code block.
4. Do not add long explanations after the prompt.

## Self-Check

Before finalizing, verify:

- Could another AI execute the prompt without needing hidden context?
- Are the role, task, inputs, workflow, output format, constraints, and quality standard clear?
- Are vague words like "专业", "详细", "高质量" translated into concrete requirements?
- Did you avoid fabricating details not provided by the user?
- Is the final prompt concise enough to use directly?
