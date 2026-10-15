# Product Thinking · 产品需求分析三步法

面向互联网公司 PM（产品经理）和全栈工程师的中文 Agent Skill，帮助你在写 PRD、排需求优先级或进入开发之前，判断需求是否真实、功能是否值得做，以及怎样用更低成本验证。

工作流结合苏格拉底提问、第一性原理和奥卡姆剃刀：先把需求问清楚，再拆解用户价值与事实，最后比较方案，落到可执行的最小验证动作。

## 适用人群

- **PM / 产品经理**：梳理业务方或用户提出的需求，明确目标用户、使用场景、问题证据、需求边界与成功标准，为 PRD 和需求评审提供依据。
- **全栈工程师 / 研发人员**：承接模糊需求或独立负责产品时，先厘清“为什么做、解决什么问题、先做哪一部分”，再决定实现范围，减少无效开发。

## 适用场景

- **需求分析**：面对“用户说想要”“业务方要求加一个功能”，判断背后的问题是否真实，以及现有方案为什么不够用。
- **需求评审与优先级**：比较做、不做或轻量替代方案，明确核心需求与边缘需求，收敛首版范围。
- **产品迭代**：分析转化、留存或流失问题，区分事实与假设，避免直接把问题归因于功能不足。
- **商业化判断**：分析定价、订阅与商业模式是否符合用户价值及使用频率。
- **开发前验证**：把产品想法拆成用户访谈、人工交付或低保真原型等最小实验，明确验证动作和成功标准。

典型输出包括问题重述、关键判断、事实与假设、方案比较、最小验证方案和下一步，可作为需求讨论与 PRD 编写的输入。判断质量依赖你提供的背景和证据，仍需结合真实用户反馈与团队评审。

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

## 从 GitHub 下载并安装到 Codex

以下命令适用于 macOS / Linux 的 Bash 或 Zsh。请先安装 Git 和 Codex CLI，并确认已经登录：

```bash
git --version
codex --version
codex login status
```

