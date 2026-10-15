# Product Thinking · 产品思考三步法

一套中文 Agent Skill：先通过苏格拉底提问把问题问清，再用第一性原理拆解用户价值与事实，最后用奥卡姆剃刀选择更简单、可验证的方案。

## 适用场景

- 判断产品或功能是否值得做、需求是否真实。
- 分析定价、订阅、商业模式、留存、流失和功能优先级。
- 将模糊产品想法拆成可执行的最小验证方案。

工作流会区分事实、假设与推断，比较解释或方案，并给出验证动作、成功标准和下一步。它辅助判断，不保证市场需求或商业结果。

## 目录

```text
product-thinking/
├── SKILL.md
├── rules/
│   ├── problem-context.md
│   ├── socratic.md
│   ├── first-principles.md
│   ├── occam.md
│   └── output.md
├── README.md
├── LICENSE
└── .gitignore
```

入口为 [SKILL.md](SKILL.md)，详细流程通过相对路径读取 `rules/`。安装时需保留整个 `rules/` 目录。

## 本地安装

下载或克隆本仓库后，在仓库根目录运行以下命令（macOS / Linux，Bash 或 Zsh）：

```bash
(
  set -eu
  skill_dir="$HOME/.agents/skills/product-thinking"
  if [ -e "$skill_dir" ] || [ -L "$skill_dir" ]; then
    echo "技能目录已存在，请先检查已有版本：$skill_dir"
    exit 1
  fi
  mkdir -p "$skill_dir"
  cp SKILL.md LICENSE "$skill_dir/"
  cp -R rules "$skill_dir/"
)
```

这会安装到当前用户的 `~/.agents/skills/product-thinking/`。如果已有同名技能装在 `~/.codex/skills/`，先检查是否为已有安装或软链接，避免重复安装。若技能列表未更新，可重启 Codex。

## 使用示例

在 Codex 中输入 `$` 选择技能，或直接发送：

```text
$product-thinking 我想做一个帮助个人整理读书笔记的工具。
目标用户是每周阅读的上班族，目前只有想法，没有访谈数据。
请比较按次付费与月订阅，并给出一周内可执行的最小验证方案。
```

以上为虚构场景。典型输出包含：问题重述、关键判断、三步法分析、最小验证方案、下一步和可复用 Prompt。缺少会改变判断的背景时，技能会优先澄清关键问题。

## 兼容性与数据边界

这是遵循 `SKILL.md` 目录约定的文本技能，当前版本没有可执行脚本、MCP 配置或网络上传代码。此前已在本机 Codex 技能加载检查中验证技能可被识别；不同模型的实际输出可能不同。

Codex 桌面端与 CLI 可通过本地技能目录发现技能。ChatGPT 桌面端的可用性取决于客户端功能和技能发现配置；本仓库尚未验证其端到端调用。复制本地文件不会自动同步到 ChatGPT 网页版或手机端。

技能运行时，宿主模型或工具可能处理用户提供或授权读取的材料。请遵守所在组织的数据与模型使用政策。仓库的示例为虚构场景，提交 Issue、截图或改进示例时也请勿附带真实公司文档、客户信息、凭据或内部链接。

## 修改与贡献

直接修改 `SKILL.md` 或其引用文件即可调整工作流。提交修改时，请说明适用场景和预期行为，检查相对引用是否有效，并使用虚构材料验证。新增文件前请检查内容和 Git 暂存区；`.gitignore` 不能识别 Markdown 正文中的敏感信息。

## 许可证

本项目采用 [MIT License](LICENSE)，允许在保留许可要求的前提下使用、修改和分发，包括商业用途。技能输出需要人工复核，项目按许可证中的 “AS IS” 条款提供。
