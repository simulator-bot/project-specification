# Simulator Bot Project Specification

Use the [project development skill](skills/project-development/SKILL.md) to locate the repository that owns a change, find the relevant code and design documents, and follow the branch and pull request workflow.

From the `simulator-bot/` workspace root, clone this repository as `.agent` alongside the other repositories. If `.agent` is already present, use the existing checkout.

```sh
git clone https://github.com/simulator-bot/project-specification.git .agent
```

When working with a coding agent from the workspace root, use this prompt and add the task below it. When starting from a sibling repository, use `../.agent/AGENTS.md`.

> 先读取 `.agent/AGENTS.md` 及其指向的开发规范，再按规范处理以下需求。