若尚未登录，运行 `codex login` 并完成登录。CLI 安装及账号要求见 [Codex CLI 官方说明](https://learn.chatgpt.com/docs/cli)。

### 下载与安装（整段复制到终端）

这段命令会从公开 GitHub 仓库克隆当前版本，只复制技能需要的文件和许可证，并在退出时删除下载临时目录；不会上传本地项目。已存在同名安装时会停止，请先检查已有版本。

```bash
(
  set -eu
  command -v git >/dev/null
  command -v codex >/dev/null
  skill_dir="$HOME/.agents/skills/product-thinking"
  legacy_skill_dir="${CODEX_HOME:-$HOME/.codex}/skills/product-thinking"
  if [ -e "$skill_dir" ] || [ -L "$skill_dir" ] || [ -e "$legacy_skill_dir" ] || [ -L "$legacy_skill_dir" ]; then
    echo "发现同名技能，请先检查已有安装：$skill_dir 或 $legacy_skill_dir"
    exit 1
  fi
  download_dir="$(mktemp -d)"
  trap 'rm -rf "$download_dir"' EXIT
  git clone --depth 1 https://github.com/score2021/product-thinking.git "$download_dir/product-thinking"
  mkdir -p "$skill_dir"
  cp "$download_dir/product-thinking/SKILL.md" "$download_dir/product-thinking/LICENSE" "$skill_dir/"
  cp -R "$download_dir/product-thinking/rules" "$skill_dir/"
  test -f "$skill_dir/SKILL.md"
  echo "安装完成：$skill_dir"
)
```

技能安装到当前用户的 `~/.agents/skills/product-thinking/`，可在不同项目中使用。[Codex 官方技能文档](https://learn.chatgpt.com/docs/build-skills)说明了该用户级发现路径。不要把它复制成 `~/.agents/skills/product-thinking/product-thinking/SKILL.md` 这样的多层目录。

### 在 Codex 中调用

安装后新开一个 Codex 会话。CLI 运行 `codex`，输入 `/skills` 查看已发现的技能，或输入 `$` 搜索 `product-thinking`；桌面端在新会话中输入 `$` 选择该技能。未出现时重启客户端。

也可以直接在终端执行以下完整命令进行一次真实调用。命令使用单引号保留 `$` 技能标记；`--skip-git-repo-check` 允许在非 Git 目录演示，`read-only` 限制本地文件写入。

```bash
codex exec --skip-git-repo-check --sandbox read-only '$product-thinking 请用三步法分析以下虚构想法：为每周阅读的上班族提供读书笔记整理服务。目前没有访谈或付费数据，用户现在用普通文档记录，只有一人和一周时间，目标是验证真实付费意愿。请比较按次付费与月订阅，区分事实和假设，给出最小验证方案；缺失背景标注为假设。'
```

正常结果应包含问题重述、事实与假设、三步法分析，以及带动作和成功标准的最小验证方案。只看到“安装完成”还不能证明调用成功，需要检查 Codex 的实际输出。

### 常见问题

- `codex: command not found`：先安装 Codex CLI，或修复终端 `PATH`。
- 登录失败、模型无权限、额度不足或网络错误：先解决 Codex 账号和连接问题；安装技能本身不会提供模型访问权限。
- 找不到技能：检查 `~/.agents/skills/product-thinking/SKILL.md` 存在，并重启 Codex；检查配置中是否禁用了该技能。
- 提示同名技能已存在：检查 `~/.agents/skills/` 和 `${CODEX_HOME:-~/.codex}/skills/` 的已有目录或软链接，再决定保留哪个版本；不要直接覆盖未知文件。
- GitHub 克隆失败：检查 GitHub 的 HTTPS 连接；安装命令会清理下载临时目录。若复制阶段中断，先检查目标目录是否完整，再决定是否重新安装。

## 使用示例

在 Codex 中输入 `$` 选择技能，或直接发送：

```text
$product-thinking 我是一家互联网公司的 PM，正在分析一个虚构需求：
业务方希望给团队协作产品增加“批量导出任务报表”功能。
目标用户是需要每周汇总进度的项目负责人，目前通过复制任务信息制作周报。
现在只有业务方反馈，没有用户访谈和使用数据，研发资源是一名全栈工程师、一周时间。
请先判断真实问题和待验证假设，比较完整报表、简单 CSV 导出与人工辅助三种方案，
给出需求优先级、首版范围和开发前的最小验证动作，作为后续 PRD 与需求评审的输入。
```

以上为虚构场景。典型输出包含：问题重述、关键判断、三步法分析、最小验证方案、下一步和可复用 Prompt。缺少会改变判断的背景时，技能会优先澄清关键问题。

## 兼容性与数据边界

这是遵循 `SKILL.md` 目录约定的文本技能，当前版本没有可执行脚本、MCP 配置或网络上传代码。已在 macOS、Codex CLI 0.162.1 环境完成从公开 GitHub 克隆、按本文命令安装、隔离技能发现到真实 `codex exec` 调用的验证；Bash 与 Zsh 安装命令均通过。验证只使用新下载的技能，未借用已有同名安装。不同系统、客户端版本、账号和模型环境仍需自行确认。

Codex 桌面端与 CLI 可通过本地技能目录发现技能。ChatGPT 桌面端的可用性取决于客户端功能和技能发现配置；本仓库尚未验证其端到端调用。复制本地文件不会自动同步到 ChatGPT 网页版或手机端。

技能运行时，宿主模型或工具可能处理用户提供或授权读取的材料。请遵守所在组织的数据与模型使用政策。仓库的示例为虚构场景，提交 Issue、截图或改进示例时也请勿附带真实公司文档、客户信息、凭据或内部链接。

## 修改与贡献

直接修改 `SKILL.md` 或其引用文件即可调整工作流。提交修改时，请说明适用场景和预期行为，检查相对引用是否有效，并使用虚构材料验证。新增文件前请检查内容和 Git 暂存区；`.gitignore` 不能识别 Markdown 正文中的敏感信息。

## 许可证

本项目采用 [MIT License](LICENSE)，允许在保留许可要求的前提下使用、修改和分发，包括商业用途。技能输出需要人工复核，项目按许可证中的 “AS IS” 条款提供。
