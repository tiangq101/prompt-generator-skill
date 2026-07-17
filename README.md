# Prompt Generator Skill

一个用于 Codex 的通用专业提示词生成 skill。它可以把用户的粗略需求转换成结构化、可执行、可复用的高质量 Prompt。

## 产品功能

`prompt-generator` 适合这些场景：

- 帮你从零写一个专业提示词。
- 优化已有 Prompt，让目标、上下文、输出格式和约束更清楚。
- 把一句模糊需求改成 AI 可以直接执行的任务指令。
- 为固定工作流生成可复用 Prompt 模板。
- 在信息不足时，先追问关键问题，再生成最终 Prompt。

## 工作流程

这个 skill 不会一上来就直接生成 Prompt，而是按下面流程执行：

1. 用户先描述自己的需求。
2. AI 判断信息是否足够。
3. 如果缺少关键信息，AI 会先提问让用户补充。
4. 当 AI 没有疑问后，开始生成结构化 Prompt。
5. 生成前会自检 Prompt 是否清晰、完整、可执行。

## 默认输出结构

生成的 Prompt 默认使用中文，并采用结构化模板：

```markdown
# 角色
# 任务目标
# 背景信息
# 输入内容
# 工作流程
# 输出格式
# 约束要求
# 质量标准
```

如果用户明确要求英文或其他格式，skill 会按用户要求调整。

## 安装方法

把仓库克隆到本地：

```bash
git clone https://github.com/tiangq101/prompt-generator-skill.git
```

复制 skill 到 Codex skills 目录：

```bash
mkdir -p ~/.codex/skills
cp -R prompt-generator-skill/prompt-generator ~/.codex/skills/
```

然后重启或刷新 Codex，让 Codex 重新发现这个 skill。

## 使用方式

在 Codex 中可以这样说：

```text
帮我写一个提示词：我想让 AI 帮我分析用户访谈内容，提炼产品机会点。
```

也可以显式调用：

```text
Use $prompt-generator to help me create a reusable prompt for summarizing meeting notes.
```

当信息不足时，它会先问类似问题：

```text
1. 这个 Prompt 的最终使用对象是谁？
2. 你希望输出成表格、Markdown 文档，还是 JSON？
3. 有没有必须遵守的语气、长度或业务限制？
```

信息足够后，它会输出可直接复制使用的完整 Prompt。

## 适合谁使用

- 经常需要写 Prompt 的产品经理、运营、分析师、创作者。
- 想把零散需求变成稳定 AI 指令的人。
- 想沉淀团队 Prompt 模板的人。
- 想减少 AI 回答跑偏、格式不稳定、目标不清楚问题的人。

## 仓库结构

```text
prompt-generator-skill/
├── README.md
└── prompt-generator/
    ├── SKILL.md
    └── agents/
        └── openai.yaml
```

## 更新方法

如果仓库后续更新，进入本地仓库后执行：

```bash
git pull
cp -R prompt-generator ~/.codex/skills/
```

然后重启或刷新 Codex。
