---
name: project-development
description: Simulator Bot 工作区的开发规范。实施需求、修复缺陷或修改受版本控制的代码、配置和文档时使用，按目录分工定位仓库和实现路径，并遵循需求分支、提交、验证及 MR（GitHub 上称 PR）合并流程。
---

# Simulator Bot 项目开发规范

适用于 Simulator Bot 工作区内的各个 Git 仓库，包括规范仓库 `.agent`。

## 开发参考目录

左列为相对于 `simulator-bot/` 工作区根目录的路径，右列的子目录以所在仓库为基准。各工程独立管理 Git 分支和提交。动手前先按下表选定仓库，阅读该仓库的 `README.md` 或 `README.zh-CN.md`，并遵循适用的 `AGENTS.md`。

| 路径 | 用途 |
| --- | --- |
| `.agent/` | 项目开发规范。入口为 `AGENTS.md`，Skill 位于 `skills/project-development/SKILL.md`。 |
| `design-docs/` | 总体架构、跨工程职责与接口边界、实施顺序。从 `README.zh-CN.md` 查总方案。 |
| `industrial-automation-connectors/` | 现场系统接入、设备协议和统一数据契约。Go 服务入口在 `cmd/`，后端实现按职责放在 `internal/`，Web 界面在 `frontend/src/`，Kubernetes 配置在 `deployments/kubernetes/`。 |
| `industrial-world-model/` | 设备、工艺、状态、约束、轨迹和场景快照。当前从 `docs/architecture/` 下的模型边界和实施设计开始。 |
| `automation-agent/` | Agent 的任务规划、工具调用和结果解释。当前从 `docs/architecture/` 下的 Agent 设计开始。 |
| `simu-portal/` | GitHub 组织展示仓库（远端名为 `.github`）。组织主页在 `profile/README.md` 和 `profile/README.zh-CN.md`。 |
| `assets/` | 工作区素材，例如组织头像。涉及素材版本管理时，先确认负责维护的仓库。 |

- 跨工程的职责、接口边界或实施顺序变更写入 `design-docs/`。单个工程的技术方案写入该工程的 `docs/architecture/`。连接器已有 `docs/modules/`，模块设计沿用这个位置。已有中英双语文档时，按 `名称.md` 和 `名称.zh-CN.md` 配对更新。
- `simulation-platform`、`scenario-evaluation` 和 `automation-agent-platform` 已在总体设计中划分职责。当前参考工作区尚无对应检出目录。涉及这些工程时先查 `design-docs/` 并确认对应仓库；新建工程的源码布局随该工程技术方案确定。
- 例如，修改连接器运维界面，进入 `industrial-automation-connectors/`，在 `frontend/src/` 定位实现后从该仓库的目标分支开需求分支。若需求还改变连接器与世界模型的接口边界，同时在 `design-docs/` 更新跨工程设计，并关联两个 PR。

## 按需求开分支

- 每个需求在每个涉及的仓库中使用独立分支。继续已有需求时，复用该需求的分支。
- 开工前确认目标仓库、工作区状态和目标分支。更新远端引用，从最新的远端目标分支创建需求分支。目标分支默认为仓库的默认分支，仓库约定或需求指定了其他目标时按指定执行。保留已有的未提交修改。
- 沿用仓库已有的分支命名约定。没有约定时，可用 `feature/<需求简述>`、`fix/<问题简述>` 或 `docs/<文档简述>`，有需求编号时可带上编号。
- 禁止直接在目标分支上提交需求改动，禁止直接向目标分支推送需求改动。

## 提交并通过 MR 合并

- 提交前检查改动范围，执行与改动相关的验证。提交内容限于当前需求。
- 将需求分支推送到远端，并向约定的目标分支发起 MR。GitHub 上使用 Pull Request（PR）。描述中写明需求或关联工单、主要改动和验证结果，列出未能执行的验证。
- 跨仓库需求在每个修改的仓库分别发起 MR，互相引用。有依赖时，在 MR 中注明合并顺序。
- 按仓库要求完成评审和检查后，通过 MR 合入目标分支。合并后确认 MR 状态为已合并。受权限、评审或检查阻塞时，报告 MR 链接和当前阻塞项。
