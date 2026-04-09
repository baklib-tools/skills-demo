# skills-demo

本仓库演示如何安装并使用 [baklib-tools/skills](https://github.com/baklib-tools/skills) 在多种场景下完成工作。**`main` 分支仅提供本页作为场景导航**；每个具体场景的代码与说明在对应**场景分支**中维护。

## 安装 skills

请参考上游仓库说明：[baklib-tools/skills](https://github.com/baklib-tools/skills)。

## 如何使用本仓库

1. 克隆本仓库。
2. 在下方「场景分支」表中找到目标场景对应的分支名。
3. 检出该分支后继续阅读该分支内的文档（通常为根目录 `README.md`）。

```bash
git checkout <场景分支名>
```

## 场景分支

| 分支名 | 场景说明 | 文档入口 |
| --- | --- | --- |
| `scenario/customer-requirements-baklib-pipeline` | 大量客户需求 → AI 整理与筛选 → 高价值需求入库 Baklib → 逐条分析生成设计方案 → 方案库与可选官网发布 | 检出该分支后阅读根目录 `README.md` |

有场景后，在本表追加一行即可；场景详情以各分支内文档为准。

## 分支命名约定

新增场景分支时统一采用：

```text
scenario/<slug>
```

- **`<slug>`**：小写英文或拼音，多词用连字符 `-` 连接；不使用空格，避免在各类工具中产生问题。
- 新建场景的**完整步骤**见下文「如何新建场景」；Agent 执行时的硬性约定见 [AGENTS.md](AGENTS.md)。

## 如何新建场景

本仓库用 **Git 分支**区分场景：`main` 只保留本导航页，每个场景在独立分支中维护文档与示例。

### 使用 AI 助手（如 Cursor）

你可以直接说「**创建新场景**」，或描述想要的业务场景。助手应按 [AGENTS.md](AGENTS.md) 操作，典型顺序如下：

1. **命名确认**：按上文的 `scenario/<slug>` 规则，向你**提议**分支名和简短场景说明；**在你明确同意之前**，不应改文件、不应提交、不应创建分支。
2. **更新导航**：切换到 **`main`**，在下方「场景分支」表中**新增一行**（分支名、场景说明、文档入口可写「检出该分支后阅读根目录 `README.md`」）。
3. **提交**：**仅提交**本次导航相关变更（通常只有 `README.md`），提交说明可用简体中文（例如「文档：新增场景 xxx 导航」）。
4. **创建场景分支**：在已包含该提交的 **`main`** 上执行 `git checkout -b <已确认的分支名>`。之后该场景的 README、示例与脚本**只在此分支**演进，避免堆在 `main`。
5. **初始化场景技能目录（必须）**：在本分支创建 `.cursor/skills/<slug>/SKILL.md`（`<slug>` 为分支名中 `scenario/` 之后的段），含合法 frontmatter 与占位说明；不得只建分支不建该目录。详见 [AGENTS.md](AGENTS.md)。
6. **初始化构建手记（建议）**：在同分支根目录添加 `HOW-TO-BUILD-THIS-SCENARIO.md` 占位并逐步补充。

更细的规则与例外以 [AGENTS.md](AGENTS.md) 为准。
