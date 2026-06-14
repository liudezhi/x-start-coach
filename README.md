# X Start Coach

`x-start-coach` 是一个面向 AI 编程代理的通用概念学习 Skill，适用于 Codex、Gemini CLI、Claude Code 以及其他兼容 [Agent Skills](https://agentskills.io/) 规范的工具。

它的目标不是简单解释术语，而是帮助学习者完成下面的转变：

> 从“听说过这个概念”，到“能够准确解释、区分相邻概念，并在真实场景中应用”。

## 主要能力

- 用适合初学者的语言解释技术、科学、商业、经济、金融、法律、医学、人文等领域的概念。
- 先讲直觉，再引入专业术语，并明确类比的适用边界。
- 对比容易混淆的概念，给出统一维度的对比表和选择标准。
- 通过苏格拉底式提问检查理解程度，每次只推进一个问题。
- 审查已有教程中的定义错误、概念混淆、过时信息和误导性类比。
- 生成 Markdown 教程、知识卡片、自测题、学习路径和关系图。
- 根据当前代理能力使用搜索、文件、Mermaid 或图片生成工具。
- 在工具不可用时自动降级，不因缺少绘图或文件能力而中断讲解。

## 工作模式

Skill 会根据用户目标选择合适的模式：

| 模式 | 适用场景 |
| --- | --- |
| 快速解释 | 想迅速理解一个术语或概念 |
| 深度教程 | 想系统学习并形成可复用文章 |
| 概念对比 | 容易混淆多个相邻概念 |
| 苏格拉底训练 | 希望通过问答检验理解 |
| 教程审查 | 检查已有内容是否准确、清晰 |
| 制品生成 | 生成教程、图表、知识卡片或脚本 |

## 设计特点

### 平台无关

核心流程不依赖特定模型、工具名、操作系统或图片生成服务。Skill 会先判断当前环境提供了哪些能力，再选择对应工具。

### 渐进式讲解

讲解通常从以下层次展开：

1. 一句话定义
2. 概念解决的问题
3. 直观类比及其边界
4. 在更大体系中的位置
5. 工作机制
6. 具体例子
7. 与相邻概念的区别
8. 常见误区和失效条件
9. 自测与记忆总结

这些部分会根据任务裁剪，不会机械地塞进每一次回答。

### 可验证的信息

遇到产品版本、法律政策、医学指南、行业标准、统计数据等可能变化的内容时，Skill 会优先查阅官方文档、法规、监管机构或原始研究，并区分事实、推断和争议观点。

## 目录结构

```text
x-start-coach/
├── SKILL.md
├── README.md
├── agents/
│   └── openai.yaml
└── references/
    └── prompt-templates.md
```

- `SKILL.md`：平台无关的核心教学流程。
- `references/prompt-templates.md`：中文学习、对比、训练和审稿提示模板。
- `agents/openai.yaml`：Codex 可选的界面元数据，不影响其他平台使用。

## 安装

### Codex

安装为用户级 Skill：

```bash
git clone https://github.com/liudezhi/x-start-coach.git ~/.agents/skills/x-start-coach
```

也可以安装到项目目录：

```text
<项目根目录>/.agents/skills/x-start-coach/
```

### Gemini CLI

Gemini CLI 同样支持通用的 `.agents/skills/` 路径：

```bash
git clone https://github.com/liudezhi/x-start-coach.git ~/.agents/skills/x-start-coach
```

也可以使用 Gemini CLI 的安装命令：

```bash
gemini skills install https://github.com/liudezhi/x-start-coach.git
```

### Claude Code

安装到 Claude Code 的用户级 Skill 目录：

```bash
git clone https://github.com/liudezhi/x-start-coach.git ~/.claude/skills/x-start-coach
```

项目级安装路径为：

```text
<项目根目录>/.claude/skills/x-start-coach/
```

安装后如未立即出现，请刷新 Skill 列表或重启对应客户端。

## 使用示例

### 学习一个概念

```text
请用 x-start-coach 帮我理解什么是 MCP。我是初学者，但希望最后能把它讲给开发者听。
```

### 对比概念

```text
对比 LLM、AI Agent 和 Agent Runtime，先给结论，再用表格和 Mermaid 关系图解释。
```

### 苏格拉底训练

```text
围绕 RAG 连续问我 6 个问题，每次只问一个，根据我的回答逐步提高难度。
```

### 生成教程

```text
把“现金流和利润的区别”整理成一篇面向创业者的中文 Markdown 教程，并加入自测题。
```

### 审查已有内容

```text
审查下面这段关于微服务的解释，指出定义错误、遗漏条件和可能误导初学者的类比。
```

更多可复用提示词参见 [`references/prompt-templates.md`](references/prompt-templates.md)。

## 适用边界

- 本 Skill 侧重概念学习和教学，不应仅因任务中出现技术或行业术语而触发。
- 医疗、法律和金融内容用于一般教育，不替代专业诊断、法律意见或投资建议。
- 当某个领域存在更专业、更具体的 Skill 时，应优先使用领域 Skill。

## 开放规范

本项目采用 Agent Skills 的通用目录格式：

- 使用 `SKILL.md` 描述触发条件和执行流程。
- 使用 `references/` 按需加载补充材料。
- 通过渐进式披露减少上下文占用。
- 核心内容保持平台无关，各平台专属元数据作为可选适配层。

