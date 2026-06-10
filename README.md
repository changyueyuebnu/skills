# skills

这个仓库收集我自己常用或觉得好用的「技能」（Skill），主要面向 AI 辅助编程、论文写作等场景。每个 skill 是一个 Markdown 文件，描述特定任务的提示词或工作流程。我自己用的Claude code + DeepSeek

## 已有 Skill

### `latex-chinese-summary`

- **功能**：自动读取当前文件夹下的 `main.tex` 文件（可以在arXiv官网上下载），提取论文或文档的中文核心内容，并生成一份中文总结，写入 `template.tex` 文件中。
- **适用场景**：LaTeX 论文/报告的快速摘要生成，便于协作或知识整理。
- **使用方法**：
  1. 将本仓库克隆到本地。
  2. 在包含 `main.tex` 的目录下，将 `latex-chinese-summary.md` 的内容提供给 AI（例如通过自定义指令或复制对话中）。
  3. AI 根据指令执行：分析 `main.tex` → 提炼中文总结 → 输出至 `template.tex`。
- **注意**：需要 AI 支持文件读写操作。论文还是要自己读的，这个skill是为那些有阅读总结任务的课题组定制的～～
