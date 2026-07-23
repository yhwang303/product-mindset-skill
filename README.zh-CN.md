# Product Mindset Skill

[English](README.md) | [简体中文](README.zh-CN.md)

Product Mindset 是一份面向 AI 编程 Agent 的产品化行为约束 Skill。它把真实产品开发经验固化为可执行规则，让 Agent 不只完成“在开发者机器上能跑”的 Demo，而是关注真实用户能否理解、开始使用、持续使用、信任并安全地完成任务。

它不会把所有项目套进同一套企业级流程。免费共享的小工具不需要被迫设计定价、客服团队和完整商业生命周期；公司内部长期使用、正式上线或涉及敏感数据的产品，则不能跳过可靠性、安全、恢复和合规要求。

## 它会改变 Agent 的哪些行为

在适用场景中，本 Skill 要求 Agent：

- 新产品开始前先显式定义产品级别；
- 区分真实用户证据与开发者或 Agent 的假设；
- 同时比较竞品、通用 AI、人工流程、现有工具组合和“不处理”；
- 检查首次使用路径并减少不必要摩擦；
- 根据暴露范围和失败后果匹配发布要求；
- 实际验证用户路径，而不是只看代码就宣称完成；
- 默认静默落实产品规则，只在需要决策、出现阻断、交付调研或发布验收时报告。

这是一层行为约束，不是安全沙箱。需要硬约束时，应继续配合测试、Hook、CI 门禁、权限控制和外部状态化工具。

## 产品级别

新产品开始实现前，用户必须显式选择或确认级别。

| 级别 | 适用场景 | 典型要求 |
| --- | --- | --- |
| **T0 · 探索原型** | 验证技术、交互或需求假设；不承诺可用 | 假设、验证方法、停止条件；不得称为已产品化 |
| **T1 · 共享小工具** | 免费或开源工具、低风险公开小产品、个人 vibecoding 项目 | 核心价值、最短路径、安装文档、错误恢复、数据边界、局限和基本验证 |
| **T2 · 持续使用产品** | 公司内部多人系统、公开长期服务、使用真实账户或数据 | T1 加指标、权限、可靠性、监控、备份、回滚、支持、升级和迁移 |
| **T3 · 商业或关键产品** | 收费、SLA、敏感数据、关键业务、受监管行业 | T2 加合规、威胁建模、审计、容量、事件响应、正式支持和生命周期 |

产品化不以盈利为前提。但只要免费工具处理凭据、隐私、支付、健康信息或不可逆操作，相应风险要求仍然必须升级。

## 一句话开始使用

上面的级别表就是用户界面，不应再要求用户填写一份很长的产品定义模板。

已经知道级别时，只需说：

```text
使用 product-mindset。我要做的是 T2 产品：<一句话想法>。
```

如果上下文已经讲清楚产品，甚至只需一句：

```text
我要做的是 T2 产品。
```

Skill 会自动进入对应流程，并从现有项目和上下文中获取信息。只有缺失信息会改变级别、范围或安全边界时，Agent 才问一个聚焦问题。

不确定级别时：

```text
使用 product-mindset。帮我判断这个想法属于 T0–T3 哪一级：<一句话想法>。
```

确认后，后续迭代同样保持简短：

```text
继续按 T2 开发，增加团队邀请功能。
```

## 安装

