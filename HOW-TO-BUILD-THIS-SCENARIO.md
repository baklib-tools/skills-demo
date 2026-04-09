# 如何构建本场景（构建手记）

本文档对应 [AGENTS.md](AGENTS.md) 中的 **「场景构建过程文档」** 约定：面向**复现、扩展或从零重做**本演示场景的人；与 [README.md](README.md) 分工——README 侧重「是什么、怎么用」，本文侧重「怎么把场景搭起来、关键决策与待办」。

---

## 一、仓库级步骤（摘自 AGENTS.md）

在 **skills-demo** 中新增任意演示场景时，Agent 与人类维护者应遵循根目录 [AGENTS.md](AGENTS.md)，核心包括：


| 顺序         | 内容                                                                                                 |
| ---------- | -------------------------------------------------------------------------------------------------- |
| 仓库定位       | 本仓库演示如何安装并使用 [baklib-tools/skills](https://github.com/baklib-tools/skills)；不是 skills 本体。           |
| 分支         | `**main`**：仅场景导航（根目录 [README.md](README.md)）。**场景分支**：每场景独立分支，专属实现与文档不放 `main`。                    |
| 新建场景 1–4   | **命名确认**（未同意不改文件/不提交/不建分支）→ 在 `**main`** 更新场景表 → **仅提交**导航 → **从 `main`** 创建 `scenario/<slug>` 分支。 |
| 新建场景 5（建议） | 创建场景分支后，在本分支根目录维护 `**HOW-TO-BUILD-THIS-SCENARIO.md**`（本文），随实现增量更新。                                 |


日常协作：改具体场景时检出对应场景分支；Git 操作前确认分支与工作区干净；远程协作时 `main` 可先 `git pull`。

---

## 二、本场景分支与目标

- **分支名**：`scenario/customer-requirements-baklib-pipeline`
- **业务目标（摘要）**：大量客户需求 → AI 整理与价值识别 → **Baklib 高价值需求库** → 逐条分析与设计方案 → **Baklib 需求方案库** → 可选官网「产品方案」发布。

---

## 三、构建步骤清单（本场景）

以下为建议顺序；完成一项可在 PR / 提交中勾选或更新本段。

### A. 仓库与文档（已部分完成）

- 在 `main` 的 README「场景分支」表中登记本分支（见 `main` 历史提交）。
- 从 `main` 创建场景分支 `scenario/customer-requirements-baklib-pipeline`。
- 场景 [README.md](README.md)：业务目标、流程图、与 skills 的配合说明、质量与合规注意点。
- **第一步技能安装**：按 [baklib-tools/skills](https://github.com/baklib-tools/skills) 安装 **baklib-mcp**、**baklib-intake-assistant** 至 `.cursor/skills/`（推荐 `npx ctx7 ... --cursor`）；本仓库已提交技能副本便于开箱即用。
- 初始化本文件 `HOW-TO-BUILD-THIS-SCENARIO.md`（当前文档）。

### B. Baklib 与 MCP（待完成）

- 在 Baklib 中确定 **高价值需求库**、**需求方案库**（及可选对外站点/栏目）的落点与命名；约定条目字段（标题、标签、批次 ID、状态、需求↔方案关联等）。
- 按 `.cursor/skills/baklib-mcp/SKILL.md` 配置 **Baklib MCP**（鉴权、server 版本、可用工具），并做连通性验证（读/写最小路径）。
- 选定录入路径：**仅 MCP** 与 **intake 本地镜像 + SQLite 台账**二选一或组合；若用镜像，遵循 `baklib-intake-assistant` 的 `local-mirror.md` 与 `scripts/README.md`。

#### Cursor Agent 窗口与 `${workspaceFolder}`

若在 `~/.cursor/mcp.json` 里为 **baklib-mcp-server** 配置了：

```json
"BAKLIB_MCP_WORKSPACE": "${workspaceFolder}"
```

须注意：**Cursor 的 Agent 窗口**与 **Editor 窗口**所绑定的「工作区根」可能不同，`${workspaceFolder}` 会随**当前窗口**解析。在 **Agent 窗口**单独使用时，其值**未必**等于你在 Editor 里打开的 **`skills-demo` 项目根路径**，从而导致服务去错目录读 **`.config/BAKLIB_MCP_TOKEN`**（或依赖工作区的其它逻辑异常）。

**建议**（任选或组合，按稳定性优先）：

1. 将 `BAKLIB_MCP_WORKSPACE` 设为 **`skills-demo` 仓库的绝对路径**，不依赖 `${workspaceFolder}`。  
2. 或使用全局 **`~/.config/BAKLIB_MCP_TOKEN`**（见 `baklib-mcp` skill），弱化对工作区路径的依赖。  
3. 需要依赖项目内 `.config/` 时，在 **Editor 中打开本项目文件夹**再使用 Agent，并仍建议用绝对路径兜底。

### C. AI 流程与可复现资产（待完成）

- 将「高价值」判定规则写成明确条文（减少模型漂移），并固化到 `prompts/` 或 playbook。
- 分阶段编写提示词 / Playbook：摄入格式、整理打标、入库模板、方案文档结构、人工审核节点、对外脱敏清单。
- **竖切演示**：用少量脱敏或虚构需求跑通：筛选 → 一条进高价值库 → 一条方案进方案库（先手工 + Agent，再考虑自动化）。

### D. 自动化与收尾（可选）

- 批量导入脚本、状态同步、或本仓库专用小 skill / 示例脚本（仍放在**本场景分支**，不污染 `main`）。
- 更新本文件「决策记录」与验证步骤，便于他人复现。

---

## 四、决策记录（增量）


| 日期 | 决策 | 说明 |
| --- | --- | --- |
| 2026-04-09 | Agent 窗口下慎用裸 `${workspaceFolder}` | 单独使用 Cursor Agent 窗口时，`workspaceFolder` 可能不是 Editor 中的项目根；`BAKLIB_MCP_WORKSPACE` 宜用绝对路径或配合 `~/.config/BAKLIB_MCP_TOKEN`。 |


---

## 五、验证与排错（占位）

- **`${workspaceFolder}` 与 Agent 窗口**：见上文 **「B. Baklib 与 MCP」** 小节 **「Cursor Agent 窗口与 `${workspaceFolder}`」**。
- **MCP 不可用**：检查 token、网络、MCP server 版本是否与 `baklib-mcp` 文档一致。
- **ctx7 找不到 `baklib-intake-assistant`**：已采用上游仓库 **手动拷贝** `skills/baklib-intake-assistant/` 至 `.cursor/skills/`（见场景 README）。
- **Python 脚本**：`baklib-intake-assistant/scripts` 依赖见该目录 `requirements.txt`，按需创建 venv。

后续排错步骤随实现补充。