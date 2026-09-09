# Skills 的按需加载：和"一坨长提示词"的根本区别

> 来源：Anthropic 官方文档《Agent Skills · Overview》
> URL: https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview
> 官方工程博客：https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills
> 检索日期：2026-09-09
> **状态：待审查**（官方文档，事实性可靠；表述需讲师自行口语化）

## 官方定义（可直接引用）

官方文档对 Skills 与 prompts 的对比原话：

> Unlike prompts (conversation-level instructions for one-off tasks), **Skills load on demand**, so you don't have to repeat the same guidance across conversations.
> （与"针对一次性任务的对话级指令"不同，Skills 是按需加载的，你不必在每次对话里重复同样的要求。）

## 三级渐进式披露（progressive disclosure）——核心机制

| 层级 | 何时加载 | 代价 | 内容 |
| --- | --- | --- | --- |
| Level 1 元数据 | **始终加载**（启动时进系统提示词） | **约 100 tokens / 每个 Skill** | 只有 name + description（YAML frontmatter） |
| Level 2 正文 | **被触发时才加载** | 建议 < 5k tokens | SKILL.md 正文：流程、规范、最佳实践 |
| Level 3 资源 | **需要时才加载** | 未读取则为 0 | 附带文件：参考文档、模板、脚本 |

## 三个可直接上屏的官方说法

1. **"装很多也不心疼"**：官方原话——因为未触发时只有 name 和 description 占位，**你可以安装很多 Skills 而不付出上下文代价**（install many Skills without context penalty）。
2. **脚本不占上下文**：Claude 用 bash 运行脚本时，**脚本代码本身从不进入上下文窗口，只有运行结果（如 "Validation passed"）进入**。
3. **可打包的内容实际上没有上限**：因为文件在被访问前不消耗上下文，Skills 可以塞进完整 API 文档、大型数据集、大量示例——**没被用到的部分零成本**。

## 官方给的类比（很好用）

- Anthropic 工程博客原话：**"给 Agent 做一个 skill，就像给新员工写一份入职指南。"**（Building a skill for an agent is like putting together an onboarding guide for a new hire.）
- 渐进式披露的比喻：**像一本组织良好的手册——先看目录，再翻具体章节，最后才是详细附录。**

## 教学转述（讲师参考）

- Skills ≠ 更长的提示词。长提示词是**每次对话都要整段念一遍**；Skills 是**平时只在系统里挂个名字（约 100 tokens），用的时候才把正文拿进来**。
- 类比（本课件采用）：**像手机里的 App——装在那儿不耗电，打开了才占内存。**
  - 注意断裂点：App 打开后代码全进内存，而 Skill 的附带文件仍是按需读取。所以更准确的说是"带目录的活页夹"。
- Skills 还能打包脚本：脚本**代码不进上下文，只有运行结果进**——这也是长提示词做不到的。

## 使用限制

- 这是 Anthropic 自家实现；其他平台的"技能/智能体"未必是同一套机制。课堂上**讲机制原理，不讲具体平台品牌**。
- 非技术岗学员不需要知道 SKILL.md、YAML、token 这些词，**只讲"平时不占地方，用的时候才拿出来"**。
