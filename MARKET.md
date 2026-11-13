# 侧边对话（@eduwork/dsh-side-chat）

> 不打断主线的侧边提问：从当前会话 fork 出独立分支，关掉即归档。
>
> Ask side questions without derailing the main thread; forks a branch and archives it when closed.

## 功能

基于原生 session fork 与 seed，侧边对话拥有独立上下文与工具权限；关闭面板时自动归档分支，不污染主会话历史。

## 安装

```bash
# 在 DSH 中把本目录作为本地 bundle 安装（绝对路径）
```

安装后由 DSH 插件系统加载，条目 id 为 `dsh-side-chat`。

## 依赖

- `@deepseek-ai/cordis`
- `@deepseek-ai/dsh-session`
- `react`

## 兼容性

- `engines.dsh`: `>=0.2.1 <0.3.0`
- 与 EduWork 发行版同源，来源于 ECNU/EduWork 仓库。

## 注意

源码包未包含构建产物 lib/，发布前需在包目录执行 pnpm install && pnpm build（详见 BUILD.md）。

## 许可

MulanPSL-2.0 AND MIT（与上游 EduWork 一致）。

## 入口修正


- 移除悬空声明：files: docs/**/*（目录不存在）