根据 Anthropic 的 [Agent Skills 官方文档](https://docs.anthropic.com/en/docs/claude-code/skills)，Claude Code 会从 `~/.claude/skills/<skill-name>/SKILL.md` 加载个人 Skill，或从 `.claude/skills/<skill-name>/SKILL.md` 加载项目 Skill。

### 方式 A：Claude Code 插件市场安装（推荐，所有系统通用）

在 Claude Code 中运行：

```text
/plugin marketplace add yhwang303/product-mindset-skill
/plugin install product-mindset@product-mindset-skills
/reload-plugins
```

本仓库使用 Anthropic 官方的 [插件市场格式](https://code.claude.com/docs/en/plugin-marketplaces)，后续可以通过 Marketplace/Plugin 更新流程获取新版本。

### 方式 B：macOS 或 Linux 个人安装

Claude Code：

```bash
mkdir -p ~/.claude/skills/product-mindset
curl -L \
  https://raw.githubusercontent.com/yhwang303/product-mindset-skill/main/skills/product-mindset/SKILL.md \
  -o ~/.claude/skills/product-mindset/SKILL.md
```

Cursor：

```bash
mkdir -p ~/.cursor/skills/product-mindset
curl -L \
  https://raw.githubusercontent.com/yhwang303/product-mindset-skill/main/skills/product-mindset/SKILL.md \
  -o ~/.cursor/skills/product-mindset/SKILL.md
```

### 方式 C：Windows PowerShell 个人安装

Claude Code：

```powershell
$dir = Join-Path $HOME ".claude\skills\product-mindset"
New-Item -ItemType Directory -Force $dir | Out-Null
Invoke-WebRequest `
  "https://raw.githubusercontent.com/yhwang303/product-mindset-skill/main/skills/product-mindset/SKILL.md" `
  -OutFile (Join-Path $dir "SKILL.md")
```

Cursor：

```powershell
$dir = Join-Path $HOME ".cursor\skills\product-mindset"
New-Item -ItemType Directory -Force $dir | Out-Null
Invoke-WebRequest `
  "https://raw.githubusercontent.com/yhwang303/product-mindset-skill/main/skills/product-mindset/SKILL.md" `
  -OutFile (Join-Path $dir "SKILL.md")
```

### 方式 D：只安装到一个项目

macOS/Linux：

```bash
mkdir -p .claude/skills/product-mindset
curl -L \
  https://raw.githubusercontent.com/yhwang303/product-mindset-skill/main/skills/product-mindset/SKILL.md \
  -o .claude/skills/product-mindset/SKILL.md
```

Windows PowerShell：

```powershell
$dir = ".claude\skills\product-mindset"
New-Item -ItemType Directory -Force $dir | Out-Null
Invoke-WebRequest `
  "https://raw.githubusercontent.com/yhwang303/product-mindset-skill/main/skills/product-mindset/SKILL.md" `
  -OutFile (Join-Path $dir "SKILL.md")
```

如果希望仓库中的所有协作者使用同一规则，应提交项目级 Skill。

### 方式 E：让 Agent 直接安装

把下面的 Prompt 发给能够访问文件系统和 GitHub 的 Agent：

```text
请从下面的仓库安装 Product Mindset Agent Skill：
https://github.com/yhwang303/product-mindset-skill

修改文件前：
1. 读取 skills/product-mindset/SKILL.md，确认其中没有脚本或可执行 Hook。
2. 把它安装为个人 Skill：~/.claude/skills/product-mindset/SKILL.md。
3. 如果目标位置已有文件，先备份，不要静默覆盖。
4. 复制后验证 YAML frontmatter。
5. 告诉我安装路径，并展示一句话选择 T0–T3 的使用 Prompt。
```

Cursor 使用 `~/.cursor/skills/product-mindset/SKILL.md`；项目级安装使用 `.claude/skills/product-mindset/SKILL.md`。

## 验证安装

向 Agent 发送：

```text
使用 product-mindset Skill。用一句话分别解释 T0–T3，然后展示一句话选择产品级别的 Prompt。
```

如果找不到 Skill：

1. 确认目录名是 `product-mindset`。
2. 确认文件名严格为 `SKILL.md`。
3. 确认 YAML frontmatter 以 `---` 开始和结束。
4. 如果此前不存在顶层 skills 目录，重启 Claude Code 后再试。

## 更新与卸载

手动安装时，重新执行安装命令即可更新。

删除 Claude Code 个人安装：

```bash
rm -rf ~/.claude/skills/product-mindset
```

Windows PowerShell：

```powershell
Remove-Item -Recurse -Force (Join-Path $HOME ".claude\skills\product-mindset")
```

删除前应再次确认路径。项目级与 Cursor 安装请使用前文对应路径。

## 仓库结构

```text
.
├── .claude-plugin/
│   └── marketplace.json
├── skills/
│   └── product-mindset/
│       └── SKILL.md
├── README.md
├── README.zh-CN.md
└── LICENSE
```

## 参与贡献

欢迎提交 Issue 和 Pull Request。修改应保持以下核心原则：

- 根据风险分层，不用一套企业检查表约束所有项目；
- 真实证据优先于 Agent 自我评价；
- 新产品必须显式确认产品级别；
- 普通实现过程中尽量减少可见的仪式化产品评论；
- 安全与数据保护阻断项不能通过选择更低级别来豁免。

## License

MIT
