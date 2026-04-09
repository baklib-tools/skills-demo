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

维护者与 Agent 协作约定见根目录 [AGENTS.md](AGENTS.md)（含「创建新场景」时的命名确认与 Git 流程）。

## 分支命名约定

新增场景分支时统一采用：

```text
scenario/<slug>
```

- **`<slug>`**：小写英文或拼音，多词用连字符 `-` 连接；不使用空格，避免在各类工具中产生问题。
- 与 [AGENTS.md](AGENTS.md) 中「新建场景」流程一致：由维护者或 Agent **先提议分支名并征得同意**，再在 `main` 上更新本表并提交，最后从 `main` 创建该分支。

## 场景分支

| 分支名 | 场景说明 | 文档入口 |
| --- | --- | --- |
| （暂无） | 待补充 | — |

有场景后，在本表追加一行即可；场景详情以各分支内文档为准。
