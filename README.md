# Progressive Investment Research

一个用于维护长期研究 dossier 的 agent skill。

它不是报告生成器。它的核心任务是维护一个可恢复、可审计、可持续更新的研究模型：我们现在怎么看、证据是什么、哪里仍不确定、什么信号会改变判断，以及哪些文件是事实和模型的 canonical source。

[English README](README.en.md)

## 这个 Skill 解决什么问题

- 为一个研究主题建立轻量 Markdown dossier。
- 以 `current-synthesis.md` 作为人类恢复当前模型的入口。
- 用 `model-map.md`、`modules/`、`models/`、`open-questions.md`、`update-log.md` 分离结论、证据、计算、开放问题和状态变化。
- 把数字、假设、公式、来源质量、权限边界当成一等研究对象，而不是埋在长文里。
- 适合投资研究、行业研究、公司研究、技术主题研究，以及任何会持续演化的问题。

## 公开版依赖模型

公开版设计目标是：没有私有工具或本地专用工具也能工作。

核心能力只需要：

- 一个能读写文件的 agent runtime。
- Python 3.10+，用于运行 `scripts/` 里的可选辅助脚本。

可选加速器：

- Web search 或 browser 工具，用于公开来源发现。
- URL 正文抽取工具，用于已知网页。
- PDF、Office、表格解析工具，用于用户提供的文件。
- 本地工具，例如 AnySearch、web-access、markitdown、pdf/docx/xlsx/pptx skills、RSS pipeline 等。

如果这些加速器不存在，不要中断研究。直接使用当前 agent runtime 可用的搜索、浏览、URL fetch 或文件读取能力。fallback 规则很简单：记录来源、标注来源质量和权限状态，不要把搜索 snippet、二手摘要或未复核材料直接提升为模型结论。

## 安装

把这个目录复制到你的 agent skill/plugin 目录，或者在支持本地 skill 加载的 runtime 中直接指向这个文件夹。

Codex 风格加载需要：

- `SKILL.md`
- `.codex-plugin/plugin.json`
- `references/`
- `templates/`
- `scripts/`

Claude 风格加载还包含：

- `.claude-plugin/plugin.json`
- `agents/`

## 快速开始

创建一个新 dossier：

```powershell
python scripts/scaffold_dossier.py "./my-topic" --title "My Topic"
```

验证 dossier：

```powershell
python scripts/validate_dossier.py "./my-topic" --strict
```

打印简单索引：

```powershell
python scripts/regenerate_index.py "./my-topic" --stdout
```

## Dossier 结构

最小活跃面：

- `context.md`：入口协议、范围、接续说明。
- `current-synthesis.md`：当前模型和人类恢复入口。
- `model-map.md`：研究边界、分析轴、模块和开放问题。
- `open-questions.md`：`active` / `monitor` / `watchlist` 状态索引。
- `update-log.md`：模型变化日志。
- `modules/`：证据模块、概念模块、registry、审计记录。

按需增加：

- `models/`：计算模型和公式驱动的推理。
- `companies/`：公司 watchlist cards。
- `data/`：模型使用的 canonical rows 或 CSV。
- `archive/`：默认不读取的历史材料和生成物。

## 示例 Fixture

`fixtures/ai-industry-chain-mini/` 是一个基于长期研究 dossier 结构模式重构的公开 mini fixture。它已经去敏：

- 用来展示当前 skill contract。
- 内容是 public-style 和 illustrative 的。
- 不是投资建议。
- 不是完整研究数据库。

## 测试

运行轻量 contract tests：

```powershell
python tests/test_contract.py
```

测试只使用 Python 标准库。

## 发布边界

公开仓库应保留：

- `SKILL.md`
- `.codex-plugin/`
- `.claude-plugin/`
- `.gitattributes`
- `agents/`
- `references/`
- `scripts/`
- `templates/`
- `fixtures/`
- `evals/`
- `tests/`
- `README.md`
- `README.en.md`
- `LICENSE`

不要提交本地 dossier、私有材料、缓存目录、生成报告、`.env` 文件或 Python bytecode。

## License

MIT. See `LICENSE`.
